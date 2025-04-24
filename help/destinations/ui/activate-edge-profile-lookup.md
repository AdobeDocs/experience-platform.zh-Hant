---
title: 即時查詢邊緣設定檔屬性
description: 瞭解如何使用自訂Personalization目的地和Edge Network API即時查詢邊緣設定檔屬性
type: Tutorial
exl-id: e185d741-af30-4706-bc8f-d880204d9ec7
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 3%

---

# 即時查詢邊緣上的設定檔屬性

Adobe Experience Platform使用[即時客戶個人檔案](../../profile/home.md)作為所有個人檔案資料的單一信任來源。 為了快速即時擷取資料，它使用[邊緣設定檔](../../profile/edge-profiles.md)，這些設定檔是分散在整個[Edge Network](../../collection/home.md#edge)的輕量型設定檔。 這可提供快速、即時的個人化使用案例。

## 使用案例 {#use-cases}

以下是邊緣設定檔查詢可協助使用的兩個使用案例。

* **即時Personalization**：從邊緣設定檔快速擷取設定檔資訊，以個人化使用者在您網站上的體驗。
* **客戶支援**：當客戶致電支援中心代理時，即時擷取設定檔資訊。

此頁面說明您必須遵循的步驟，以便即時查詢邊緣設定檔資料、提供個人化體驗，或透過下游應用程式通知決策規則。

## 術語和先決條件 {#prerequisites}

設定本頁面所述的使用案例時，您將使用下列Experience Platform元件：

* [資料串流](../../datastreams/overview.md)：資料串流會接收來自Web SDK的傳入事件資料，並以邊緣設定檔資料回應。
* [合併原則](../../segmentation/ui/segment-builder.md#merge-policies)：您將建立[!UICONTROL Edge上的Active-On]合併原則，以確保邊緣設定檔使用正確的設定檔資料。
* [自訂Personalization連線](../catalog/personalization/custom-personalization.md)：您將設定新的自訂個人化連線，以將設定檔屬性傳送至Edge Network。
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)：您將使用Edge Network API [互動式資料集合](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)功能，從邊緣設定檔快速擷取設定檔屬性。

## 效能護欄 {#guardrails}

Edge設定檔查詢使用案例須受下表所述的特定效能護欄約束。 如需Edge Network API護欄的詳細資訊，請參閱護欄[檔案頁面](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/)。

| Edge Network服務 | Edge區段 | 每秒要求數 |
|---------|----------|---------|
| [透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)自訂個人化目的地](../catalog/personalization/custom-personalization.md) | 是 | 1500 |
| [透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)自訂個人化目的地](../catalog/personalization/custom-personalization.md) | 無 | 1500 |

## 步驟1：建立和設定資料流 {#create-datastream}

請依照[資料流設定](../../datastreams/configure.md#create-a-datastream)檔案中的步驟，使用下列&#x200B;**[!UICONTROL 服務]**&#x200B;設定來建立新的資料流：

* **[!UICONTROL 服務]**： [!UICONTROL Adobe Experience Platform]
* **[!UICONTROL Personalization目的地]**：已啟用
* **[!UICONTROL Edge分段]**：如果您需要邊緣分段，請啟用此選項。 如果您只想在邊緣上查詢設定檔屬性，但不想根據邊緣設定檔執行任何分段，則請停用此選項。


  <!-- >[!IMPORTANT]
    >
    >Enabling edge segmentation limits the maximum number of lookup requests to 1500 request per second. If you need a higher request throughput, disable edge segmentation for your datastream. See the [guardrails documentation](../guardrails.md#edge-destinations-activation) for detailed information. -->

  ![顯示資料流設定畫面的Experience Platform UI影像。](../assets/ui/activate-edge-profile-lookup/datastream-config.png)


## 步驟2：設定您的對象以進行邊緣評估 {#audience-edge-evaluation}

在Edge上查詢設定檔屬性時，需要針對邊緣評估設定您的對象。

確定您計畫啟用的對象已將[Edge上作用中合併原則](../../segmentation/ui/segment-builder.md#merge-policies)設定為預設值。 [!DNL Active-On-Edge]合併原則可確保持續評估邊緣](../../segmentation/methods/edge-segmentation.md)上的對象[，並可用於即時個人化使用案例。

依照[建立合併原則](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)上的指示進行，並確定啟用&#x200B;**[!UICONTROL Edge上主動式合併原則]**&#x200B;切換按鈕。

>[!IMPORTANT]
>
>如果您的對象使用不同的合併原則，您將無法從邊緣擷取設定檔屬性，且您將無法執行邊緣設定檔查詢。

## 步驟3：將設定檔屬性資料傳送至Edge Network{#configure-custom-personalization-connection}

為了即時查詢邊緣設定檔，包括屬性和對象成員資格資料，這些資料必須在Edge Network上提供。 為此，您必須建立與&#x200B;**[!UICONTROL 具有屬性的自訂Personalization]**&#x200B;目的地的連線，並啟用對象，包括您想在邊緣設定檔上查閱的屬性。

+++ 使用屬性連線設定自訂Personalization

請依照[目的地連線建立教學課程](../ui/connect-destination.md)中的指示進行，以取得有關如何建立新目的地連線的詳細說明。

設定新目的地時，請在&#x200B;**[!UICONTROL 資料串流識別碼]**&#x200B;欄位中選取您在[步驟1](#create-datastream)中建立的資料串流。 對於&#x200B;**[!UICONTROL 整合別名]**，您可以使用任何有助於您日後識別此目的地連線的值，例如目的地名稱。

![Experience Platform UI影像顯示「具有屬性的自訂Personalization」設定畫面。](../assets/ui/activate-edge-profile-lookup/destination-config.png)

+++

+++透過屬性連線啟用自訂Personalization的對象

建立具有屬性&#x200B;]**的**[!UICONTROL &#x200B;自訂Personalization連線後，您就可以將設定檔資料傳送至Edge Network了。

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用工作流程的[對應步驟](#mapping)，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;以及&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
> 
> 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

1. 移至&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   在Experience Platform UI中反白顯示![目的地目錄索引標籤。](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 尋找&#x200B;**[!UICONTROL 具有屬性的自訂Personalization]**&#x200B;目的地卡片，然後選取&#x200B;**[!UICONTROL 啟用對象]**，如下圖所示。

   ![在目錄中的目的地卡上反白顯示啟用對象控制項。](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 選取您先前設定的目的地連線，然後選取&#x200B;**[!UICONTROL 下一步]**。

   ![在啟動工作流程中選取目的地步驟。](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 選取您的對象。 使用對象名稱左邊的核取方塊來選取您要啟用至目的地的對象，然後選取&#x200B;**[!UICONTROL 下一步]**。

   您可以根據對象的來源，從多種對象型別中進行選取：

   * **[!UICONTROL 細分服務]**：細分服務在Experience Platform中產生的對象。 如需詳細資訊，請參閱[分段檔案](../../segmentation/ui/overview.md)。
   * **[!UICONTROL 自訂上傳]**：對象是在Experience Platform外部產生，並以CSV檔案形式上傳至Experience Platform。 若要深入瞭解外部對象，請參閱有關[匯入對象](../../segmentation/ui/overview.md#import-audience)的檔案。
   * 其他型別的對象，源自其他Adobe解決方案，例如[!DNL Audience Manager]。

     ![選取啟用工作流程的對象步驟，並反白數個對象。](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

1. 選取您要讓邊緣輪廓可用的輪廓屬性。

   * **選取來源屬性**。 若要新增來源屬性，請在&#x200B;**[!UICONTROL Source欄位]**&#x200B;欄位上選取&#x200B;**[!UICONTROL 新增欄位]**&#x200B;控制項，然後搜尋或導覽至您想要的XDM屬性欄位，如下所示。

     ![熒幕錄製，顯示如何在對應步驟中選取目標屬性。](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

   * **選取目標屬性**。 若要新增目標屬性，請選取&#x200B;**[!UICONTROL 目標欄位]**&#x200B;欄位上的&#x200B;**[!UICONTROL 新增欄位]**&#x200B;控制項，並輸入您要對應來源屬性的自訂屬性名稱。

     ![顯示如何在對應步驟](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)中選取XDM屬性的熒幕錄製



當您完成對應設定檔屬性時，請選取&#x200B;**[!UICONTROL 下一步]**。

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您可以看到選取專案的摘要。 選取&#x200B;**[!UICONTROL 取消]**&#x200B;以中斷流程，**[!UICONTROL 上一步]**&#x200B;以修改您的設定，或&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始將設定檔資料傳送至Edge Network。

![檢閱步驟中的選擇摘要。](../assets/ui/activate-edge-personalization-destinations/review.png)

+++

+++同意原則評估

如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。如需詳細資訊，請參閱[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。

**資料使用原則檢查**

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟中，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 在解決違規之前，您無法完成對象啟用工作流程。 如需有關如何解決原則違規的資訊，請參閱資料治理檔案一節中的關於[資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)。

![資料原則違規的範例。](../assets/common/data-policy-violation.png)

+++

+++篩選對象

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟中，您可以使用頁面上的可用篩選器來僅顯示其排程或對應已隨著此工作流程而更新的對象。 您也可以切換要檢視的表格欄。

![熒幕錄製，顯示稽核步驟中可用的對象篩選器。](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)


如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取[完成] **[!UICONTROL 以確認您的選擇。]**

+++

## 步驟4：在邊緣上查詢設定檔屬性 {#configure-edge-profile-lookup}

現在您應該已完成[設定資料串流](#create-datastream)，您已[建立新的具有屬性的自訂Personalization目的地連線](#configure-destination)，而且您已使用此連線來[傳送設定檔屬性](#activate-audiences)，以便查閱Edge Network。

下一步是設定個人化解決方案，以從邊緣設定檔擷取設定檔屬性。

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 若要保護此資料，您必須透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/)擷取設定檔屬性。 此外，您必須透過Edge Network API [互動式資料收集端點](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)擷取設定檔屬性，才能驗證API呼叫。
><br>如果您不遵循上述要求，個人化將僅以對象成員資格為基礎，而且您將無法取得設定檔屬性。

您在[步驟1](#create-datastream)中設定的資料流現在已準備好接受傳入的事件資料並以邊緣設定檔資訊回應。

設定您的整合以擷取邊緣設定檔資訊，如下列範例所示。

### 請求 {#request}

若要擷取邊緣設定檔資料，請傳送空的`POST`呼叫至`/interact`端點，其中包含您要查詢包含在事件中的設定檔屬性的主要身分，如下所示。

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
    "event":
    {
        "xdm": {
            "identityMap": {
                "Email": [
                    {  
                        "id":"test123@adobetest.com",
                        "primary":true
                    }
                ]
            }
        }
    }
    
}'
```

| 參數 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 您在[步驟1](#create-datastream)中建立的資料流的資料流識別碼。 |

### 回應 {#response}

成功的回應會傳回HTTP狀態`200 OK`，其中的`Handle`物件包含與下列標籤中範例類似的資訊，端視設定檔是否位於邊緣而定。

>[!NOTE]
>
>API回應是模組化的，`handle`物件可包含多種型別的`payload`物件。 與Edge設定檔查詢相關的資訊會分組到`payload`具有`"type": "activation:pull"`的物件下，

>[!BEGINTABS]

>[!TAB 設定檔存在於邊緣]

如果設定檔存在於邊緣，根據啟動至邊緣的設定檔屬性和對象，您可以預期會有與以下內容類似的屬性和對象會籍回應。

```json
{
  "requestId": "3c600138-d785-42ca-a025-bb725f4b5da9",
  "handle": [
    {
      "payload": [
        {
          "type": "profileLookup",
          "destinationId": "9218b727-ec59-4a46-b8b9-05503f138c5d",
          "alias": "rk-demo-custom-personalization-XXXX",
          "attributes": {
            "zip": {
              "value": "19000"
            },
            "firstName": {
              "value": "Test"
            },
            "lastName": {
              "value": "User123"
            },
            "gender": {
              "value": "male"
            },
            "city": {
              "value": "Philadelphia"
            },
            "state": {
              "value": "PA"
            },
            "email": {
              "value": "test123@adobetest.com"
            }
          },
          "segments": [
            {
              "id": "85018bd8-7ad1-4e17-ae30-8389c04bd3c0",
              "namespace": "ups"
            },
            {
              "id": "d09a8159-8b30-4178-b2f2-7a8c5e3168d9",
              "namespace": "ups"
            }
          ]
        }
      ],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

`handle`物件提供下表所述的資訊。

| 參數 | 說明 |
|---------|----------|
| `payload` | 包含邊緣查詢資訊的`payload`物件。 回應可能包含多個其他`payload`物件，與邊緣查詢無關。 |
| `type` | 負載會依其型別分組在回應中。 邊緣設定檔查詢的裝載型別一律設為`profileLookup`。 |
| `destinationId` | 您在[步驟3](#configure-custom-personalization-connection)中建立的&#x200B;**[!UICONTROL 自訂Personalization]**&#x200B;連線執行個體的識別碼。 |
| `alias` | 目的地連線的別名，由使用者在建立[自訂Personalization](../catalog/personalization/custom-personalization.md)目的地連線時設定。 |
| `attributes` | 此陣列包含您在[步驟3](#configure-custom-personalization-connection)中啟動之對象的邊緣設定檔屬性。 |
| `segments` | 此陣列包含您在[步驟3](#configure-custom-personalization-connection)中啟用的對象。 |
| `type` | `handle`物件依型別分組。 若是邊緣設定檔查詢使用案例，`handle`物件的型別一律為`activation:pull`。 |
| `eventIndex` | Edge Network會以陣列的形式從使用者端接收事件。 陣列中事件的順序會在處理期間保留，並會反映在此索引中。 事件索引從`0`開始。 |

>[!TAB 邊緣上不存在設定檔]

如果邊緣上沒有設定檔，您可以預期類似以下的回應。

```json
{
  "requestId": "531b541a-4541-419e-ac99-fd7e452f0c0f",
  "handle": [
    {
      "payload": [],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

`handle`物件提供下表所述的資訊。

| 參數 | 說明 |
|---------|----------|
| `payload` | 當設定檔不存在於邊緣時，`payload`物件為空白。 |
| `type` | `payload`物件依型別分組。 若是邊緣設定檔查詢使用案例，`payload`物件的型別一律為`activation:pull`。 |
| `eventIndex` | Edge Network會以陣列的形式接收來自使用者端的事件。 陣列中事件的順序會在處理期間保留，並會反映在此索引中。 事件索引從`0`開始。 |

>[!ENDTABS]

>[!SUCCESS]
>
>如果您已正確設定整合，您現在可以存取邊緣設定檔資料，且可以使用邊緣設定檔的屬性和對象成員資格，在下游個人化引擎中觸發即時個人化。

## 結論 {#conclusion}

依照上述步驟，您可以有效率地即時查詢邊緣設定檔屬性，透過下游應用程式實現個人化體驗和明智的決策。
