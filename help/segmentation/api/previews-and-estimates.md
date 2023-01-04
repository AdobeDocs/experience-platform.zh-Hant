---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；預覽；估計；預覽和估計；估計和預覽；API;API;
solution: Experience Platform
title: 預覽和估計API端點
topic-legacy: developer guide
description: 在開發區段定義時，您可以使用Adobe Experience Platform中的預估和預覽工具來檢視摘要層級資訊，以協助您確保隔離預期的對象。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 預覽和估計端點

當您開發區段定義時，可以使用Adobe Experience Platform中的預估和預覽工具來檢視摘要層級資訊，以協助您確保隔離預期的對象。

* **預覽** 為區段定義提供合格設定檔的編頁清單，讓您能比較結果與預期。

* **估計** 提供區段定義的統計資訊，例如投影對象大小、信賴區間和錯誤標準差。

>[!NOTE]
>
>若要存取與即時客戶設定檔資料相關的類似量度，例如特定命名空間或設定檔資料存放區內的設定檔片段和合併設定檔總數，請參閱 [設定檔預覽（預覽範例狀態）端點指南](../../profile/api/preview-sample-status.md)，此為設定檔API開發人員指南的一部分。

## 快速入門

本指南中使用的端點屬於 [!DNL Adobe Experience Platform Segmentation Service] API。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 如何產生估計

當將記錄擷取至設定檔存放區時，總設定檔計數會增加或減少超過5%，就會觸發取樣工作以更新計數。 資料取樣的觸發方式取決於擷取方法：

* **批次內嵌：** 對於批次內嵌，在成功將批次內嵌至設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新計數。
* **串流內嵌：** 對於串流資料工作流程，會每小時進行檢查，以判斷是否符合5%的增加或減少臨界值。 如果已觸發，則會自動觸發工作以更新計數。

掃描的樣本大小取決於設定檔存放區中的整體數量。 下表顯示以下樣本大小：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000至2000萬 | 100萬 |
| 2000多萬 | 總共5% |

>[!NOTE]
>
>估計通常需要10到15秒才能運行，從粗略估計開始，隨著記錄的讀取增加而細化。

## 建立新預覽 {#create-preview}

您可以向 `/preview` 端點。

>[!NOTE]
>
>建立預覽作業時，系統會自動建立預估作業。 這兩個工作會共用相同的ID。

**API格式**

```http
POST /preview
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `predicateExpression` | 用於查詢資料的PQL表達式。 |
| `predicateType` | 下查詢表達式的謂詞類型 `predicateExpression`. 目前，此屬性唯一接受的值是 `pql/text`. |
| `predicateModel` | 的名稱 [!DNL Experience Data Model] (XDM)設定檔資料所根據的架構類別。 |
| `graphType` | 要從中獲取群集的圖形類型。 支援的值為 `none` （不執行身分匯整）和 `pdg` （根據您的私人身分圖表執行身分拼接）。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立），並包含新建立預覽的詳細資訊。

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
| `state` | 預覽作業的目前狀態。 最初建立時，會處於「NEW」狀態。 隨後，它將處於「正在運行」狀態，直到處理完成，此時它將變為「RESULT_READY」或「FAILED」。 |
| `previewId` | 預覽工作的ID，用於檢視預估或預覽時的查閱用途，如下一節所述。 |

## 擷取特定預覽的結果 {#get-preview}

您可以向提出GET要求，以擷取特定預覽的詳細資訊 `/preview` 端點，並在請求路徑中提供預覽ID。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 此 `previewId` 您要擷取的預覽值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定預覽的詳細資訊。

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
| `results` | 實體ID的清單，及其相關身分識別。 提供的連結可用來查詢指定的實體，使用 [設定檔存取API端點](../../profile/api/entities.md). |

## 檢索特定估計作業的結果 {#get-estimate}

建立預覽作業後，即可使用其 `previewId` 在GET請求的路徑中 `/estimate` 端點來檢視區段定義的統計資訊，包括投影對象大小、信賴區間和錯誤標準差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在建立預覽作業，且兩個作業共用相同的ID值以進行查詢時，才會觸發預估作業。 具體來說，這是 `previewId` 值會在建立預覽作業時傳回。 |

**要求**

下列請求會擷取特定預估工作的結果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含預估工作的詳細資訊。

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
| `estimatedNamespaceDistribution` | 一個物件陣列，顯示依身分命名空間劃分之區段內的設定檔數量。 依命名空間的設定檔總數（將每個命名空間顯示的值加總）可能比設定檔計數量度高，因為一個設定檔可能與多個命名空間相關聯。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。 |
| `state` | 預覽作業的目前狀態。 狀態將為「RUNNING」，直到處理完成，此時狀態將變為「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當 `state` 為&quot;RESULT_READY&quot;，此欄位提供URL以檢視預估值。 |

## 後續步驟

閱讀本指南後，您應該能更清楚了解如何使用「細分API」來處理預覽和預估。 若要了解如何存取與您的即時客戶設定檔資料相關的量度，例如特定命名空間內的設定檔片段和合併的設定檔總數，或整個設定檔資料存放區，請造訪 [設定檔預覽(`/previewsamplestatus`)端點指南](../../profile/api/preview-sample-status.md).
