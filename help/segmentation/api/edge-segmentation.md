---
keywords: Experience Platform；主題；流行主題；分段；分段；分段服務；邊緣分段；邊緣分段；流動邊緣；
solution: Experience Platform
title: 使用API的邊緣分割
description: 本文檔包含如何使用Adobe Experience Platform分段服務API進行邊緣分段的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# 邊緣分割

>[!NOTE]
>
>以下文檔說明如何使用API執行邊緣分割。 有關使用UI執行邊緣分割的資訊，請閱讀 [邊緣分割UI指南](../ui/edge-segmentation.md)。
>
>現在，所有平台用戶都可以使用邊緣分割。 如果在測試期間建立了邊段，則這些段將繼續運行。

邊緣分割是一種在邊緣上即時評估Adobe Experience Platform區段的能力，使同一頁和下一頁個性化使用案例成為可能。

>[!IMPORTANT]
>
> 邊緣資料將儲存在最靠近其收集位置的邊緣伺服器位置，並且可以儲存在指定為集線器（或主體）Adobe Experience Platform資料中心的位置以外的位置。
>
> 此外，邊緣分割引擎將僅處理存在邊緣的請求 **一個** 主標籤標識，與非基於邊緣的主標識一致。

## 快速入門

本開發人員指南要求對各種 [!DNL Adobe Experience Platform] 與邊緣分割相關的服務。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個源的聚合資料即時提供統一的用戶配置檔案。
- [[!DNL Segmentation]](../home.md):提供從您的 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

要成功調用任何Experience PlatformAPI終結點，請閱讀上的指南 [平台API入門](../../landing/api-guide.md) 瞭解所需標頭以及如何讀取示例API調用。

## 邊緣分割查詢類型 {#query-types}

要使用邊緣分割來評估段，查詢必須符合以下准則：

| 查詢類型 | 詳細資訊 | 範例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 單個事件 | 任何引用無時間限制的單個傳入事件的段定義。 | 已將物料添加到購物車中的人員。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單個配置檔案 | 引用單個僅配置檔案屬性的任何段定義 | 住在美國的人。 | `homeAddress.countryCode = "US"` |
| 引用配置檔案的單個事件 | 引用一個或多個配置檔案屬性和單個傳入事件且沒有時間限制的任何段定義。 | 訪問首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 使用配置檔案屬性否定單個事件 | 任何引用否定的單個傳入事件和一個或多個配置檔案屬性的段定義 | 生活在美國並擁有 **不** 已訪問首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 時間窗口內的單個事件 | 任何段定義，它指的是在設定的時間段內的單個傳入事件。 | 過去24小時內訪問首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 時間窗口內具有配置檔案屬性的單個事件 | 在設定的時間段內引用一個或多個配置檔案屬性和單個傳入事件的任何段定義。 | 過去24小時內訪問首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 在時間窗口內使用配置檔案屬性否定單個事件 | 指一個或多個配置檔案屬性和一個時間段內否定的單個傳入事件的任何段定義。 | 生活在美國並擁有 **不** 在過去24小時內訪問了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| 24小時時間窗內的頻率事件 | 任何段定義，指在24小時的時間窗口內發生一定次數的事件。 | 訪問首頁的人 **至少** 24小時內有5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間窗口內具有配置檔案屬性的頻率事件 | 指一個或多個配置檔案屬性以及在24小時的時間窗口內發生一定次數的事件的任何段定義。 | 訪問首頁的美國人 **至少** 24小時內有5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間窗口內使用配置檔案否定頻率事件 | 任何段定義，它指一個或多個配置檔案屬性以及在24小時的時間窗口內發生一定次數的已取消事件。 | 未訪問首頁的人 **更多** 比過去24小時里多了5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小時內的時間配置檔案內多次傳入命中 | 任何段定義，指在24小時的時間窗口內發生的多個事件。 | 訪問首頁的人員 **或** 在過去24小時內訪問了簽出頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時間窗口內使用配置檔案的多個事件 | 任何段定義，它指在24小時的時間窗口內發生的一個或多個配置檔案屬性和多個事件。 | 訪問首頁的美國人 **和** 在過去24小時內訪問了簽出頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 分部 | 包含一個或多個批或流段的任何段定義。 | 居住在美國並屬於&quot;現有部門&quot;的人。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查詢 | 任何引用屬性映射的段定義。 | 已基於外部段資料添加到購物車中的人員。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

此外，該分部 **必須** 綁定到邊緣上處於活動狀態的合併策略。 有關合併策略的詳細資訊，請閱讀 [合併策略指南](../../profile/api/merge-policies.md)。

段定義將 **不** 在以下情況下啟用邊緣分割：

- 段定義包括單個事件和 `inSegment` 的子菜單。
   - 然而，倘分部包含於 `inSegment` 事件僅是配置檔案，段定義 **會** 啟用邊緣分割。

## 檢索所有為邊緣分割啟用的段

通過向組織中發出GET請求，可以檢索組織內啟用了邊緣分割的所有段的清單 `/segment/definitions` 端點。

**API格式**

要檢索為邊緣分割啟用的段，必須包括查詢參數 `evaluationInfo.synchronous.enabled=true` 的子菜單。

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

成功的響應將返回組織中啟用邊緣分割的段陣列。 有關返回的段定義的詳細資訊，請參見 [段定義端點指南](./segment-definitions.md)。

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

## 建立啟用邊緣分割的段

可通過向POST請求建立允許邊緣分割的段 `/segment/definitions` 與其中一個 [上面列出的邊緣分割查詢類型](#query-types)。

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>下面的示例是建立段的標準請求。 有關建立段定義的詳細資訊，請閱讀有關 [建立段](../tutorials/create-a-segment.md)。

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

成功的響應將返回新建立的段定義的詳細資訊，該定義啟用了邊緣分割。

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

現在您知道如何建立啟用邊緣分割的段，可以使用這些段啟用同一頁和下一頁個性化使用案例。

要瞭解如何使用Adobe Experience Platform用戶介面執行類似操作和使用段，請訪問 [段生成器使用手冊](../ui/segment-builder.md)。

## 附錄

以下部分列出了有關邊緣分割的常見問題：

### 在邊緣網路上提供一個網段需要多長時間？

在邊緣網路上可用的網段最多需要一個小時。