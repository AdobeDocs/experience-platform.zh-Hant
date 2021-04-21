---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；邊緣分段；邊緣分段；流邊緣；
solution: Experience Platform
title: '使用API進行邊緣區段 '
topic-legacy: developer guide
description: 本檔案包含如何搭配Adobe Experience Platform分段服務API使用邊緣分段的範例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# 邊緣分段（測試版）

>[!NOTE]
>
>下列檔案說明如何使用API執行邊緣分段。 如需使用UI執行邊緣分段的資訊，請閱讀[邊緣分段UI指南](../ui/edge-segmentation.md)。 此外，邊緣區段目前也在測試中。 文件和功能可能會有所變更。

邊緣區段是指能夠即時評估Adobe Experience Platform邊緣區段的能力，讓相同的頁面和下一頁個人化使用案例。

## 快速入門

本開發人員指南需要對邊緣區隔相關的各種[!DNL Adobe Experience Platform]服務有良好的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
- [[!DNL Segmentation]](../home.md):提供從資料建立區段和觀眾的 [!DNL Real-time Customer Profile] 能力。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

為了成功呼叫[!DNL Data Prep] API端點，請閱讀[平台API](../../landing/api-guide.md)快速入門手冊，以瞭解必要標題以及如何讀取範例API呼叫。

## 邊緣分段查詢類型{#query-types}

若要使用邊緣分段來評估區段，查詢必須符合下列准則：

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 |
| 頻率查詢 | 任何區段定義，指發生至少特定次數之事件。 |
| 參照描述檔的頻率查詢 | 任何區段定義，是指發生至少特定次數且具有一或多個描述檔屬性的事件。 |

{style=&quot;table-layout:auto&quot;}

下列查詢類型為&#x200B;**not**，目前受邊緣分段支援：

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 相對時間窗口 | 如果查詢引用時間窗口，則無法使用邊緣分割來評估該查詢。 |
| 否定 | 如果查詢包含否定或`not`事件，則無法使用邊緣分段來評估。 |
| 多個事件 | 如果查詢包含多個事件，則無法使用邊緣分段來評估。 |

{style=&quot;table-layout:auto&quot;}

## 擷取所有啟用邊緣區段的區段

您可以向`/segment/definitions`端點提出GET請求，以擷取IMS組織內啟用邊緣分段的所有區段清單。

**API格式**

若要擷取啟用邊緣分段的區段，您必須在請求路徑中加入查詢參數`evaluationInfo.synchronous.enabled=true`。

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回IMS組織中已啟用邊緣分段的區段陣列。 有關返回的段定義的詳細資訊，請參閱[段定義端點指南](./segment-definitions.md)。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
            "imsOrgId": "{IMS_ORG_ID}",
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

## 建立已啟用邊緣區段的區段

您可以建立區段，並透過向`/segment/definitions`端點提出POST要求來啟用邊緣區段。 除了匹配上述](#query-types)所列的[邊緣分段查詢類型之外，您還必須將裝載中的`evaluationInfo.synchronous.enabled`標幟設為true。

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>以下範例是建立區段的標準請求。 如需建立區段定義的詳細資訊，請閱讀有關建立區段[的教學課程。](../tutorials/create-a-segment.md)

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | `evaluationInfo`物件會決定區段定義將要進行的評估類型。 若要使用邊緣分段，請設定`evaluationInfo.synchronous.enabled`值`true`。 |

**回應**

成功的回應會傳回新建立的區段定義的詳細資料，此定義可用於邊緣分段。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
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
```

## 後續步驟

現在您知道如何建立啟用邊緣區段的區段，您可以使用這些區段來啟用相同頁面和下一頁的個人化使用案例。

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪[區段產生器使用指南](../ui/segment-builder.md)。
