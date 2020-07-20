---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 預覽和估計端點
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 2%

---


# 預覽和估計端點

當您開發區段定義時，可以使用中的估計和預覽工具來檢 [!DNL Adobe Experience Platform] 視摘要層級的資訊，以協助您隔離預期的觀眾。 **預覽** 提供區段定義之合格描述檔的分頁清單，讓您比較結果與預期。 **估計** 提供區段定義的統計資訊，例如預測受眾大小、信賴區間和錯誤標準差。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請先檢閱 [快速入門手冊](./getting-started.md) ，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 如何產生估計

資料採樣觸發方式取決於提取方法。

對於批次擷取，描述檔存放區會每十五分鐘自動掃描一次，以查看自上次執行取樣工作以來是否成功擷取新批次。 如果是這樣，則隨後掃描配置檔案儲存，以查看記錄數是否至少有5%的變化。 如果滿足這些條件，則觸發新的採樣作業。

對於串流擷取，會每小時自動掃描描述檔存放區，以查看記錄數是否至少有5%的變更。 如果符合此條件，則會觸發新的取樣工作。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

>[!NOTE] 估計通常需要10到15秒才能執行，從粗略的估計開始，並隨著讀取更多記錄而調整。

## Create a new preview {#create-preview}

您可以向端點發出POST請求，以建立新的預 `/preview` 覽。

>[!NOTE] 在建立預覽作業時自動建立估計作業。 這兩個工作將共用相同的ID。

**API格式**

```http
POST /preview
```

**請求**

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
| `predicateType` | 下查詢表達式的謂詞類型 `predicateExpression`。 目前，此屬性唯一接受的值是 `pql/text`。 |
| `predicateModel` | 描述檔資料所依據之體驗資料模型(XDM)架構的名稱。 |

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

## 擷取特定預覽的結果 {#get-preview}

您可以向端點提出GET請求並在請求路徑中提供預覽ID，以 `/preview` 擷取特定預覽的詳細資訊。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 您 `previewId` 要擷取的預覽值。 |

**請求**

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
        },
        "state": "RESULT_READY",
        "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
        }
    }],
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `results` | 實體ID的清單，以及其相關身分。 提供的連結可用來使用描述檔存取API來查 [找指定實體](../../profile/api/entities.md)。 |

## 檢索特定估計作業的結果 {#get-estimate}

建立預覽工作後，您就可在GET要求到端點的路徑中使用該工作，以檢視區段定義的相關統計資訊，包括預計的觀眾大小、信賴區間和錯誤標準差。 `previewId``/estimate`

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在建立預覽工作且兩個工作共用相同的ID值以進行查閱時，才會觸發估計工作。 具體而言，這是建 `previewId` 立預覽工作時傳回的值。 |

**請求**

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
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `state` | 預覽作業的目前狀態。 在處理完成之前，將為「RUNNING」，此時它將變為「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當預覽作業的當前狀態為&quot;RESULT_READY&quot;時，此屬性提供URL以檢視估計值。 |

## 後續步驟

閱讀本指南後，您現在更能瞭解如何使用預覽和估計。 若要進一步瞭解其他分段服務API端點，請閱讀分段服務開 [發人員指南總覽](./overview.md)。