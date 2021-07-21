---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；邊緣分段；邊緣分段；串流邊緣；
solution: Experience Platform
title: '使用API進行邊緣劃分 '
topic-legacy: developer guide
description: 本檔案包含如何搭配Adobe Experience Platform區段服務API使用邊緣區段的範例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 3de00fb9ae5348b129a499cfd81d8db6dbac2d46
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---

# 邊緣區段（測試版）

>[!NOTE]
>
>下列檔案說明如何使用API執行邊緣分段。 如需使用UI執行邊緣分段的資訊，請參閱[邊緣分段UI指南](../ui/edge-segmentation.md)。 此外，邊緣區段目前仍在測試中。 文件和功能可能會有所變更。

邊緣分段是即時評估Adobe Experience Platform中邊緣區段的功能，可啟用相同的頁面和下一頁個人化使用案例。

## 快速入門

本開發人員指南需要妥善了解與邊緣細分相關的各種[!DNL Adobe Experience Platform]服務。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。
- [[!DNL Segmentation]](../home.md):提供從資料建立區段和對象的 [!DNL Real-time Customer Profile] 功能。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

若要成功呼叫[!DNL Data Prep] API端點，請參閱[平台API快速入門手冊](../../landing/api-guide.md)，以了解所需標題及如何讀取範例API呼叫。

## 邊緣分段查詢類型 {#query-types}

為了使用邊緣分段來評估區段，查詢必須符合下列准則：

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 |
| 參照設定檔的傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件，以及一或多個設定檔屬性。 |
| 頻率查詢 | 任何區段定義，是指至少發生特定次數之事件。 |
| 參考設定檔的頻率查詢 | 任何區段定義，是指發生至少特定次數的事件，且具有一或多個設定檔屬性。 |

{style=&quot;table-layout:auto&quot;}

下列查詢類型是邊緣分段目前支援的&#x200B;**not**:

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 相對時間窗口 | 如果查詢引用時間視窗，則無法使用邊緣分段來評估。 |
| 否定 | 如果查詢包含否定或`not`事件，則無法使用邊緣分段來評估。 |
| 多個事件 | 如果查詢包含多個事件，則無法使用邊緣分段來評估。 |

{style=&quot;table-layout:auto&quot;}

## 擷取為邊緣細分啟用的所有區段

您可以向`/segment/definitions`端點提出GET請求，以擷取IMS組織內已啟用邊緣分段的所有區段清單。

**API格式**

若要擷取已啟用邊緣分段功能的區段，您必須在請求路徑中加入查詢參數`evaluationInfo.synchronous.enabled=true`。

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

成功的回應會傳回IMS組織中已啟用邊緣分段的區段陣列。 有關返回的段定義的詳細資訊，請參見[段定義終結點指南](./segment-definitions.md)。

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

## 建立已啟用邊緣分段的區段

您可以向`/segment/definitions`端點提出符合上方所列[邊緣分段查詢類型之一的POST請求，以建立已啟用邊緣分段的區段。](#query-types)

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>以下範例是建立區段的標準請求。 如需建立區段定義的詳細資訊，請參閱關於[建立區段](../tutorials/create-a-segment.md)的教學課程。

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

現在您知道如何建立啟用邊緣分段的區段，可以使用它們來啟用相同頁面和下一頁個人化的使用案例。

若要了解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪[區段產生器使用指南](../ui/segment-builder.md)。
