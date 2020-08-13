---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: 描述檔預覽——即時客戶描述檔API
description: Adobe Experience Platform可讓您從多個來源收集客戶資料，為個別客戶建立強穩的統一個人檔案。 當啟用「即時客戶描述檔」的資料被收錄到「平台」中時，該資料會儲存在「描述檔」資料儲存區中。 隨著描述檔儲存區中記錄數的增加或減少，會執行範例工作，其中包含資料儲存區中有多少描述檔片段和合併的描述檔的相關資訊。 使用描述檔API，您可以預覽最新成功的範例，以及依資料集和身分命名空間來列出描述檔散發。
topic: guide
translation-type: tm+mt
source-git-commit: 75a07abd27f74bcaa2c7348fcf43820245b02334
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 1%

---


# 預覽範例狀態端點（描述檔預覽）

Adobe Experience Platform可讓您從多個來源收集客戶資料，為個別客戶建立強穩的統一個人檔案。 當「即時客戶描述檔」啟用的資料已收錄到其中 [!DNL Platform]時，它會儲存在「描述檔」資料儲存區中。

當將記錄擷取至描述檔存放區時，會觸發工作以更新該計數，將總描述檔計數增加或減少超過5%。 對於串流資料工作流程，會每小時檢查一次，以判斷是否符合5%增加或減少臨界值。 如果已觸發，則會自動觸發作業以更新計數。 對於批處理，在成功將批處理裝入配置檔案儲存的15分鐘內，如果達到5%增加或減少閾值，則運行作業以更新計數。 使用描述檔API，您可以預覽最新成功的範例工作，以及依資料集和身分命名空間來列出描述檔散發。

這些量度也可在Experience Platform UI的「 [!UICONTROL Profiles] 」區段中使用。 如需如何使用UI存取描述檔資料的詳細資訊，請造訪使 [[!DNL Profile] 用指南](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是 [[!DNL Real-time Customer Profile] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 查看最後一個示例狀態 {#view-last-sample-status}

您可以對端點執行GET請 `/previewsamplestatus` 求，以檢視您IMS組織上次成功執行範例工作的詳細資訊。 這包括範例中的描述檔總數，以及描述檔計數量度，或您的組織在Experience Platform中擁有的描述檔總數。 描述檔計數是在合併一些描述檔片段後產生，以針對每個個別客戶形成單一描述檔。 換言之，您的組織可能有多個與跨不同通道與品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併政策），並會傳回「1」個描述檔計數，因為這些片段都與同一個人相關。

描述檔計數也包含具有屬性（記錄資料）的描述檔，以及僅包含時間系列（事件）資料的描述檔，例如Adobe Analytics描述檔。 當擷取描述檔資料時，系統會定期重新整理範例工作，以便提供平台內的最新描述檔總數。

**API格式**

```http
GET /previewsamplestatus
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含上次為IMS組織執行之成功範例工作的詳細資訊。

>[!NOTE]
>
>在此示例響應中， `numRowsToRead` 並 `totalRows` 且彼此相等。 視貴組織在Experience Platform中擁有的設定檔數而定。 但是，這兩個數字通常不同， `numRowsToRead` 因為它表示樣本是描述檔總數(`totalRows`)的子集。

```json
{
  "numRowsToRead": "41003",
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
| `numRowsToRead` | 範例中合併的描述檔總數。 |
| `cosmosDocCount` | Cosmos中的檔案總計。 |
| `totalFragmentCount` | 描述檔儲存區中的描述檔片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次擷取時間戳記。 |
| `streamingDriven` | *此欄位已過時，且不包含回應的重要性。* |
| `totalRows` | Experience平台中合併的設定檔總數，也稱為「設定檔計數」。 |
| `lastBatchId` | 上次批次擷取ID。 |
| `status` | 最後一個範例的狀態。 |
| `samplingRatio` | 採樣()的合併描述檔`numRowsToRead`與合併描述檔總計(`totalRows`)的比率，以小數格式的百分比表示。 |
| `mergeStrategy` | 範例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的範例時間戳記。 |

## 依資料集的清單描述檔分發

若要依資料集檢視描述檔的分佈，您可以對端點執行GET `/previewsamplestatus/report/dataset` 要求。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回404錯誤。 如果未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例: `date=2024-12-31` |

**請求**

下列請求會使用 `date` 參數，傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

該響應包括 `data` 包含資料集對象的清單的陣列。 顯示的回應已截斷，以顯示三個資料集。

>[!NOTE]
>
>如果日期存在多個報表，則只會傳回最新的報表。 如果資料集報表不存在於提供的日期，則會傳回HTTP狀態404（找不到）。

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
| `sampleCount` | 使用此資料集ID的取樣合併描述檔總數。 |
| `samplePercentage` | 以 `sampleCount` 小數格式表示的取樣合併描述檔總數( `numRowsToRead` 上次取樣狀 [態傳回的值](#view-last-sample-status))的百分比。 |
| `fullIDsCount` | 使用此資料集ID的合併描述檔總數。 |
| `fullIDsPercentage` | 以 `fullIDsCount` 小數格式表示的合併描述檔總數百分比( `totalRows` 在上個範例狀態 [中傳回的值](#view-last-sample-status))。 |
| `name` | 資料集的名稱，如建立資料集時所提供。 |
| `description` | 資料集的說明，如建立資料集時所提供。 |
| `value` | 資料集的ID。 |
| `streamingIngestionEnabled` | 資料集是否啟用串流擷取。 |
| `createdUser` | 建立資料集之使用者的使用者ID。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請 `date` 求期間提供參數，則傳回的報表會是提供日期。 如果未提 `date` 供參數，則會傳回最近的報表。 |



## 依命名空間列出描述檔分發

您可以對端點執行GET請求， `/previewsamplestatus/report/namespace` 以在您的描述檔商店中，依識別名稱空間檢視劃分。 身分名稱空間是Adobe Experience Platform Identity Service的重要元件，可做為客戶資料相關內容的指標。 若要進一步瞭解，請造訪 [身分命名空間概觀](../../identity-service/namespaces.md)。

>[!NOTE]
>
>依名稱空間劃分的描述檔總數（將每個名稱空間顯示的值加在一起）一律會高於描述檔計數量度，因為一個描述檔可能與多個名稱空間相關聯。 例如，如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶關聯。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回404錯誤。 如果未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例: `date=2024-12-31` |

**請求**

下列請求不會指定參 `date` 數，因此會傳回最近的報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含一個 `data` 陣列，其中包含每個命名空間的詳細資料的個別物件。 顯示的回應已截斷，以顯示四個名稱空間。

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
| `sampleCount` | 命名空間中取樣的合併描述檔總數。 |
| `samplePercentage` | 以 `sampleCount` 小數格式表示的取樣合併描述檔( `numRowsToRead` 上次取樣狀態 [中傳回的值](#view-last-sample-status))的百分比。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請 `date` 求期間提供參數，則傳回的報表會是提供日期。 如果未提 `date` 供參數，則會傳回最近的報表。 |
| `fullIDsFragmentCount` | 命名空間中的描述檔片段總數。 |
| `fullIDsCount` | 命名空間中合併的描述檔總數。 |
| `fullIDsPercentage` | 以 `fullIDsCount` 小數格式表示的合併描述檔總數( `totalRows` 上個範例狀態 [中傳回的值](#view-last-sample-status))的百分比。 |
| `code` | namespace `code` 的名稱空間。 使用 [Adobe Experience Platform Identity Service API使用名稱空間時可找到此點](../../identity-service/api/list-namespaces.md) ，也稱為Experience Platform UI中的  Identity符號。 若要進一步瞭解，請造訪 [身分命名空間概觀](../../identity-service/namespaces.md)。 |
| `value` | 命名 `id` 空間的值。 使用 [Identity Service API使用名稱空間時，可找到此點](../../identity-service/api/list-namespaces.md)。 |

## 後續步驟

您也可以使用類似的估計和預覽來檢視區段定義的摘要層級資訊，以協助您隔離預期的觀眾。 若要尋找使用 [!DNL Adobe Experience Platform Segmentation Service] API處理區段預覽和估計的詳細步驟，請造訪API開發 [人員指南中的預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)[!DNL Segmentation] 。

