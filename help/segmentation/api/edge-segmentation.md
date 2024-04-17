---
solution: Experience Platform
title: 使用API的邊緣細分
description: 本檔案包含如何搭配Adobe Experience Platform Segmentation Service API使用邊緣區段的範例。
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# 邊緣分段

>[!NOTE]
>
>以下檔案說明如何使用API執行邊緣細分。 如需使用UI執行邊緣區段的資訊，請參閱 [邊緣分段UI指南](../ui/edge-segmentation.md).
>
>邊緣區段現在可供所有Platform使用者普遍使用。 如果您在Beta版期間建立邊緣區段定義，這些區段定義仍可繼續運作。

邊緣區段能讓您在Adobe Experience Platform的邊緣即時評估區段定義，啟用相同頁面和下一頁個人化使用案例。

>[!IMPORTANT]
>
> 邊緣資料將會儲存在距離收集地點最近的邊緣伺服器位置，而且可能會儲存在指定為Adobe Experience Platform資料中心中心（或主體）以外的位置。
>
> 此外，邊緣區段引擎只會處理有以下情況的邊緣請求： **一** 主要標籤的身分，這與非edge型的主要身分一致。

## 快速入門

這份開發人員指南需要您實際瞭解各種 [!DNL Adobe Experience Platform] 邊緣細分涉及的服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者個人檔案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從建立對象 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

為了成功呼叫任何Experience Platform API端點，請閱讀以下指南： [Platform API快速入門](../../landing/api-guide.md) 以瞭解必要的標頭以及如何讀取範例API呼叫。

## 邊緣細分查詢型別 {#query-types}

為了使用邊緣區段來評估區段，查詢必須符合以下准則：

| 查詢型別 | 詳細資料 | 範例 | PQL範例 |
| ---------- | ------- | ------- | ----------- |
| 單一事件 | 任何會參照沒有時間限制的單一傳入事件的區段定義。 | 將專案新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單一設定檔 | 任何參考單一設定檔屬性的區段定義 | 美國居民。 | `homeAddress.countryCode = "US"` |
| 參考設定檔的單一事件 | 任何參考一或多個設定檔屬性以及沒有時間限制的單一傳入事件的區段定義。 | 居住在美國的人造訪了首頁。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 否定具有設定檔屬性的單一事件 | 任何參考已否定單一傳入事件和一個或多個設定檔屬性的區段定義 | 居住在美國且擁有 **非** 造訪了首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 時間範圍內的單一事件 | 任何參照一段時間內單一傳入事件的區段定義。 | 過去24小時內造訪過首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 在少於24小時的相對時間範圍內，具有設定檔屬性的單一事件 | 任何區段定義，會參照具有一或多個設定檔屬性的單一傳入事件，且會在少於24小時的相對時間範圍內發生。 | 居住在美國的人在過去24小時內瀏覽了首頁。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 在時間範圍內否定具有設定檔屬性的單一事件 | 任何區段定義，會參照一或多個設定檔屬性，以及一段時間內否定單一傳入事件。 | 居住在美國且擁有 **非** 在過去24小時內造訪了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| 24小時時間範圍內的頻率事件 | 任何分段定義，會參照在24小時之時間範圍內發生特定次數的事件。 | 造訪首頁的人 **至少** 過去24小時內5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間範圍內具有設定檔屬性的頻率事件 | 任何區段定義，會參照一或多個設定檔屬性，以及在24小時之時間範圍內發生特定次數的事件。 | 造訪首頁的美國人 **至少** 過去24小時內5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間範圍內具有設定檔的否定頻率事件 | 任何區段定義，會參照一或多個設定檔屬性，以及在24小時之時間範圍內發生特定次數之否定事件。 | 尚未造訪首頁的人 **更多** 在過去24小時內超過五次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24小時內時間設定檔中有多個傳入點選 | 任何會參照24小時內發生之多個事件的區段定義。 | 造訪過首頁的人 **或** 在過去24小時內造訪過結帳頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時間範圍內有多個具有設定檔的事件 | 任何區段定義，會參照在24小時之時間範圍內發生的一或多個設定檔屬性和多個事件。 | 造訪首頁的美國人 **和** 在過去24小時內造訪過結帳頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 區段區段 | 包含一或多個批次或串流區段的任何區段定義。 | 居住在美國且處於「現有區段」區段的人員。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 參考地圖的查詢 | 任何參照屬性對應的區段定義。 | 已根據外部區段資料新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

此外，區段 **必須** 繫結至在edge上作用中的合併原則。 如需有關合併原則的詳細資訊，請參閱 [合併原則指南](../../profile/api/merge-policies.md).

區段定義會 **非** 在下列情況下啟用邊緣分段：

- 區段定義包含單一事件和 `inSegment` 事件。
   - 但是，如果區段包含在 `inSegment` 事件只是設定檔，區段定義 **將** 啟用邊緣區段。
- 區段定義會使用「忽略年份」作為其時間限制的一部分。

## 擷取所有已啟用邊緣細分的區段

您可以透過向以下網站發出GET請求，擷取貴組織內所有啟用邊緣劃分的區段清單： `/segment/definitions` 端點。

**API格式**

若要擷取已啟用邊緣細分的區段，您必須包含查詢引數 `evaluationInfo.synchronous.enabled=true` 在請求路徑中。

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

成功的回應會傳回組織中已啟用邊緣區段的一系列區段。 有關傳回的區段定義的詳細資訊，請參閱 [區段定義端點指南](./segment-definitions.md).

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

您可以透過向以下發出POST請求，建立已啟用邊緣劃分的區段： `/segment/definitions` 符合下列任一專案的端點： [上面列出的邊緣區段查詢型別](#query-types).

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>以下範例是建立區段的標準請求。 如需建立區段定義的詳細資訊，請參閱以下教學課程： [建立區段](../tutorials/create-a-segment.md).

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
    }
}'
```

**回應**

成功的回應會傳回為邊緣細分啟用的新建立區段定義的詳細資料。

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

現在您知道如何建立啟用邊緣細分的區段，就能使用它們來啟用相同頁面和下一頁個人化使用案例。

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪 [區段產生器使用手冊](../ui/segment-builder.md).

## 附錄

下節列出與邊緣細分相關的常見問題：

### 區段需要多久才能在Edge Network上使用？

區段在Edge Network上可供使用最多需要一小時。