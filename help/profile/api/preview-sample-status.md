---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；預覽；示例
title: 預覽示例狀態（配置檔案預覽）API終結點
description: 即時客戶配置檔案API的預覽示例狀態終結點允許您預覽配置檔案資料的最新成功示例、按資料集和按標識列出配置檔案分發，並生成顯示資料集重疊、標識重疊和未縫合配置檔案的報告。
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 1%

---

# 預覽示例狀態終結點（配置檔案預覽）

Adobe Experience Platform使您能夠從多個源中接收客戶資料，以便為您的每個客戶構建一個強健、統一的配置檔案。 當資料被引入平台時，將運行示例作業以更新配置檔案計數和其他與即時客戶配置檔案資料相關的度量。

此示例作業的結果可使用 `/previewsamplestatus` 終結點，即時客戶配置檔案API的一部分。 此終結點還可用於按資料集和標識命名空間列出配置檔案分發，以及生成多個報告，以便能夠查看組織配置檔案儲存的組成。 本指南介紹使用 `/previewsamplestatus` API終結點。

>[!NOTE]
>
>作為Adobe Experience Platform分段服務API的一部分，有可用的估計和預覽端點，允許您查看有關段定義的摘要級資訊，以幫助確保隔離預期的受眾。 要查找使用段預覽和估計端點的詳細步驟，請訪問 [預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)的 [!DNL Segmentation] API開發人員指南。

## 快速入門

本指南中使用的API終結點是 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 配置檔案片段與合併的配置檔案

本指南同時引用「配置檔案片段」和「合併的配置檔案」。 在繼續之前，必須瞭解這些術語之間的區別。

每個單獨的客戶配置檔案由多個配置檔案片段組成，這些片段已合併以形成該客戶的單個視圖。 例如，如果客戶通過多個渠道與您的品牌進行交互，則您的組織可能會在多個資料集中顯示與該單個客戶相關的多個配置檔案片段。

將配置檔案片段放入平台時，它們會合併在一起（基於合併策略），以便為該客戶建立單個配置檔案。 因此，輪廓片段的總數可能總是高於合併的輪廓的總數，因為每個輪廓由多個片段組成。

要瞭解有關配置檔案及其在Experience Platform中的角色的更多資訊，請首先閱讀 [即時客戶概要資訊概述](../home.md)。

## 示例作業的觸發方式

當為即時客戶配置檔案啟用的資料被接收到 [!DNL Platform]，它儲存在Profile資料儲存中。 當將記錄導入配置檔案儲存中時，將配置檔案總數增加或減少5%以上，將觸發一個採樣作業以更新該計數。 觸發樣本的方式取決於所使用的攝取類型：

* 對於 **流式資料工作流**，每小時檢查以確定是否滿足5%增加或減少閾值。 如果已觸發，則自動觸發示例作業以更新計數。
* 對於 **批處理**，如果滿足5%的增加或減少閾值，則運行作業以更新計數。 使用配置檔案API，您可以預覽最新成功的示例作業，以及按資料集和標識命名空間列出配置檔案分發。

按命名空間度量列出的配置檔案計數和配置檔案也可在 [!UICONTROL 配置檔案] 的子菜單。 有關如何使用UI訪問配置檔案資料的資訊，請訪問 [[!DNL Profile] UI指南](../ui/user-guide.md)。

## 查看最後一個示例狀態 {#view-last-sample-status}

您可以執行對 `/previewsamplestatus` 終結點，以查看為您的組織運行的上次成功示例作業的詳細資訊。 這包括示例中的配置檔案總數，以及配置檔案計數度量，或您的組織在Experience Platform中擁有的配置檔案總數。

在將配置檔案片段合併以為每個單獨客戶形成單個配置檔案之後生成配置檔案計數。 換句話說，當配置檔案片段合併在一起時，它們返回「1」個配置檔案計數，因為它們都與同一個人相關。

配置檔案計數還包括具有屬性（記錄資料）的配置檔案以及僅包含時間序列（事件）資料的配置檔案，如Adobe Analytics配置檔案。 在接收配置檔案資料時定期刷新示例作業，以便提供平台內最新的配置檔案總數。

**API格式**

```http
GET /previewsamplestatus
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

響應包括為組織運行的上次成功示例作業的詳細資訊。

>[!NOTE]
>
>在本示例響應中， `numRowsToRead` 和 `totalRows` 是相等的。 根據您的組織在Experience Platform中擁有的配置檔案數，情況可能是這樣。 但是，這兩個數字一般是不同的， `numRowsToRead` 是較小的數，因為它將示例表示為配置檔案總數的子集(`totalRows`)。

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| 屬性 | 說明 |
|---|---|
| `numRowsToRead` | 示例中合併的配置檔案總數。 |
| `sampleJobRunning` | 返回的布爾值 `true` 示例作業正在進行時。 為從上載批處理檔案到實際添加到配置檔案儲存時發生的延遲提供透明度。 |
| `cosmosDocCount` | Cosmos中的文檔總數。 |
| `totalFragmentCount` | 配置檔案儲存中的配置檔案片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批處理接收時間戳。 |
| `streamingDriven` | *此欄位已棄用，對響應沒有任何意義。* |
| `totalRows` | Experience Platform中合併的配置檔案總數，也稱為「配置檔案計數」。 |
| `lastBatchId` | 上次批處理接收ID。 |
| `status` | 上一個示例的狀態。 |
| `samplingRatio` | 採樣的合併輪廓的比率(`numRowsToRead`)到合併配置檔案總數(`totalRows`)，以十進位格式的百分比表示。 |
| `mergeStrategy` | 示例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的示例時間戳。 |

## 按資料集列出配置檔案分發

要按資料集查看配置檔案的分佈，可以向 `/previewsamplestatus/report/dataset` 端點。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在該日期運行了多個報表，則返回該日期的最新報表。 如果指定日期不存在報告，則返回404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

以下請求使用 `date` 參數，以返回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

響應包括 `data` 陣列，包含資料集對象清單。 顯示的響應已被截斷，以顯示三個資料集。

>[!NOTE]
>
>如果該日期存在多個報表，則只返回最新的報表。 如果提供的日期不存在資料集報告，則返回HTTP狀態404（未找到）。

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 屬性 | 說明 |
|---|---|
| `sampleCount` | 具有此資料集ID的採樣合併配置檔案的總數。 |
| `samplePercentage` | 的 `sampleCount` 合併配置檔案總數的百分比( `numRowsToRead` 返回的值 [上次抽樣狀態](#view-last-sample-status))，以十進位格式表示。 |
| `fullIDsCount` | 具有此資料集ID的合併配置檔案的總數。 |
| `fullIDsPercentage` | 的 `fullIDsCount` 合併配置檔案總數的百分比 `totalRows` 返回的值 [上次抽樣狀態](#view-last-sample-status))，以十進位格式表示。 |
| `name` | 資料集的名稱，如建立資料集時提供的。 |
| `description` | 資料集的說明，如在建立資料集期間提供的。 |
| `value` | 資料集的ID。 |
| `streamingIngestionEnabled` | 是否為流式接收啟用資料集。 |
| `createdUser` | 建立資料集的用戶的用戶ID。 |
| `reportTimestamp` | 報表的時間戳。 如果 `date` 參數在請求期間提供，返回的報告是提供的日期。 否 `date` 提供參數，並返回最近的報告。 |

## 按標識名稱空間列出配置檔案分發

您可以執行對 `/previewsamplestatus/report/namespace` 終結點：查看配置檔案儲存中所有合併的配置檔案中按標識命名空間劃分的細分。 這包括Adobe提供的標準標識以及您的組織定義的自定義標識。

標識名稱空間是Adobe Experience Platform身份服務的一個重要元件，用作客戶資料相關上下文的指示器。 要瞭解更多資訊，請從閱讀 [標識命名空間概述](../../identity-service/namespaces.md)。

>[!NOTE]
>
>按命名空間（將每個命名空間顯示的值加在一起）的配置檔案總數可能高於配置檔案計數度量，因為一個配置檔案可能與多個命名空間相關聯。 例如，如果客戶在多個渠道上與您的品牌進行交互，則多個命名空間將與該客戶關聯。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在該日期運行了多個報表，則返回該日期的最新報表。 如果指定日期不存在報告，則返回404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

以下請求未指定 `date` 參數，因此將返回最近的報告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

響應包括 `data` 陣列，其中單個對象包含每個命名空間的詳細資訊。 顯示的響應已截斷，以顯示四個命名空間。

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 屬性 | 說明 |
|---|---|
| `sampleCount` | 命名空間中採樣的合併配置檔案的總數。 |
| `samplePercentage` | 的 `sampleCount` 按採樣合併的配置檔案的百分比 `numRowsToRead` 返回的值 [上次抽樣狀態](#view-last-sample-status))，以十進位格式表示。 |
| `reportTimestamp` | 報表的時間戳。 如果 `date` 參數在請求期間提供，返回的報告是提供的日期。 否 `date` 提供參數，並返回最近的報告。 |
| `fullIDsFragmentCount` | 命名空間中配置檔案片段的總數。 |
| `fullIDsCount` | 命名空間中合併的配置檔案的總數。 |
| `fullIDsPercentage` | 的 `fullIDsCount` 合併配置檔案總數的百分比( `totalRows` 返回的值 [上次抽樣狀態](#view-last-sample-status))，以十進位格式表示。 |
| `code` | 的 `code` 的子菜單。 使用命名空間時，可以找到 [Adobe Experience Platform身份服務API](../../identity-service/api/list-namespaces.md) 也稱為 [!UICONTROL 身份符號] 的子菜單。 要瞭解更多資訊，請訪問 [標識命名空間概述](../../identity-service/namespaces.md)。 |
| `value` | 的 `id` 命名空間的值。 使用命名空間時，可以找到 [標識服務API](../../identity-service/api/list-namespaces.md)。 |

## 生成資料集重疊報告

資料集重疊報告通過公開對可定址受眾（合併的配置檔案）貢獻最大的資料集，提供了對組織配置檔案儲存組成的可見性。 除了提供對資料的洞察力外，此報告還可以幫助您採取措施來優化許可證使用，例如為某些資料集設定過期時間。

通過對執行GET請求，可以生成資料集重疊報告 `/previewsamplestatus/report/dataset/overlap` 端點。

有關如何使用命令行或PostmanUI生成資料集重疊報告的逐步說明，請參閱 [生成資料集重疊報告教程](../tutorials/dataset-overlap-report.md)。

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在同一日期運行了多個報告，則返回該日期的最近報告。 如果指定日期不存在報告，則返回404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

以下請求使用 `date` 參數，以返回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的請求返回HTTP狀態200(OK)和資料集重疊報告。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| 屬性 | 說明 |
|---|---|
| `data` | 的 `data` 對象包含以逗號分隔的資料集清單及其各自的配置檔案計數。 |
| `reportTimestamp` | 報表的時間戳。 如果 `date` 參數在請求期間提供，返回的報告是提供的日期。 否 `date` 提供參數，並返回最近的報告。 |

### 解釋資料集重疊報告

報告的結果可以從響應中的資料集和配置檔案計數中解釋。 請考慮以下示例報告 `data` 對象：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報表提供以下資訊：

* 有123個配置檔案，包括來自以下資料集的資料： `5d92921872831c163452edc8`。 `5da7292579975918a851db57`。 `5eb2cdc6fa3f9a18a7592a98`。
* 共有454,412個配置檔案包含來自這兩個資料集的資料： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`。
* 有107個配置檔案僅包含來自資料集的資料 `5eeda0032af7bb19162172a7`。
* 該組織共有454 642份檔案。

## 生成標識命名空間重疊報告 {#identity-overlap-report}

標識名稱空間重疊報告通過公開對可定址受眾（合併的配置式）貢獻最大的身份命名空間，提供了對組織配置檔案儲存組成的可見性。 這既包括Adobe提供的標準標識命名空間，也包括組織定義的自定義標識命名空間。

通過對執行GET請求，可以生成標識命名空間重疊報告 `/previewsamplestatus/report/namespace/overlap` 端點。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要返回的報告的日期。 如果在同一日期運行了多個報告，則返回該日期的最近報告。 如果指定日期不存在報告，則返回404（未找到）錯誤。 如果未指定日期，則返回最近的報告。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

以下請求使用 `date` 參數，以返回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的請求返回HTTP狀態200（確定）和標識命名空間重疊報告。

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| 屬性 | 說明 |
|---|---|
| `data` | 的 `data` 對象包含以逗號分隔的清單，這些清單具有標識命名空間代碼及其各自配置檔案計數的唯一組合。 |
| 命名空間代碼 | 的 `code` 是每個標識命名空間名稱的縮寫。 每個的映射 `code` 到 `name` 可使用 [Adobe Experience Platform身份服務API](../../identity-service/api/list-namespaces.md)。 的 `code` 也稱為 [!UICONTROL 身份符號] 的子菜單。 要瞭解更多資訊，請訪問 [標識命名空間概述](../../identity-service/namespaces.md)。 |
| `reportTimestamp` | 報表的時間戳。 如果 `date` 參數在請求期間提供，返回的報告是提供的日期。 否 `date` 提供參數，並返回最近的報告。 |

### 解釋標識名稱空間重疊報告

報告的結果可以從響應中的身份和配置檔案計數中解釋。 每行的數值告訴您有多少配置檔案是由標準和自定義標識命名空間的精確組合組成的。

請考慮以下摘錄 `data` 對象：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此報表提供以下資訊：

* 共有142個剖面 `AAID`。 `ECID`, `Email` 標準身份，以及自定義 `crmid` 標識命名空間。
* 有24個配置檔案，由 `AAID` 和 `ECID` 標識命名空間。
* 有6,565個配置檔案，只包含 `ECID` 身份。

## 生成未縫合配置檔案報告

您可以通過未縫合的配置檔案報告進一步瞭解組織配置檔案儲存的構成。 「未縫合」配置檔案是只包含一個配置檔案片段的配置檔案。 「未知」配置檔案是與假名標識命名空間(如 `ECID` 和 `AAID`。 未知配置檔案處於非活動狀態，這意味著它們在指定的時間段內沒有添加新事件。 未縫合的配置檔案報告提供了7、30、60、90和120天的配置檔案細目。

通過執行GET請求，可以生成未縫合配置檔案報告 `/previewsamplestatus/report/unstitchedProfiles` 端點。

**API格式**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**要求**

以下請求返回未縫合配置檔案報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的請求返回HTTP狀態200（確定）和未縫合配置檔案報告。

>[!NOTE]
>
>為本指南的目的，報告被截短，僅包括 `"120days"` 和`7days`&quot;期間。 完整未縫合配置檔案報告提供了7、30、60、90和120天的配置檔案細目。

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| 屬性 | 說明 |
|---|---|
| `data` | 的 `data` 對象包含為未縫合配置檔案報表返回的資訊。 |
| `totalNumberOfProfiles` | 配置檔案儲存中唯一配置檔案的總數。 這相當於可定址的觀眾數。 它包括已知和未縫合的配置檔案。 |
| `totalNumberOfEvents` | 配置檔案儲存中的ExperienceEvents總數。 |
| `unstitchedProfiles` | 包含未縫合配置檔案按時段細分的對象。 未縫合的配置檔案報告提供7、30、60、90和120天時段的配置檔案細目。 |
| `countOfProfiles` | 時間段的未縫合配置檔案計數或命名空間的未縫合配置檔案計數。 |
| `eventsAssociated` | 時間範圍的ExperienceEvents數或命名空間的事件數。 |
| `nsDistribution` | 包含單個標識命名空間的對象，每個命名空間具有未縫合配置檔案和事件的分佈。 注：合計 `countOfProfiles` 中每個標識命名空間的 `nsDistribution` 對象等於 `countOfProfiles` 的下界。 對於 `eventsAssociated` 每個命名空間和總數 `eventsAssociated` 每個時段。 |
| `reportTimestamp` | 報表的時間戳。 |

### 解釋未縫合配置檔案報表

報告結果可讓您深入瞭解您的組織在其配置檔案儲存中有多少未縫合和非活動配置檔案。

請考慮以下摘錄 `data` 對象：

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

此報表提供以下資訊：

* 有1,782個配置檔案只包含一個配置檔案片段，過去七天沒有新事件。
* 與1,782個未縫合配置檔案相關的體驗事件有29,151個。
* 有1,734個未縫合的配置檔案，其中包含來自ECID標識命名空間的單個配置檔案片段。
* 有28,591個事件與1,734個未縫合的配置檔案關聯，這些配置檔案包含來自ECID標識命名空間的單個配置檔案片段。

## 後續步驟

現在，您知道如何在配置檔案儲存中預覽示例資料並對資料運行多個報告，您還可以使用分段服務API的估計和預覽端點來查看有關段定義的摘要級別資訊。 此資訊有助於確保隔離您所在細分市場的預期受眾。 要瞭解有關使用分段API處理段預覽和估計的詳細資訊，請訪問 [預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)。

