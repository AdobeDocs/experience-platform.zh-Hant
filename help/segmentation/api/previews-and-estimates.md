---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；預覽；預測；預覽和估計；估計和預測；api;API;
solution: Experience Platform
title: 預覽和估計API端點
description: 在開發段定義時，您可以使用Adobe Experience Platform內的估計和預覽工具來查看摘要級別資訊，以幫助確保隔離預期的受眾。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 預覽和估計端點

在開發段定義時，您可以使用Adobe Experience Platform內的估計和預覽工具來查看摘要級資訊，以幫助確保隔離預期的受眾。

* **預覽** 為段定義提供分頁的合格配置檔案清單，允許您將結果與預期結果進行比較。

* **估計** 提供有關段定義的統計資訊，如預計受眾大小、置信區間和誤差標準偏差。

>[!NOTE]
>
>要訪問與即時客戶配置檔案資料相關的類似度量，例如特定命名空間或整個配置檔案資料儲存中配置檔案片段和合併配置檔案的總數，請參閱 [配置檔案預覽（預覽示例狀態）終結點指南](../../profile/api/preview-sample-status.md), Profile API開發人員指南的一部分。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 如何生成估計

當將記錄引入Profile儲存中時，將總配置檔案計數增加或減少5%以上，將觸發採樣作業以更新該計數。 資料採樣的觸發方式取決於攝入方法：

* **批量攝取：** 對於批處理接收，在成功將批處理插入配置檔案儲存15分鐘內，如果滿足5%增加或減少閾值，則運行作業以更新計數。
* **流攝入：** 對於流式資料工作流，每小時檢查以確定是否滿足5%的增減閾值。 如果已觸發，則自動觸發作業以更新計數。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表顯示了這些示例大小：

| 配置檔案儲存中的實體 | 示例大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 2000多萬 | 5% |

>[!NOTE]
>
>估計通常需要10到15秒才能運行，從粗略估計開始，隨著讀取更多記錄而細化。

## 建立新預覽 {#create-preview}

可通過向POST請求建立新預覽 `/preview` 端點。

>[!NOTE]
>
>在建立預覽作業時自動建立評估作業。 這兩個作業將共用同一ID。

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
| `predicateType` | 下查詢表達式的謂詞類型 `predicateExpression`。 當前，此屬性唯一接受的值是 `pql/text`。 |
| `predicateModel` | 名稱 [!DNL Experience Data Model] (XDM)配置檔案資料所基於的架構類。 |
| `graphType` | 要從中獲取群集的圖形類型。 支援的值為 `none` （不執行身份拼接）和 `pdg` （根據您的私有身份圖執行身份拼接）。 |

**回應**

成功的響應將返回HTTP狀態201（已建立），並返回新建立的預覽的詳細資訊。

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
| `state` | 預覽作業的當前狀態。 最初建立時，它將處於「NEW」狀態。 隨後，它將處於「RUNNING」狀態，直到處理完成，此時它將變為「RESULT_READY」或「FAILED」。 |
| `previewId` | 預覽作業的ID，在查看估計或預覽時用於查找目的，如下一節中所述。 |

## 檢索特定預覽的結果 {#get-preview}

可通過向GET請求來檢索有關特定預覽的詳細資訊 `/preview` 在請求路徑中提供預覽ID。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 的 `previewId` 要檢索的預覽的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定預覽的詳細資訊。

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
| `results` | 實體ID及其相關標識的清單。 提供的連結可用於使用 [配置檔案訪問API終結點](../../profile/api/entities.md)。 |

## 檢索特定評估作業的結果 {#get-estimate}

建立預覽作業後，可以使用 `previewId` 在GET請求到 `/estimate` 終結點以查看有關段定義的統計資訊，包括投影受眾大小、置信區間和誤差標準偏差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在建立預覽作業時才觸發評估作業，並且兩個作業共用相同的ID值以供查找。 具體來說，這是 `previewId` 建立預覽作業時返回的值。 |

**要求**

以下請求檢索特定估計作業的結果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應返回HTTP狀態200，並返回估計作業的詳細資訊。

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
| `estimatedNamespaceDistribution` | 顯示按標識命名空間細分的段內配置檔案數的對象陣列。 按命名空間（將每個命名空間顯示的值加在一起）的配置檔案總數可能高於配置檔案計數度量，因為一個配置檔案可能與多個命名空間相關聯。 例如，如果客戶在多個渠道上與您的品牌進行交互，則多個命名空間將與該客戶關聯。 |
| `state` | 預覽作業的當前狀態。 在處理完成之前，狀態將為「RUNNING」，此時它將變為「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當 `state` 為&quot;RESULT_READY&quot;，此欄位提供URL來查看估計。 |

## 後續步驟

閱讀本指南後，您應更瞭解如何使用「分段API」來處理預覽和估計。 要瞭解如何訪問與即時客戶配置檔案資料相關的度量，例如特定命名空間或整個配置檔案資料儲存中配置檔案片段和合併配置檔案的總數，請訪問 [配置檔案預覽(P)`/previewsamplestatus`)終結點指南](../../profile/api/preview-sample-status.md)。
