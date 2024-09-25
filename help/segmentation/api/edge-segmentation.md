---
solution: Experience Platform
title: 使用API的Edge區段
description: 本檔案包含如何搭配Adobe Experience Platform Segmentation Service API使用邊緣區段的範例。
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# 邊緣分段

>[!NOTE]
>
>以下檔案說明如何使用API執行邊緣細分。 如需使用UI執行邊緣區段的資訊，請參閱[邊緣區段UI指南](../ui/edge-segmentation.md)。
>
>Edge區段現在可供所有Platform使用者普遍使用。 如果您在Beta版期間建立邊緣區段定義，這些區段定義仍可繼續運作。

Edge區段能讓您在Adobe Experience Platform的邊緣即時評估區段定義，啟用相同頁面和下一頁個人化使用案例。

>[!IMPORTANT]
>
> 邊緣資料將會儲存在距離收集地點最近的邊緣伺服器位置，而且可能會儲存在指定為Adobe Experience Platform資料中心中心（或主體）以外的位置。
>
> 此外，邊緣區段引擎將只處理邊緣上有&#x200B;**one**&#x200B;主要標籤身分的請求，這與非邊緣型主要身分一致。

## 快速入門

此開發人員指南需要深入瞭解與邊緣細分相關的各種[!DNL Adobe Experience Platform]服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從[!DNL Real-Time Customer Profile]資料建立對象。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。

為了成功呼叫任何Experience Platform API端點，請閱讀[Platform API快速入門](../../landing/api-guide.md)的指南，瞭解必要的標頭以及如何讀取範例API呼叫。

## Edge區段查詢型別 {#query-types}

為了使用邊緣區段來評估區段，查詢必須符合以下准則：

| 查詢型別 | 詳細資料 |
| ---------- | ------- |
| 少於24小時時間範圍內的單一事件 | 任何會參照少於24小時之時間範圍內的單一傳入事件的區段定義。 |
| 僅限設定檔 | 僅參考設定檔屬性的任何區段定義。 |
| 在少於24小時的相對時間範圍內，具有設定檔屬性的單一事件 | 任何區段定義，會參照具有一或多個設定檔屬性的單一傳入事件，且會在少於24小時的相對時間範圍內發生。 |
| 區段區段 | 包含一或多個批次或串流區段的任何區段定義。 **注意：**&#x200B;如果使用區段區段，則設定檔取消資格將&#x200B;**每24小時發生一次**。 |
| 具有設定檔屬性的多個事件 | 任何在過去24小時&#x200B;**內參考多個事件**&#x200B;且（選擇性）具有一或多個設定檔屬性的區段定義。 |

此外，區段&#x200B;**必須**&#x200B;繫結至邊緣上作用中的合併原則。 如需有關合併原則的詳細資訊，請參閱[合併原則指南](../../profile/api/merge-policies.md)。

在下列情況下，區段定義將&#x200B;**不會**&#x200B;啟用邊緣分段：

- 區段定義包含單一事件和`inSegment`事件的組合。
   - 但是，如果`inSegment`事件中包含的區段僅為設定檔，則區段定義&#x200B;**將**&#x200B;啟用邊緣分段。
- 區段定義會使用「忽略年份」作為其時間限制的一部分。

## 擷取所有已啟用邊緣細分的區段

您可以向`/segment/definitions`端點發出GET要求，擷取貴組織內所有啟用邊緣劃分的區段清單。

**API格式**

若要擷取為邊緣細分啟用的區段，您必須在請求路徑中包含查詢引數`evaluationInfo.synchronous.enabled=true`。

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

成功的回應會傳回組織中已啟用邊緣區段的一系列區段。 在[區段定義端點指南](./segment-definitions.md)中找到有關傳回的區段定義的詳細資訊。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

您可以對符合上述[邊緣劃分查詢型別](#query-types)之一的`/segment/definitions`端點發出POST要求，以建立已啟用邊緣劃分的區段。

**API格式**

```http
POST /segment/definitions
```

**要求**

>[!NOTE]
>
>以下範例是建立區段的標準請求。 如需建立區段定義的詳細資訊，請閱讀[建立區段](../tutorials/create-a-segment.md)的教學課程。

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

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似的動作並處理區段，請造訪[區段產生器使用手冊](../ui/segment-builder.md)。

## 附錄

下節列出與邊緣細分相關的常見問題：

### 區段需要多久才能在Edge Network上使用？

區段在Edge Network上可供使用最多需要一小時。
