---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難排解；API；預覽；示例
title: 預覽範例狀態（描述檔預覽）API端點
description: 使用「即時客戶描述檔API」的一部分預覽範例狀態端點，您可以預覽您描述檔資料的最新成功範例，以及依資料集和Adobe Experience Platform境內的身分命名空間來分發清單描述檔。
topic-legacy: guide
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 1%

---

# 預覽範例狀態端點（描述檔預覽）

Adobe Experience Platform可讓您從多個來源收集客戶資料，以便為個別客戶建立強穩的統一個人檔案。 當啟用「即時客戶描述檔」的資料被收錄到[!DNL Platform]時，它會儲存在「描述檔」資料儲存區中。

當將記錄擷取至描述檔儲存區時，會觸發取樣工作以更新該計數，將總描述檔計數增加或減少超過5%。 觸發範例的方式取決於使用的擷取類型：

* 對於&#x200B;**串流資料工作流程**，會每小時檢查一次，以判斷是否符合5%增加或減少臨界值。 如果已觸發，系統會自動觸發範例工作以更新計數。
* 對於&#x200B;**批次提取**，在成功將批次提取到配置檔案儲存的15分鐘內，如果滿足5%增加或減少閾值，則運行作業以更新計數。 使用描述檔API，您可以預覽最新成功的範例工作，以及依資料集和身分命名空間來列出描述檔散發。

這些量度也可在Experience PlatformUI的[!UICONTROL Profiles]區段中使用。 有關如何使用UI存取描述檔資料的資訊，請造訪[[!DNL Profile] 使用指南](../ui/user-guide.md)。

>[!NOTE]
>
>Adobe Experience Platform區段服務API提供預估和預覽端點，可讓您檢視區段定義的摘要層級資訊，以協助您隔離預期的觀眾。 若要尋找使用區段預覽和估計端點的詳細步驟，請造訪[預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)，此為[!DNL Segmentation] API開發人員指南的一部分。

## 快速入門

本指南中使用的API端點是[[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 描述檔片段與合併的描述檔

本指南同時引用「描述檔片段」和「合併的描述檔」。 請務必先瞭解這些術語之間的差異，再繼續。

每個客戶個人檔案都由多個已合併的個人檔案片段組成，以形成該客戶的單一檢視。 例如，如果客戶透過多個通道與您的品牌互動，您的組織將會在多個資料集中顯示與該單一客戶相關的多個描述檔片段。 當這些片段被收錄到Platform中時，它們會合併（根據合併原則），以便為該客戶建立單一個人檔案。 因此，由於每個描述檔由多個片段組成，因此描述檔片段的總數可能永遠高於合併描述檔的總數。

## 查看最後一個示例狀態{#view-last-sample-status}

您可以對`/previewsamplestatus`端點執行GET請求，以檢視您IMS組織上次成功執行範例工作的詳細資料。 這包括範例中的描述檔總數，以及描述檔計數量度，或您組織在Experience Platform中的描述檔總數。 描述檔計數是在合併一些描述檔片段後產生，以針對每個個別客戶形成單一描述檔。 換言之，您的組織可能有多個與跨不同通道與品牌互動的單一客戶相關的描述檔片段，但這些片段會合併在一起（根據預設合併政策），並會傳回「1」個描述檔計數，因為這些片段都與同一個人相關。

描述檔計數還包括具有屬性（記錄資料）的描述檔，以及僅包含時間系列（事件）資料的描述檔，例如Adobe Analytics描述檔。 當擷取描述檔資料時，系統會定期重新整理範例工作，以便提供平台內的最新描述檔總數。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含上次為IMS組織執行之成功範例工作的詳細資訊。

>[!NOTE]
>
>在此示例響應中，`numRowsToRead`和`totalRows`彼此相等。 視您的組織在Experience Platform中的設定檔數量而定，情況可能是這樣。 但是，這兩個數字通常不同，`numRowsToRead`是較小的數字，因為它表示樣本是配置檔案總數(`totalRows`)的子集。

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
| `numRowsToRead` | 範例中合併的描述檔總數。 |
| `sampleJobRunning` | 一個布爾值，在示例作業進行中時返回`true`。 對實際將批次檔案新增至描述檔存放區時的延遲提供透明度。 |
| `cosmosDocCount` | Cosmos中的檔案總計。 |
| `totalFragmentCount` | 描述檔儲存區中的描述檔片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次擷取時間戳記。 |
| `streamingDriven` | *此欄位已過時，且不包含回應的重要性。* |
| `totalRows` | Experience Platform中合併的描述檔總數，也稱為「描述檔計數」。 |
| `lastBatchId` | 上次批次擷取ID。 |
| `status` | 最後一個範例的狀態。 |
| `samplingRatio` | 採樣的合併配置檔案(`numRowsToRead`)與合併配置檔案(`totalRows`)的比率，以小數格式表示。 |
| `mergeStrategy` | 範例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的範例時間戳記。 |

## 依資料集的清單描述檔分發

若要依資料集檢視描述檔的分佈，您可以對`/previewsamplestatus/report/dataset`端點執行GET要求。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回404錯誤。 如果未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求使用`date`參數，傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

響應包括`data`陣列，包含資料集對象清單。 顯示的回應已截斷，以顯示三個資料集。

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
| `samplePercentage` | `sampleCount`是取樣合併描述檔總數的百分比（[最後一個示例狀態](#view-last-sample-status)中傳回的`numRowsToRead`值），以小數格式表示。 |
| `fullIDsCount` | 使用此資料集ID的合併描述檔總數。 |
| `fullIDsPercentage` | `fullIDsCount`是合併描述檔總數的百分比（[最後一個範例狀態](#view-last-sample-status)中傳回的`totalRows`值），以小數格式表示。 |
| `name` | 資料集的名稱，如建立資料集時所提供。 |
| `description` | 資料集的說明，如建立資料集時所提供。 |
| `value` | 資料集的ID。 |
| `streamingIngestionEnabled` | 資料集是否啟用串流擷取。 |
| `createdUser` | 建立資料集之使用者的使用者ID。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請求期間提供`date`參數，則傳回的報表是提供日期。 如果未提供`date`參數，則會傳回最近的報表。 |

## 依命名空間列出描述檔分發

您可以對`/previewsamplestatus/report/namespace`端點執行GET請求，以在您的描述檔商店中，依識別名稱空間檢視劃分。 身分名稱空間是Adobe Experience Platform身分服務的重要元件，可做為客戶資料相關內容的指標。 若要進一步瞭解，請造訪[identity namespace overview](../../identity-service/namespaces.md)。

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
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多份報表，則會傳回該日期的最新報表。 如果報表在指定日期不存在，則會傳回404錯誤。 如果未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求未指定`date`參數，因此會傳回最新的報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含`data`陣列，其中包含每個命名空間的詳細資料的個別物件。 顯示的回應已截斷，以顯示四個名稱空間。

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
| `samplePercentage` | `sampleCount`是取樣合併描述檔的百分比（[最後一個示例狀態](#view-last-sample-status)中返回的`numRowsToRead`值），以小數格式表示。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請求期間提供`date`參數，則傳回的報表是提供日期。 如果未提供`date`參數，則會傳回最近的報表。 |
| `fullIDsFragmentCount` | 命名空間中的描述檔片段總數。 |
| `fullIDsCount` | 命名空間中合併的描述檔總數。 |
| `fullIDsPercentage` | `fullIDsCount`佔合併描述檔總數的百分比（[最後一個範例狀態](#view-last-sample-status)中傳回的`totalRows`值），以小數格式表示。 |
| `code` | namespace的`code`。 使用[Adobe Experience PlatformIdentity Service API](../../identity-service/api/list-namespaces.md)使用名稱空間時，可找到此點，也稱為Experience PlatformUI中的[!UICONTROL Identity symbol]。 若要進一步瞭解，請造訪[identity namespace overview](../../identity-service/namespaces.md)。 |
| `value` | namespace的`id`值。 使用[Identity Service API](../../identity-service/api/list-namespaces.md)使用名稱空間時，可以找到此點。 |

## 後續步驟

現在您知道如何在描述檔儲存區中預覽範例資料，您也可以使用分段服務API的估計和預覽端點來檢視區段定義的摘要層級資訊。 這些資訊有助於確保您隔離區段中預期的觀眾。 若要進一步瞭解如何使用區段預覽和估計，請造訪[預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)。
