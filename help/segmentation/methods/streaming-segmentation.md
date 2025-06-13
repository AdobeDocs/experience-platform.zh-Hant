---
solution: Experience Platform
title: 串流分段指南
description: 瞭解串流細分是什麼、如何建立使用串流細分評估的受眾，以及如何檢視使用串流細分建立的受眾。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 6935cee30adb59d52db6c6fed7036f81b54edd52
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 2%

---

# 串流分段指南

>[!BEGINSHADEBOX]

>[!NOTE]
>
>串流細分資格標準已於2025年5月20日更新。

+++資格更新

>[!IMPORTANT]
>
>目前使用串流或邊緣區段評估的所有現有區段定義仍會繼續依原樣運作，除非加以編輯或更新。

## 規則集 {#ruleset}

任何符合下列規則集的&#x200B;**新區段或編輯的**&#x200B;區段定義都將&#x200B;**不再使用**&#x200B;串流或邊緣區段進行評估。 相反地，將會使用批次區段來評估這些區段。

- 時間超過24小時的單一事件
   - 使用過去3天內檢視過網頁的所有設定檔啟用對象。
- 沒有時間範圍的單一事件
   - 使用所有檢視了網頁的設定檔來啟用對象。

## 時間段 {#time-window}

為了使用串流細分評估對象，它&#x200B;**必須**&#x200B;限制在24小時時間範圍內。

## 在串流對象中包含批次資料 {#include-batch-data}

在此更新之前，您可以建立結合批次和串流資料來源的串流對象定義。 不過，透過最新更新，使用批次和串流資料來源建立對象時，將會使用批次細分進行評估。

如果您需要使用符合更新後規則集的串流或邊緣細分來評估區段定義，您需要明確建立批次和串流規則集，並使用區段區段將它們合併。 此批次規則集&#x200B;**必須**&#x200B;以設定檔結構描述為基礎。

例如，假設您有兩個對象，其中一個對象容納設定檔結構描述資料，另一個則容納體驗事件結構描述資料：

| 客群 | 結構描述 | Source型別 | 查詢定義 | 客群 ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| 加州居民 | 輪廓 | 批次 | 住家地址在加利福尼亞州 | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| 最近結帳 | 體驗事件 | 串流 | 在過去24小時內至少有一個結帳 | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

如果您想在串流對象中使用批次元件，必須使用區段參考批次對象。

因此，將兩個對象結合在一起的規則集範例如下所示：

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

將使用串流細分來評估產生的對象&#x200B;**，因為它透過參考批次對象元件來運用批次對象的成員資格。

不過，如果您想要結合兩個對象與事件資料，您&#x200B;**無法**&#x200B;只結合這兩個事件。 您需要建立兩個對象，然後建立另一個使用`inSegment`來參照這兩個對象的對象。

例如，假設您有兩個對象，這兩個對象都會容納體驗事件結構描述資料：

| 客群 | 結構描述 | Source型別 | 查詢定義 | 客群 ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| 最近的放棄 | 體驗事件 | 批次 | 過去24小時內至少有一個放棄事件 | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| 最近結帳 | 體驗事件 | 串流 | 在過去24小時內至少有一個結帳 | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

在此情況下，您需要建立第三個對象，如下所示：

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>所有符合規則集的現有區段定義都將繼續使用串流或邊緣區段進行評估，直到編輯為止。
>
>此外，目前符合其他串流或邊緣區段評估標準的所有現有區段定義，仍將使用串流或邊緣區段進行評估。

## 合併原則 {#merge-policy}

任何符合串流或邊緣分段&#x200B;**資格的**&#x200B;新或已編輯&#x200B;**區段定義，都必須**&#x200B;位於「Edge上的&#39;a5&#39;5c用」合併原則上。

如果沒有作用中的合併原則集，您需要[設定您的合併原則](../../profile/merge-policies/ui-guide.md#configure)，並將它設定為在Edge上作用中。


+++

>[!ENDSHADEBOX]

串流細分是近乎即時評估Adobe Experience Platform中的受眾，同時專注於資料豐富度的能力。

有了串流區隔，當串流資料進入Experience Platform時，對象資格就會立即生效，無需排程及執行區隔工作。 這可讓您在資料傳入Experience Platform時評估資料，讓對象成員資格自動保持在最新狀態。

## 合格的規則集 {#rulesets}

>[!IMPORTANT]
>
>為了使用串流分段，您&#x200B;**必須**&#x200B;使用「在Edge上有效」的合併原則。 如需合併原則的詳細資訊，請閱讀[合併原則概觀](../../profile/merge-policies/overview.md)。

如果規則集符合下表所列的任何條件，就符合串流區段的資格。

>[!NOTE]
>
>為了讓串流細分發揮作用，您需要為組織啟用已排程的分段。 如需啟用排程細分的詳細資訊，請參閱[對象入口網站概觀](../ui/audience-portal.md#scheduled-segmentation)。

| 查詢型別 | 詳細資料 | 查詢 | 範例 |
| ---------- | ------- | ----- | ------- |
| 少於24小時時間範圍內的單一事件 | 任何會參照少於24小時之時間範圍內的單一傳入事件的區段定義。 | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![顯示相對時間範圍內單一事件的範例。](../images/methods/streaming/single-event.png) |
| 僅限設定檔 | 僅參考設定檔屬性的任何區段定義。 | `homeAddress.country.equals("US", false)` | ![顯示的設定檔屬性範例。](../images/methods/streaming/profile-attribute.png) |
| 在少於24小時的相對時間範圍內，具有設定檔屬性的單一事件 | 任何區段定義，會參照具有一或多個設定檔屬性的單一傳入事件，且會在少於24小時的相對時間範圍內發生。 | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![顯示相對時間範圍內具有設定檔屬性的單一事件範例。](../images/methods/streaming/single-event-with-profile-attribute.png) |
| 24小時相對時間範圍內的多個事件 | 任何在過去24小時&#x200B;**內參考多個事件**&#x200B;且（選擇性）具有一或多個設定檔屬性的區段定義。 | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![顯示具有設定檔屬性的多個事件範例。](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

在下列情況下，區段定義將&#x200B;**不**&#x200B;適用於串流分段：

- 區段定義包含Adobe Audience Manager (AAM)區段或特徵。
- 區段定義包括多個實體（多實體查詢）。
- 區段定義包含單一事件和`inSegment`事件的組合。
   - 例如，在單一規則集中鏈結下列專案： `inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and  CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false))  WHEN(<= 24 hours before now)])`。
- 區段定義會使用「忽略年份」作為其時間限制的一部分。

請注意下列適用於串流細分查詢的准則：

| 查詢型別 | 方針 |
| ---------- | -------- |
| 單一事件規則集 | 回顧期間限製為&#x200B;**一天**。 |
| 使用事件歷史記錄進行查詢 | <ul><li>回顧期間限製為&#x200B;**一天**。</li><li>事件之間必須有嚴格的時間排序條件&#x200B;**且**。</li><li>支援至少具有一個否定事件的查詢。 不過，整個事件&#x200B;**不可**&#x200B;為否定。</li></ul> |

如果區段定義經過修改，使其不再符合串流區段的條件，則區段定義會自動從「串流」切換為「批次」。

此外，區段取消資格（類似於區段資格）會即時發生。 因此，如果對象不再符合區段的資格，則會立即取消資格。 例如，如果區段定義要求「過去三小時內購買紅鞋子的所有使用者」，三小時後，所有最初符合區段定義資格的設定檔都將不合格。

### 合併對象 {#combine-audiences}

若要合併來自批次和串流來源的資料，您必須將批次和串流元件分隔為個別的對象。

### 設定檔屬性和體驗事件 {#profile-and-event}

例如，我們考慮以下兩個範例對象：

| 客群 | 結構描述 | Source型別 | 查詢定義 | 客群 ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| 加州居民 | 輪廓 | 批次 | 住家地址在加利福尼亞州 | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| 最近結帳 | 體驗事件 | 串流 | 在過去24小時內至少有一個結帳 | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

如果您想在串流對象中使用批次元件，必須使用區段參考批次對象。

因此，將兩個對象結合在一起的規則集範例如下所示：

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

將使用串流細分來評估產生的對象&#x200B;**，因為它透過參考批次對象元件來運用批次對象的成員資格。

### 多個體驗事件 {#two-events}

如果您想要結合多個對象與事件資料，您&#x200B;**不能**&#x200B;只結合這些事件。 您必須為每個事件建立對象，然後建立另一個使用`inSegment`來參照所有對象的對象。

例如，假設您有兩個對象，這兩個對象都會容納體驗事件結構描述資料：

| 客群 | 結構描述 | Source型別 | 查詢定義 | 客群 ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| 最近的放棄 | 體驗事件 | 批次 | 在過去48小時內至少有一個放棄事件 | `7deb246a-49b4-4687-95f9-6316df049948` |
| 最近結帳 | 體驗事件 | 串流 | 在過去24小時內至少有一個結帳 | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

在此情況下，您需要建立第三個對象，如下所示：

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948) and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

## 建立客群 {#create-audience}

您可以使用Segmentation Service API或透過UI中的對象入口網站，建立使用串流細分來評估的對象。

如果區段定義符合[合格的規則集](#eligible-rulesets)之一，則可啟用串流功能。

>[!BEGINTABS]

>[!TAB 分段服務API]

**API格式**

```http
POST /segment/definitions
```

**要求**

+++ 建立已啟用串流細分之區段定義的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": false
            },
            "continuous": {
                "enabled": true
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及您新建立區段定義的詳細資料。

+++建立區段定義時的範例回應。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

在[區段定義端點指南](../api/segment-definitions.md)中找到有關使用此端點的詳細資訊。

>[!TAB Audience Portal]

在對象入口網站中，選取&#x200B;**[!UICONTROL 建立對象]**。

![對象入口網站中會醒目顯示[建立對象]按鈕。](../images/methods/streaming/select-create-audience.png)

彈出視窗隨即顯示。 選取&#x200B;**[!UICONTROL 建置規則]**&#x200B;以輸入區段產生器。

![「建立對象」彈出視窗中會醒目顯示「建置規則」按鈕。](../images/methods/streaming/select-build-rules.png)

在區段產生器中，建立符合其中一個[合格規則集](#eligible-rulesets)的區段定義。 如果區段定義符合串流區段的資格，您就可以選取&#x200B;**[!UICONTROL 串流]**&#x200B;作為&#x200B;**[!UICONTROL 評估方法]**。

![會顯示區段定義。 評估型別已反白顯示，顯示可以使用串流區段來評估區段定義。](../images/methods/streaming/streaming-evaluation-method.png)

若要深入瞭解如何建立區段定義，請參閱[區段產生器指南](../ui/segment-builder.md)

>[!ENDTABS]

## 擷取對象 {#retrieve-audiences}

您可以使用Segmentation Service API或透過UI中的對象入口網站，擷取使用串流細分評估的所有對象。

>[!BEGINTABS]

>[!TAB 分段服務API]

向`/segment/definitions`端點發出GET要求，以擷取使用組織內串流細分評估的所有區段定義清單。

**API格式**

您必須在要求路徑中包含查詢引數`evaluationInfo.synchronous.enabled=true`，以擷取使用串流細分評估的區段定義。

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**要求**

+++ 列出所有已啟用串流之區段定義的範例請求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含貴組織中已啟用串流細分的區段定義陣列。

+++此範例回應包含貴組織中所有已啟用串流區段定義的清單

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

在[區段定義端點指南](../api/segment-definitions.md)中找到有關傳回的區段定義的詳細資訊。

+++

>[!TAB Audience Portal]

您可以使用Audience Portal中的篩選條件，擷取貴組織內針對串流細分啟用的所有對象。 選取![篩選器圖示](../../images/icons/filter.png)圖示以顯示篩選器清單。

![對象入口網站中會醒目顯示篩選圖示。](../images/methods/filter-audiences.png)

在可用的篩選器內，移至&#x200B;**[!UICONTROL 更新頻率]**&#x200B;並選取[!UICONTROL 串流]。 使用此篩選器會顯示貴組織中使用串流細分評估的所有對象。

![已選取串流更新頻率，顯示組織中使用串流細分評估的所有對象。](../images/methods/streaming/filter-streaming.png)

若要進一步瞭解如何在Experience Platform中檢視對象，請參閱[對象入口網站指南](../ui/audience-portal.md)。

>[!ENDTABS]

## 客群詳細資料 {#audience-details}

您可以在對象入口網站中選取串流區隔，以檢視使用串流區隔評估的特定對象詳細資料。

在Audience Portal上選取對象後，對象詳細資訊頁面就會顯示。 這會顯示對象的相關資訊，包括對象詳細資訊的摘要、一段時間內合格設定檔的數量，以及對象已啟用的目的地。

![對於使用串流細分評估的對象，會顯示對象詳細資訊頁面。](../images/methods/streaming/audience-details.png)

針對已啟用串流的對象，會顯示&#x200B;**[!UICONTROL 設定檔特定時段]**&#x200B;卡片，其中顯示合格的總數以及新對象更新的量度。

根據此對象的批次和串流評估，**[!UICONTROL 合格總計]**&#x200B;量度代表合格對象的總數。

**[!UICONTROL 新對象已更新]**&#x200B;量度以折線圖表示，該折線圖顯示透過串流細分而發生的對象人數變化。 您可以調整下拉式清單以顯示過去24小時、上週或過去30天。

![已醒目提示一段時間的設定檔卡片。](../images/methods/streaming/profiles-over-time.png)

如需對象詳細資料的詳細資訊，請參閱[對象入口網站概觀](../ui/audience-portal.md#audience-details)。

## 後續步驟

本指南說明串流啟用區段定義如何在Adobe Experience Platform上運作，以及如何監視串流啟用區段定義。

若要進一步瞭解如何使用Adobe Experience Platform使用者介面，請參閱[分段使用手冊](./overview.md)。

如需有關串流區段的常見問題，請參閱常見問題](../faq.md#streaming-segmentation)的[串流區段區段。
