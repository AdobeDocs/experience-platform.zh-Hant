---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立區段
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# 建立區段

本檔案提供教學課程，說明如何使用區段API來開發、測試、預覽和儲存區 [段定義](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

如需如何使用使用者介面建立區段的詳細資訊，請參閱「區段產 [生器指南」](../ui/overview.md)。

## 快速入門

本教學課程需要有效瞭解建立受眾細分所涉及的各種Adobe Experience Platform服務。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [即時客戶個人檔案](../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [Adobe Experience Platform細分服務](../home.md): 可讓您從即時客戶個人檔案資料建立受眾細分。
- [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。

以下章節提供您必須知道的其他資訊，才能成功呼叫平台API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型： application/json

## 開發區段定義

分段的第一步是定義分段，在稱為分段定義的構造中 **表示**。 段定義是一個對象，它封裝了用配置檔案查詢語言(PQL)編寫的查詢。 此對象也稱為 **PQL謂詞**。 PQL謂語根據與您提供給「即時客戶配置檔案」的任何記錄或時間系列資料相關的條件定義段規則。 有關編寫 [PQL查詢的詳細資訊](../pql/overview.md) ，請參見PQL指南。

您可以透過對即時客戶描述檔API中的端點提出POST `/segment/definitions` 要求來建立新的區段定義。 下列範例概述如何設定定義請求的格式，包括成功定義區段所需的資訊。

區段定義可用兩種方式來評估——批次分段和串流分段。 批次分段會根據預設排程或手動觸發評估時評估區段，而串流分段則會在資料擷取到平台時立即評估區段。 本教學課程將使用批 **次分段**。 如需串流區段的詳細資訊，請閱讀串 [流區段的概觀](../api/streaming-segmentation.md)。

**API格式**

```http
POST /segment/definitions
```

**請求**

下列請求會為稱為&quot;MyProfile&quot;的結構建立新的區段定義。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| 屬性 | 說明 |
| --------- | ------------ | 
| `name` | **必填。** 參考區段的唯一名稱。 |
| `schema` | **必填。** 與區段中的實體關聯的架構。 由或字 `id` 段 `name` 組成。 |
| `expression` | **必填。** 包含區段定義之欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`: 根據發佈的PQL語法對段定義的文本表示。  例如, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | 符合中指定類型的表達式 `expression.format`。 |
| `mergePolicyId` | 用於導出資料的合併策略的標識符。 有關詳細資訊，請閱讀合 [並策略配置文檔](../../profile/api/merge-policies.md)。 |
| `description` | 定義的人類可讀描述。 |

**回應**

成功的回應會傳回新建立之區段定義的詳細資料，包括其系統產生的唯讀定義，此定 `id` 義將在本教學課程稍後使用。

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## 預估和預覽觀眾 {#estimate-and-preview-an-audience}

當您開發區段定義時，可以使用即時客戶個人檔案中的估計和預覽工具來檢視摘要層級資訊，以協助您隔離預期的受眾。 估計值提供區段定義的統計資訊，例如預計讀者大小和信賴區間。 預覽提供區段定義的合格設定檔分頁清單，讓您比較結果與預期結果。

透過估計和預覽受眾，您可以測試和最佳化PQL謂語，直到產生可預期的結果，然後在更新的區段定義中使用。

預覽或取得區段估計需要兩個步驟：

1. [建立預覽工作](#create-a-preview-job)
2. [使用預覽工作的ID](#view-an-estimate-or-preview) ，檢視估計值或預覽

### 如何產生估計

資料樣本可用來評估區段並估計符合資格的設定檔數目。 每天早上（12AM-2AM PT，即7-9AM UTC），新資料會載入記憶體中，所有區段查詢都會使用當天的樣本資料來估計。 因此，新增的欄位或收集的其他資料，都會反映在次日的估計值中。

範例大小取決於您描述檔商店中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

估計值一般會持續10-15秒，從粗略的估計開始，並隨著讀取更多記錄而調整。

### 建立預覽工作

您可以向端點發出POST請求，以建立新的預覽 `/preview` 作業。

**API格式**

```http
POST /preview
```

**請求**

下列請求會建立新的預覽工作。 請求主體包含與區段相關的查詢資訊。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `predicateExpression` | 用於查詢資料的PQL表達式。 |
| `predicateModel` | 配置檔案資料所基於的XDM架構的名稱。 |

**回應**

成功的回應會傳回新建立之預覽工作的詳細資料，包括其ID和目前的處理狀態。

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `state` | 預覽作業的目前狀態。 在處理完成之前，它將處於「運行」狀態，此時它將變為「RESULT_READY」或「FAILED」。 |
| `previewId` | 預覽工作的ID，在檢視估計值或預覽時用於查閱目的，如下一節所述。 |

### 檢視估計或預覽

由於不同的查詢可能需要不同的時間才能完成，因此會以非同步方式執行估計和預覽程式。 一旦查詢啟動後，您就可以使用API呼叫來擷取(GET)估計或預覽的目前狀態。

使用「即時客戶描述檔API」，您可以透過其ID來查閱預覽工作的目前狀態。 如果狀態為&quot;RESULT_READY&quot;，則可以查看結果。 視您要檢視預估或預覽而定，每個API中都有自己的端點。 以下提供兩者的範例。

### 檢視估計值

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 您要檢視之預覽工作的ID。 |

**請求**

下列請求會使用上一步驟中建立 `previewId` 的估計來擷取估計。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回估計的詳細資訊。

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `state` | 預覽作業的目前狀態。 在處理完成之前，將為「RUNNING」，此時它將變為「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當預覽作業的當前狀態為&quot;RESULT_READY&quot;時，此屬性提供URL以檢視估計值。 |

### 檢視預覽

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 您要檢視之預覽工作的ID。 |

**請求**

下列請求會使用在上一步驟中建 `previewId` 立的預覽擷取。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回預覽的詳細資訊。

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
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## 後續步驟

在您開發、測試並儲存區段定義後，您就可以使用即時客戶設定檔API建立區段工作以建立觀眾。 請參閱評估和存 [取區段結果的教學課程](./evaluate-a-segment.md) ，以取得如何完成此作業的詳細步驟。