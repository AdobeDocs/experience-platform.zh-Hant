---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；邊緣分段；邊緣分段；串流邊緣；
solution: Experience Platform
title: 使用API進行邊緣劃分
description: 本檔案包含如何搭配Adobe Experience Platform區段服務API使用邊緣區段的範例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# 邊緣分割

>[!NOTE]
>
>下列檔案說明如何使用API執行邊緣分段。 如需使用UI執行邊緣分段的資訊，請參閱 [邊緣劃分UI指南](../ui/edge-segmentation.md).
>
>現在所有Platform使用者都能使用邊緣區段。 如果您在測試期間建立邊緣區段，這些區段將可繼續運作。

邊緣分段是即時評估Adobe Experience Platform中邊緣區段的功能，可啟用相同的頁面和下一頁個人化使用案例。

>[!IMPORTANT]
>
> 邊緣資料會儲存在最靠近其收集位置的邊緣伺服器位置，並可儲存在指定為中樞（或主要）Adobe Experience Platform資料中心以外的位置。
>
> 此外，邊緣分段引擎只會執行邊緣上有的請求 **one** 主要標示身分，與非邊緣型主要身分一致。

## 快速入門

本開發人員指南需要妥善了解 [!DNL Adobe Experience Platform] 與邊緣細分相關的服務。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。
- [[!DNL Segmentation]](../home.md):提供從 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

若要成功呼叫任何Experience PlatformAPI端點，請參閱 [Platform API快速入門](../../landing/api-guide.md) 以了解必要標題及如何讀取範例API呼叫。

## 邊緣分段查詢類型 {#query-types}

為了使用邊緣分段來評估區段，查詢必須符合下列准則：

| 查詢類型 | 詳細資訊 | 範例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 單一事件 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | 已將項目新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單一設定檔 | 任何參考單一僅限設定檔屬性的區段定義 | 住在美國的人。 | `homeAddress.countryCode = "US"` |
| 參照設定檔的單一事件 | 任何區段定義，是指一或多個設定檔屬性以及沒有時間限制的單一傳入事件。 | 訪問首頁的美國居民。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 使用設定檔屬性否定單一事件 | 任何區段定義，是指否定的單一傳入事件和一或多個設定檔屬性 | 住在美國並擁有 **not** 造訪首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 一個時間範圍內的單一事件 | 任何區段定義，是指在指定的時間內單一傳入事件。 | 過去24小時內造訪首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 時間視窗內具有設定檔屬性的單一事件 | 任何區段定義，指的是一或多個設定檔屬性，以及設定時間內的單一傳入事件。 | 過去24小時內造訪首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 在時間窗口內用配置檔案屬性否定單個事件 | 任何區段定義，指的是一或多個設定檔屬性以及一段時間內否定的單一傳入事件。 | 住在美國並擁有 **not** 在過去24小時內瀏覽了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| 24小時時段內的頻率事件 | 任何區段定義，是指在24小時的時間範圍內發生特定次數的事件。 | 造訪首頁的人員 **至少** 24小時內五次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時段內具有設定檔屬性的頻率事件 | 任何區段定義，指的是一或多個設定檔屬性，以及在24小時的時間範圍內發生特定次數的事件。 | 訪問首頁的美國人 **至少** 24小時內五次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時段內使用設定檔否定頻率事件 | 任何區段定義，指的是一或多個設定檔屬性，以及在24小時的時間範圍內發生特定次數的否定事件。 | 未訪問首頁的人 **更多** 在過去的24小時里不過5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小時的時間設定檔內傳入多個點擊 | 任何區段定義，是指在24小時的時間範圍內發生的多個事件。 | 瀏覽首頁的人員 **或** 在過去24小時內瀏覽了結帳頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時段內使用設定檔執行多個事件 | 任何區段定義，是指在24小時的時間範圍內發生的一或多個設定檔屬性和多個事件。 | 訪問首頁的美國人 **和** 在過去24小時內瀏覽了結帳頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 區段 | 包含一或多個批次或串流區段的任何區段定義。 | 居住在美國且位於「現有區段」區段的人。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查詢 | 任何參考屬性地圖的區段定義。 | 根據外部區段資料新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

此外，區段 **必須** 系結至邊緣上作用中的合併原則。 有關合併策略的詳細資訊，請閱讀 [合併策略指南](../../profile/api/merge-policies.md).

區段定義將 **not** 在下列情況下啟用邊緣分段功能：

- 區段定義包含單一事件和 `inSegment` 事件。
   - 不過，若 `inSegment` 事件僅限設定檔，區段定義 **will** 啟用邊緣分割功能。

## 擷取為邊緣細分啟用的所有區段

您可以向 `/segment/definitions` 端點。

**API格式**

若要擷取已啟用邊緣分段功能的區段，您必須包含查詢參數 `evaluationInfo.synchronous.enabled=true` 在請求路徑中。

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回IMS組織中已啟用邊緣分段的區段陣列。 如需傳回之區段定義的詳細資訊，請參閱 [區段定義端點指南](./segment-definitions.md).

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
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

## 建立已啟用邊緣分段的區段

您可以向 `/segment/definitions` 符合其中一個端點 [上面列出的邊緣細分查詢類型](#query-types).

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>以下範例是建立區段的標準請求。 如需建立區段定義的詳細資訊，請參閱 [建立區段](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

**回應**

成功的回應會傳回新建立的區段定義的詳細資訊，此定義已啟用邊緣分段功能。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## 後續步驟

現在您知道如何建立啟用邊緣分段的區段，可以使用它們來啟用相同頁面和下一頁個人化的使用案例。

若要了解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪 [區段產生器使用手冊](../ui/segment-builder.md).

## 附錄

下節列出邊緣區段的常見問題：

### 邊緣網路上可用區段需要多久的時間？

在邊緣網路上可用區段最多需要1小時。