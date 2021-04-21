---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；預覽；預覽和估計；估計和預覽；api;API;
solution: Experience Platform
title: 預覽和估計API端點
topic-legacy: developer guide
description: 在開發區段定義時，您可以使用Adobe Experience Platform的預估和預覽工具來檢視摘要層級資訊，以協助您隔離預期的觀眾。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---

# 預覽和估計端點

當您開發區段定義時，可以使用Adobe Experience Platform的預估和預覽工具來檢視摘要層級資訊，以協助您隔離預期的觀眾。

* **預** 覽提供區段定義之合格描述檔的分頁清單，讓您比較結果與預期。

* **「估** 計」會提供區段定義的統計資訊，例如預測對象大小、信賴區間和錯誤標準差。

>[!NOTE]
>
>若要存取與即時客戶描述檔資料相關的類似度量，例如特定名稱空間或描述檔資料存放區中的描述檔片段和合併描述檔總數，請參閱描述檔API開發人員指南中的[描述檔預覽（預覽範例狀態）端點指南](../../profile/api/preview-sample-status.md)。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請參閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 如何產生估計

當將記錄擷取至描述檔儲存區時，會觸發取樣工作以更新該計數，將總描述檔計數增加或減少超過5%。 觸發資料取樣的方式取決於擷取方法：

* **批次擷取：** 對於批次擷取，在成功將批次擷取至描述檔存放區的15分鐘內，如果達到5%增加或減少臨界值，則會執行工作以更新計數。
* **串流擷取：** 對於串流資料工作流程，會每小時檢查一次，以判斷是否達到5%的增加或減少臨界值。如果已觸發，則會自動觸發作業以更新計數。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

>[!NOTE]
>
>估計通常需要10到15秒才能執行，從粗略的估計開始，並隨著讀取更多記錄而調整。

## 建立新的預覽{#create-preview}

您可以向`/preview`端點發出POST請求，以建立新預覽。

>[!NOTE]
>
>在建立預覽作業時自動建立估計作業。 這兩個工作將共用相同的ID。

**API格式**

```http
POST /preview
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `predicateExpression` | 用於查詢資料的PQL表達式。 |
| `predicateType` | `predicateExpression`下查詢表達式的謂詞類型。 目前，此屬性唯一接受的值是`pql/text`。 |
| `predicateModel` | 配置檔案資料所基於的[!DNL Experience Data Model](XDM)模式類的名稱。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立），並包含您新建立之預覽的詳細資訊。

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `state` | 預覽作業的目前狀態。 最初建立時，它將處於「新」狀態。 隨後，它將處於「運行」狀態，直到處理完成，此時它將變為「RESULT_READY」或「FAILED」。 |
| `previewId` | 預覽工作的ID，在檢視估計值或預覽時用於查閱目的，如下一節所述。 |

## 擷取特定預覽的結果{#get-preview}

您可以向`/preview`端點提出GET請求，並在請求路徑中提供預覽ID，以擷取特定預覽的詳細資訊。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 您要擷取之預覽的`previewId`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定預覽的詳細資訊。

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `results` | 實體ID的清單，以及其相關身分。 提供的連結可用於使用[配置檔案訪問API端點](../../profile/api/entities.md)查找指定實體。 |

## 檢索特定估計作業的結果{#get-estimate}

在建立預覽工作後，您可以在至`/estimate`端點的GET請求路徑中使用其`previewId`，以檢視區段定義的統計資訊，包括預計讀者大小、信賴區間和錯誤標準差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在建立預覽工作且兩個工作共用相同的ID值以供查閱時，才會觸發估計工作。 具體而言，這是建立預覽工作時傳回的`previewId`值。 |

**要求**

下列請求會擷取特定估計工作的結果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含估計工作的詳細資訊。

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | 顯示區段內依身分名稱空間劃分之描述檔數目的物件陣列。 依名稱空間劃分的描述檔總數（將每個名稱空間顯示的值加在一起）可能高於描述檔計數量度，因為一個描述檔可能與多個名稱空間相關聯。 例如，如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶關聯。 |
| `state` | 預覽作業的目前狀態。 狀態將為「RUNNING」，直到處理完成，此時狀態將變為「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當`state`為&quot;RESULT_READY&quot;時，此欄位會提供URL以檢視估計值。 |

## 後續步驟

閱讀本指南後，您應更瞭解如何使用區段API來處理預覽和估計。 要瞭解如何存取與即時客戶個人檔案資料相關的度量，例如特定名稱空間或個人檔案資料存放區中的個人檔案片段和合併個人檔案總數，請造訪[個人檔案預覽(`/previewsamplestatus`)端點指南](../../profile/api/preview-sample-status.md)。
