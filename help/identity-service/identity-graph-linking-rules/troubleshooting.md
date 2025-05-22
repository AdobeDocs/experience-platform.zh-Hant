---
title: 身分圖表連結規則疑難排解指南
description: 瞭解如何疑難排解身分圖表連結規則中的常見問題。
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: c9b5de33de91b93f179b4720f692eb876e94df72
workflow-type: tm+mt
source-wordcount: '3295'
ht-degree: 0%

---

# [!DNL Identity Graph Linking Rules]的疑難排解指南

當您測試及驗證[!DNL Identity Graph Linking Rules]時，您可能會遇到一些與資料擷取和圖表行為相關的問題。 閱讀本檔案以瞭解如何疑難排解您在使用[!DNL Identity Graph Linking Rules]時可能會遇到的一些常見問題。

## 資料擷取流程概觀 {#data-ingestion-flow-overview}

下圖是資料如何流入Adobe Experience Platform和應用程式的簡化表示。 使用此圖表作為參考，協助您更清楚瞭解此頁面的內容。

![資料擷取在Identity Service中的流程圖表。](../images/troubleshooting/dataflow_in_identity.png "識別服務中資料擷取的流程圖表。"){zoomable="yes"}

請務必注意下列因素：

* 對於串流資料，即時客戶設定檔、身分服務和資料湖將在資料傳送後開始處理資料。 不過，完成資料處理的延遲需視服務而定。 通常而言，與設定檔和身分識別相比，資料湖需要更長的時間來處理。
   * 如果資料在數小時後對資料集執行查詢時仍沒有顯示，則資料很可能未內嵌到Experience Platform中。
* 針對批次資料，所有資料將先流入資料湖，然後如果資料集已啟用設定檔和身分功能，資料將傳播到設定檔和身分識別中。
* 對於內嵌相關問題，務必要在服務層級隔離問題，以便進行精確的偵錯和疑難排解。 需要考慮三種潛在問題型別：

| 擷取問題型別 | 資料會擷取到Data Lake中嗎？ | 資料會內嵌在設定檔中嗎？ | 資料會內嵌在Identity Service中嗎？ |
| --- | --- | --- | --- |
| 一般擷取問題 | 無 | 無 | 無 |
| 圖表問題 | 是 | 是 | 無 |
| 設定檔片段問題 | 是 | 無 | 是 |

## 資料擷取問題 {#data-ingestion-issues}

>[!NOTE]
>
>* 本節假設資料已成功擷取至Data Lake，且沒有語法或其他錯誤會阻止資料先擷取至Experience Platform。
>
>* 這些範例使用ECID作為Cookie名稱空間，使用CRMID作為人員名稱空間。

### 我的身分未內嵌到Identity Service中{#my-identities-are-not-getting-ingested-into-identity-service}

發生此情形有多種原因，包括但不限於下列各項：

* [未針對設定檔](../../catalog/datasets/enable-for-profile.md)啟用資料集。
* 系統會略過記錄，因為事件中只有一個身分。
* [識別服務](../guardrails.md#identity-value-validation)發生驗證失敗。
   * 例如，ECID可能超過38個字元的最大長度。
* 依預設，[AAID會封鎖擷取](../guardrails.md#identity-namespace-ingestion)。
* 身分已移除，因為[系統護欄](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)。

在[!DNL Identity Graph Linking Rules]的內容中，可能會拒絕識別服務的記錄，因為傳入事件有兩個或多個具有相同唯一名稱空間但不同識別值的識別。 發生此情形通常是因為實作錯誤。

考量下列事件有兩個假設：

1. 欄位名稱CRMID會以名稱空間CRMID標示為身分。
2. 名稱空間CRMID定義為唯一的名稱空間。

下列事件將傳回錯誤訊息，指出擷取失敗。

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**疑難排解步驟**

若要解決此錯誤，您必須先收集下列資訊：

* 您預期要在身分圖形中內嵌的身分值(`identity_value`)。
* 傳送事件的資料集(`dataset_name`)。

接下來，使用[Adobe Experience Platform查詢服務](../../query-service/home.md)並執行下列查詢：

>[!TIP]
>
>將`dataset_name`和`identity_value`取代為您收集的資訊。

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

執行查詢後，尋找您預期產生圖形的事件記錄，然後驗證同一列中的身分值是否不同。 檢視下列影像以取得範例：

![產生重複名稱空間的未命名查詢。](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>如果兩個身分完全相同，而且事件是透過串流擷取，則身分和設定檔都會刪除身分重複。

### 驗證後ExperienceEvents被歸因到錯誤的已驗證設定檔

名稱空間優先順序在事件片段判斷主要身分的方式中會扮演重要角色。

* 設定並儲存指定沙箱的[身分設定](./identity-settings-ui.md)後，設定檔就會使用[名稱空間優先順序](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events)來判斷主要身分。 在identityMap的情況下，設定檔將不再使用`primary=true`旗標。
* 雖然設定檔將不再參考此標幟，但Experience Platform上的其他服務可能會繼續使用`primary=true`標幟。

為了將[已驗證的使用者事件](implementation-guide.md#ingest-your-data)繫結至人員名稱空間，所有已驗證的事件都必須包含人員名稱空間(CRMID)。 這表示即使使用者登入後，每個已驗證的事件上仍必須存在人員名稱空間。

在設定檔檢視器中查詢設定檔時，您可能會繼續看到`primary=true`個「事件」標幟。 不過，此專案會被忽略，且不會由設定檔使用。

預設會封鎖AAID。 因此，如果您使用[Adobe Analytics來源聯結器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)，您必須確定ECID的優先順序高於ECID，讓未驗證的事件具有ECID的主要身分識別。

**疑難排解步驟**

1. 若要驗證驗證事件是否同時包含人員和Cookie名稱空間，請閱讀[疑難排解未擷取至身分識別服務之資料的錯誤一節中概述的步驟](#my-identities-are-not-getting-ingested-into-identity-service)。
2. 若要驗證驗證事件是否具有人員名稱空間的主要身分（例如CRMID），請使用不拼接合併原則（這是不使用私人圖表的合併原則）在設定檔檢視器上搜尋人員名稱空間。 此搜尋只會傳回與人員名稱空間關聯的事件。

### 我的體驗事件片段未內嵌到設定檔中 {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

您的體驗事件片段未擷取至設定檔中的原因有很多，包含但不限於：

* [未針對設定檔](../../catalog/datasets/enable-for-profile.md)啟用資料集。
* [設定檔](../../xdm/classes/experienceevent.md)可能發生驗證失敗。
   * 例如，體驗事件必須同時包含`_id`和`timestamp`。
   * 此外，每個事件（記錄）的`_id`必須是唯一的。

在名稱空間優先順序的情境下，設定檔將拒絕任何包含兩個或多個具有最高名稱空間優先順序的身分的事件。 例如，如果GAID未標籤為唯一的名稱空間，且有兩個身分都具有GAID名稱空間和不同的身分值傳入，則設定檔不會儲存任何事件。

**疑難排解步驟**

如果您的資料已傳送至Data Lake但未傳送設定檔，而您認為這是因為在單一事件中傳送了兩個以上具有最高名稱空間優先順序的身分，則可執行下列查詢以驗證針對相同名稱空間傳送了兩個不同的身分值：

>[!TIP]
>
>在下列查詢中，您必須：
>
>* 以傳送身分的路徑取代`_testimsorg.identification.core.email`。
>* 以最高優先順序的名稱空間取代`Email`。 這是未擷取的相同名稱空間。
>* 以您要查詢的資料集取代`dataset_name`。

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

此查詢假設：

* 一個身分會從identityMap傳送，另一個身分會從身分描述項傳送。 **注意**：在Experience Data Model (XDM)結構描述中，身分描述項是標示為身分的欄位。
* CRMID會透過identityMap傳送。 如果CRMID是以欄位傳送，請從WHERE子句移除`key='Email'`。

>[!NOTE]
>
>**在WebSDK實作與ECID重複上**：如果ECID欄位標示為身分（身分描述項）而非identityMap，則在identityMap中產生第二個ECID。 由於單一事件中出現兩個ECID，這種複製可能會導致Real-time Customer Profile無法儲存匿名事件。

## 圖表行為相關問題 {#graph-behavior-related-issues}

本節概述您可能會遇到的有關身分圖表行為方式的常見問題。

### 未驗證的ExperienceEvents被附加到錯誤的已驗證設定檔

身分最佳化演演算法會接受[最近建立的連結，並移除最舊的連結](./identity-optimization-algorithm.md#identity-optimization-algorithm-details)。 因此，啟用此功能後，ECID可能會從一個人重新指派（重新連結）至另一個人。 若要瞭解身分在一段時間內如何連結的歷史記錄，請遵循下列步驟：

**疑難排解步驟**

>[!NOTE]
>
>下列步驟將擷取下列假設下的資訊：
>
>* 單一資料集正在使用中（這不會查詢多個資料集）。
>
>* 由於[進階資料生命週期管理](../../hygiene/home.md)、[Privacy Service](../../privacy-service/home.md)或其他執行刪除的服務已刪除，因此資料不會從資料湖中刪除。

首先，您必須收集下列資訊：

1. 已傳送之Cookie名稱空間（例如ECID）和人員名稱空間（例如CRMID）的身分符號(namespaceCode)。
1.1.針對Web SDK實作，這些通常是identityMap中包含的名稱空間。
1.2.對於Analytics來源聯結器實作，這些是identityMap中包含的Cookie識別碼。 個人識別碼是標籤為身分的eVar欄位。
2. 在中傳送事件的資料集(dataset_name)。
3. 要查閱的Cookie名稱空間身分值(identity_value)。

身分符號(namespaceCode)區分大小寫。 若要擷取identityMap中指定資料集的所有身分符號，請執行以下查詢：

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

如果您不知道Cookie識別碼的身分值，而想要搜尋已連結至多個人員識別碼的Cookie ID，則必須執行下列查詢。 此查詢假設ECID為Cookie名稱空間，CRMID為人員名稱空間。

>[!BEGINTABS]

>[!TAB Web SDK實作]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Analytics來源聯結器實施]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**注意：**&#x200B;人員ID參考描述項的路徑。 您可以在結構描述下找到此資訊。

>[!ENDTABS]

現在您已識別連結至多個人員ID的Cookie值，請從結果中取一個，並在以下查詢中使用它來取得該Cookie值連結至不同人員ID時的時間順序檢視：

>[!BEGINTABS]

>[!TAB Web SDK實作]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Analytics來源聯結器實施]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**注意**：此範例假設`eVar10`已標示為身分。 針對您的設定，您必須根據自己組織的實作變更eVar。

>[!ENDTABS]

### 身分最佳化演演算法未如預期「運作」

**疑難排解步驟**

請參閱有關[身分最佳化演演算法](./identity-optimization-algorithm.md)的檔案，以及支援的圖表結構型別。

* 閱讀[圖形組態指南](./example-configurations.md)以取得支援的圖形結構範例。
* 您也可以閱讀[實作指南](./implementation-guide.md#appendix)，以取得不支援的圖表結構範例。 有兩種情況可能發生：
   * 您的所有設定檔中沒有單一名稱空間。
   * 發生[「擱置識別碼」](./implementation-guide.md#dangling-loginid-scenario)個狀況。 在此案例中，Identity Service無法判斷暫留ID是否與圖形中的任何個人實體相關聯。

您也可以在UI[&#128279;](./graph-simulation.md)中使用圖形模擬工具來模擬事件，並設定您自己的唯一名稱空間和名稱空間優先順序設定。 這麼做有助於您基本瞭解「身分最佳化演演算法」應有的行為。

如果您的模擬結果與圖形行為預期相符，則可以檢查您的[身分設定](./identity-settings-ui.md)是否與您在模擬中設定的設定相符。

### 即使在設定身分設定後，我仍會在沙箱中看到摺疊的圖表

在儲存設定後&#x200B;_身分圖表將遵循您設定的唯一名稱空間和名稱空間優先順序_。 在&#x200B;_之前您儲存新設定的任何「摺疊」圖形，在擷取新資料以更新摺疊的圖形之前，都不會受到影響。_&#x200B;即使名稱空間優先順序有所變更，即時客戶設定檔上的事件片段的主要身分也不會更新。

**疑難排解步驟**

您可以使用[身分圖表檢視器](../features/identity-graph-viewer.md)來檢查您的圖表是在設定之前或之後擷取。 檢查[!UICONTROL 連結屬性]下上次更新的時間戳記，以檢視Identity Service何時擷取圖形。 如果時間戳記在設定之前，則表示在啟用功能之前已建立「摺疊」圖形。

![具有範例圖形的身分圖表檢視器。](../images/troubleshooting/graph_viewer.png)

### 我想知道我的沙箱中有多少「摺疊」的圖表

使用身分儀表板來深入分析身分圖表的狀態，例如身分計數和圖表。 請參閱量度「具有多個名稱空間的圖表計數」，以取得已收合的圖表計數 — 這些圖表包含兩個或多個具有相同名稱空間的身分。 假設沙箱沒有資料，並且您已將名稱空間（例如CRMID）設定為唯一，則預期應該有零個具有兩個或更多CRMID的圖表。 在下列範例中，有兩個圖表包含兩個或多個電子郵件地址。

![身分儀表板，包含兩個以上名稱空間的身分計數、圖表計數、名稱空間計數、大小圖表計數和圖表計數等量度。](../images/troubleshooting/identity_dashboard.png)

您可以執行下列查詢，在Data Lake的[設定檔快照匯出資料集](../../dashboards/query.md)中找到詳細的劃分：

>[!NOTE]
>
>* 將`dataset_name`取代為您的資料集實際名稱。
>
>* 這些計數可能並不完全相符。 身分儀表板是以身分圖表計數為基礎，而以下查詢是以具有兩個或多個身分的設定檔計數為基礎。 資料會由服務獨立處理和更新。

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

您可以在設定檔快照匯出資料集中使用以下查詢，以從「摺疊」的圖形取得範例身分。

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>如果沙箱未針對共用裝置臨時方法啟用，則上述兩個查詢將產生預期結果，且行為與[!DNL Identity Graph Linking Rules]不同。

## 常見問題 {#faq}

本節概述有關[!DNL Identity Graph Linking Rules]常見問題的解答清單。

## 身分最佳化演演算法 {#identity-optimization-algorithm}

請閱讀本節，瞭解有關[身分最佳化演演算法](./identity-optimization-algorithm.md)的常見問題解答。

### 我的每個企業單位(B2C CRMID、B2B CRMID)都有一個CRMID，但我所有的設定檔中沒有唯一的名稱空間。 如果我將B2C CRMID和B2B CRMID標示為唯一，並啟用我的身分設定，會發生什麼事？

此情境不受支援。 因此，當使用者使用其B2C CRMID登入，而另一個使用者使用其B2B CRMID登入時，您可能會看到圖形摺疊。 如需詳細資訊，請參閱實作頁面中[單一人員名稱空間需求](./implementation-guide.md#single-person-namespace-requirement)一節。

### 身分最佳化演演算法是否會「修正」現有的收合圖形？

現有收合的圖形只有在您儲存新設定後更新時，才會受到圖形演演算法的影響（「固定」）。

### 如果兩個人使用同一部裝置登入和登出，事件會發生什麼事？ 所有事件是否會轉移給最後驗證的使用者？

* 匿名事件（在即時客戶個人檔案上以ECID為主要身分的事件）將傳輸給最後驗證的使用者。 這是因為ECID將連結至上次驗證使用者（位於Identity Service）的CRMID。
* 所有已驗證的事件（CRMID定義為主要身分的事件）將保留在人員身分。

如需詳細資訊，請閱讀[判斷體驗事件](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events)的主要身分的指南。

### 當ECID從一個人傳輸至另一個人時，Adobe Journey Optimizer中的歷程會受到哪些影響？

上次驗證使用者的CRMID將會連結至ECID （共用裝置）。 ECID可根據使用者行為從一個人重新指派給另一個人。 影響將取決於如何建構歷程，因此客戶在開發沙箱環境中測試歷程以驗證行為非常重要。

重點如下：

* 設定檔進入歷程後，ECID重新指派不會導致設定檔在歷程中結束。
   * 圖表變更不會觸發歷程退出。
* 如果設定檔不再與ECID相關聯，則在使用對象資格的條件時，這可能會導致變更歷程路徑。
   * ECID移除可能會變更與設定檔相關聯的事件，進而導致對象資格變更。
* 歷程的重新進入取決於歷程屬性。
   * 如果您停用重新進入歷程，當設定檔從該歷程退出時，相同的設定檔將在91天內不會重新進入（根據全域歷程逾時）。
* 如果歷程以ECID名稱空間開始，則進入的設定檔和收到動作的設定檔(例如 電子郵件、選件)可能會因歷程的設計方式而異。
   * 例如，如果動作之間存在等待條件，且在等待期間會傳輸ECID，則可能會鎖定不同的設定檔。
   * 透過此功能，ECID不再一律與一個設定檔相關聯。
   * 建議使用人員名稱空間(CRMID)開始歷程。

>[!TIP]
>
>歷程應查詢具有唯一名稱空間的設定檔，因為非唯一名稱空間可能會重新指派給其他使用者。
>
>* ECID及非唯一電子郵件/電話名稱空間可從一個人移動至另一個人。
>* 如果歷程有等待條件，且如果這些非唯一名稱空間用於在歷程中查詢設定檔，則歷程訊息可能會傳送給錯誤的人。

## 命名空間優先順序

請閱讀本節，瞭解有關[名稱空間優先順序](./namespace-priority.md)的常見問題解答。

### 我已啟用我的身分設定。 如果在啟用設定後新增自訂名稱空間，我的設定會發生什麼事？

名稱空間有兩個「貯體」：人員名稱空間和裝置/Cookie名稱空間。 新建立的自訂名稱空間在每個「貯體」中的優先順序最低，因此這個新的自訂名稱空間不會影響現有的資料擷取。

### 如果即時客戶設定檔不再使用identityMap上的「主要」標幟，是否仍需傳送此值？

是，identityMap上的「主要」旗標已由其他服務使用。 如需詳細資訊，請閱讀[名稱空間優先順序對其他Experience Platform服務的影響](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services)指南。

### 名稱空間優先順序是否會套用至即時客戶個人檔案中的個人檔案記錄資料集？

不可以。 名稱空間優先順序僅適用於使用XDM ExperienceEvent類別的體驗事件資料集。

### 此功能如何與每個圖表50個身分的身分圖表護欄搭配運作？ 名稱空間優先順序是否會影響此系統定義的護欄？

將先套用身分最佳化演演算法，以確保個人實體表示。 之後，如果圖表嘗試超過[身分圖表護欄](../guardrails.md) （每個圖表50個身分），則會套用此邏輯。 名稱空間優先順序不會影響50身分/圖表護欄的刪除邏輯。

## 測試

請閱讀本節，以取得有關[!DNL Identity Graph Linking Rules]中測試和偵錯功能的常見問題解答。

### 我應該在開發沙箱環境中測試哪些情境？

一般而言，在開發沙箱上測試應模擬您打算在生產沙箱上執行的使用案例。 請參考下表以瞭解進行全面測試時需驗證的一些關鍵區域：

| 測試案例 | 測試步驟 | 預期結果 |
| --- | --- | --- |
| 精確的個人實體表示 | <ul><li>模擬匿名瀏覽</li><li>模擬兩個使用者(John、Jane)使用相同裝置登入</li></ul> | <ul><li>John和Jane都應該與其屬性和已驗證事件相關聯。</li><li>最後驗證的使用者應與匿名瀏覽事件相關聯。</li></ul> |
| 區段 | 建立四個區段定義（**注意**：每一對區段定義都應該使用批次評估一個區段定義，並使用另一個串流評估。） <ul><li>區段定義A：根據John的已驗證事件和/或屬性的區段資格。</li><li>區段定義B：根據Jane的已驗證事件和/或屬性的區段資格。</li></ul> | 無論共用裝置情況為何，John和Jane都應該符合各自的區段資格。 |
| Adobe Journey Optimizer上的對象資格/單一歷程 | <ul><li>從對象資格活動（例如上面建立的串流細分）開始建立歷程。</li><li>建立以單一事件開始的歷程。 此單一事件應為已驗證的事件。</li><li>建立這些歷程時，您必須停用重新進入。</li></ul> | <ul><li>無論共用裝置情況為何，John和Jane都應觸發其應輸入的個別歷程。</li><li>當ECID傳回給John和Jane時，他們不應重新進入歷程。</li></ul> |

{style="table-layout:auto"}

### 如何驗證此功能是否如預期運作？

使用[圖表模擬工具](./graph-simulation.md)來驗證功能是否可在個別的圖表層級運作。

若要在沙箱層級驗證功能，請參閱身分儀表板中具有多個名稱空間的[!UICONTROL 圖表計數]區段。