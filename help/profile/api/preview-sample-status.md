---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；預覽；範例
title: 預覽範例狀態（設定檔預覽）API端點
description: 即時客戶設定檔API的預覽範例狀態端點可讓您預覽設定檔資料的最新成功範例、依資料集和身分列出設定檔分送，以及產生顯示資料集重疊、身分重疊和未拼接設定檔的報表。
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 1%

---

# 預覽示例狀態終結點（配置檔案預覽）

Adobe Experience Platform可讓您內嵌來自多個來源的客戶資料，以便為每個個別客戶建立強大且統一的設定檔。 將資料內嵌至Platform時，會執行範例工作以更新設定檔計數和其他與即時客戶設定檔資料相關的量度。

此範例工作的結果可使用 `/previewsamplestatus` 端點，即時客戶設定檔API的一部分。 此端點也可用來列出資料集和身分命名空間的設定檔分配，以及產生多個報表，以便洞察組織的設定檔存放區組成。 本指南會逐步說明使用 `/previewsamplestatus` API端點。

>[!NOTE]
>
>Adobe Experience Platform分段服務API提供預估和預覽端點，可讓您檢視關於區段定義的摘要層級資訊，以協助您確保隔離預期的對象。 若要尋找使用區段預覽和預估端點的詳細步驟，請造訪 [預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md), [!DNL Segmentation] API開發人員指南。

## 快速入門

本指南中使用的API端點屬於 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 設定檔片段與合併的設定檔

本指南會同時參考「設定檔片段」和「已合併的設定檔」。 在繼續之前，請務必了解這些術語之間的差異。

每個個別客戶設定檔都由多個已合併的設定檔片段組成，以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織可能會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。

將設定檔片段擷取至Platform時，會合併這些片段（根據合併原則），以便為該客戶建立單一設定檔。 因此，由於每個設定檔由多個片段組成，因此設定檔片段的總數可能一律高於合併設定檔的總數。

若要進一步了解設定檔及其在Experience Platform中的角色，請先閱讀 [即時客戶個人檔案概觀](../home.md).

## 範例工作的觸發方式

當為「即時客戶設定檔」啟用的資料擷取至 [!DNL Platform]，則會儲存在設定檔資料存放區中。 當將記錄擷取至設定檔存放區時，總設定檔計數會增加或減少超過5%，就會觸發取樣工作以更新計數。 觸發範例的方式取決於使用的擷取類型：

* 針對 **串流資料工作流程**，則會每小時進行檢查，以判斷是否符合5%增加或減少臨界值。 若已觸發，則會自動觸發範例工作以更新計數。
* 針對 **批次內嵌**，在成功將批次擷取至設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新計數。 使用設定檔API，您可以預覽最新成功的範例工作，以及依資料集和身分命名空間列出設定檔分送。

您也可以在 [!UICONTROL 設定檔] 區段。 如需如何使用UI存取設定檔資料的資訊，請造訪 [[!DNL Profile] UI指南](../ui/user-guide.md).

## 查看最後一個示例狀態 {#view-last-sample-status}

您可以對 `/previewsamplestatus` 端點來檢視上次為貴組織執行的成功範例作業的詳細資訊。 這包括範例中的設定檔總數，以及設定檔計數量度，或您的組織在Experience Platform內的設定檔總數。

將設定檔片段合併為每個個別客戶的單一設定檔後，會產生設定檔計數。 換句話說，將設定檔片段合併在一起時，會傳回「1」設定檔的計數，因為它們都與相同的個人相關。

設定檔計數也包含具有屬性（記錄資料）的設定檔，以及僅包含時間序列（事件）資料的設定檔，例如Adobe Analytics設定檔。 擷取設定檔資料時，範例工作會定期重新整理，以提供Platform內最新的設定檔總數。

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

回應包含上次為組織執行的成功範例作業的詳細資訊。

>[!NOTE]
>
>在此範例回應中， `numRowsToRead` 和 `totalRows` 彼此相等。 視貴組織在Experience Platform中擁有的設定檔數量而定，情況可能會如此。 不過，這兩個數字通常不同， `numRowsToRead` 較小，因為它代表範例為設定檔總數的子集(`totalRows`)。

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
| `numRowsToRead` | 範例中合併的設定檔總數。 |
| `sampleJobRunning` | 傳回的布林值 `true` 執行範例工作時。 提供將批次檔案上傳至實際新增至設定檔存放區時的延遲透明度。 |
| `cosmosDocCount` | Cosmos中的文檔總數。 |
| `totalFragmentCount` | 設定檔存放區中的設定檔片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功批次擷取時間戳記。 |
| `streamingDriven` | *此欄位已遭取代，且對回應不含任何意義。* |
| `totalRows` | Experience Platform中合併的設定檔總數，也稱為「設定檔計數」。 |
| `lastBatchId` | 上次批次擷取ID。 |
| `status` | 上一個示例的狀態。 |
| `samplingRatio` | 已合併的描述檔取樣的比率(`numRowsToRead`)，總計合併的設定檔(`totalRows`)，以小數格式的百分比表示。 |
| `mergeStrategy` | 範例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的範例時間戳記。 |

## 按資料集列出配置檔案分發

若要依資料集查看設定檔的分佈，您可以向 `/previewsamplestatus/report/dataset` 端點。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求會使用 `date` 參數來傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含 `data` 陣列，包含資料集物件清單。 顯示的回應已截斷，以顯示三個資料集。

>[!NOTE]
>
>如果該日期有多個報表，則只會傳回最新的報表。 如果提供的日期沒有資料集報表，則會傳回HTTP狀態404（找不到）。

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
| `sampleCount` | 使用此資料集ID的取樣合併設定檔總數。 |
| `samplePercentage` | 此 `sampleCount` 取樣合併設定檔總數的百分比( `numRowsToRead` 值，如 [上次範例狀態](#view-last-sample-status))，以小數格式表示。 |
| `fullIDsCount` | 具有此資料集ID的合併設定檔總數。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 以合併設定檔總數的百分比( `totalRows` 值，如 [上次範例狀態](#view-last-sample-status))，以小數格式表示。 |
| `name` | 資料集的名稱，如建立資料集期間所提供。 |
| `description` | 資料集的說明，如建立資料集期間所提供。 |
| `value` | 資料集的ID。 |
| `streamingIngestionEnabled` | 資料集是否啟用串流內嵌功能。 |
| `createdUser` | 建立資料集之使用者的使用者ID。 |
| `reportTimestamp` | 報表的時間戳記。 若 `date` 參數時，傳回的報表會是提供日期的。 若否 `date` 參數時，會傳回最新的報表。 |

## 按身份命名空間列出配置檔案分發

您可以對 `/previewsamplestatus/report/namespace` 端點來檢視「設定檔存放區」中所有合併設定檔的劃分，並依身分命名空間劃分。 這包括Adobe提供的標準身分識別，以及貴組織定義的自訂身分識別。

身分識別命名空間是Adobe Experience Platform Identity Service的重要元件，可作為客戶資料相關內容的指標。 若要進一步了解，請先閱讀 [身分命名空間概述](../../identity-service/namespaces.md).

>[!NOTE]
>
>依命名空間的設定檔總數（將每個命名空間顯示的值加總）可能比設定檔計數量度高，因為一個設定檔可能與多個命名空間相關聯。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在日期上執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求未指定 `date` 參數和，因此會傳回最新的報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含 `data` 陣列，包含每個命名空間的詳細資訊的個別物件。 顯示的回應已截斷，以顯示四個命名空間。

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
| `sampleCount` | 命名空間中取樣的合併設定檔總數。 |
| `samplePercentage` | 此 `sampleCount` 取樣的合併設定檔百分比( `numRowsToRead` 值，如 [上次範例狀態](#view-last-sample-status))，以小數格式表示。 |
| `reportTimestamp` | 報表的時間戳記。 若 `date` 參數時，傳回的報表會是提供日期的。 若否 `date` 參數時，會傳回最新的報表。 |
| `fullIDsFragmentCount` | 命名空間中的設定檔片段總數。 |
| `fullIDsCount` | 命名空間中合併的設定檔總數。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 以百分比表示合併的設定檔總數( `totalRows` 值，如 [上次範例狀態](#view-last-sample-status))，以小數格式表示。 |
| `code` | 此 `code` 命名空間。 使用的命名空間 [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) 和也稱為 [!UICONTROL 標識符] 在Experience PlatformUI中。 若要進一步了解，請造訪 [身分命名空間概述](../../identity-service/namespaces.md). |
| `value` | 此 `id` 值。 使用的命名空間 [Identity服務API](../../identity-service/api/list-namespaces.md). |

## 產生資料集重疊報表

資料集重疊報表會顯示對可定址對象（合併的設定檔）貢獻最大的資料集，讓您掌握組織的設定檔存放區組成。 除了提供資料的深入分析外，此報表還可協助您採取動作，以最佳化授權使用情形，例如為特定資料集設定到期日。

您可以對 `/previewsamplestatus/report/dataset/overlap` 端點。

如需逐步指示，說明如何使用命令列或Postman UI產生資料集重疊報表，請參閱 [產生資料集重疊報表教學課程](../tutorials/dataset-overlap-report.md).

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在相同日期執行多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求會使用 `date` 參數來傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的要求會傳回HTTP狀態200（確定）和資料集重疊報表。

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
| `data` | 此 `data` 物件包含以逗號分隔的資料集清單及其個別的設定檔計數。 |
| `reportTimestamp` | 報表的時間戳記。 若 `date` 參數時，傳回的報表會是提供日期的。 若否 `date` 參數時，會傳回最新的報表。 |

### 解譯資料集重疊報表

您可以從回應中的資料集和設定檔計數來解讀報表結果。 請考量下列範例報表 `data` 物件：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報告提供下列資訊：

* 有123個設定檔，由來自下列資料集的資料組成： `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 來自這兩個資料集的資料共454,412個設定檔： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107個設定檔僅由資料集的資料組成 `5eeda0032af7bb19162172a7`.
* 組織中共有454,642個設定檔。

## 產生身分命名空間重疊報表 {#identity-overlap-report}

身分命名空間重疊報表會公開對可定址對象（合併的設定檔）貢獻最大的身分命名空間，讓您可洞察組織的設定檔存放區組成。 這包括Adobe提供的標準身分識別命名空間，以及貴組織定義的自訂身分識別命名空間。

您可以執行GET請求，以產生身分命名空間重疊報表 `/previewsamplestatus/report/namespace/overlap` 端點。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在相同日期執行多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404（找不到）錯誤。 若未指定日期，則會傳回最近的報表。 格式：YYYY-MM-DD。 範例：`date=2024-12-31` |

**要求**

下列請求會使用 `date` 參數來傳回指定日期的最新報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的要求會傳回HTTP狀態200（確定）和身分命名空間重疊報表。

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
| `data` | 此 `data` 物件包含以逗號分隔的清單，以及身分命名空間程式碼及其個別設定檔計數的不重複組合。 |
| 命名空間代碼 | 此 `code` 是每個身分命名空間名稱的簡短表單。 每個 `code` 到 `name` 可使用 [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md). 此 `code` 也稱為 [!UICONTROL 標識符] 在Experience PlatformUI中。 若要進一步了解，請造訪 [身分命名空間概述](../../identity-service/namespaces.md). |
| `reportTimestamp` | 報表的時間戳記。 若 `date` 參數時，傳回的報表會是提供日期的。 若否 `date` 參數時，會傳回最新的報表。 |

### 解譯身分命名空間重疊報表

報表的結果可從回應中的身分和設定檔計數來解讀。 每一列的數值會告訴您有多少個設定檔是由標準與自訂身分命名空間的精確組合所組成。

請考量下列摘自 `data` 物件：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此報告提供下列資訊：

* 共有142個設定檔，由 `AAID`, `ECID`，和 `Email` 標準身分識別，以及來自自訂 `crmid` 身分識別命名空間。
* 共有24個設定檔，由 `AAID` 和 `ECID` 身分識別命名空間。
* 有6,565個設定檔僅包含 `ECID` 身份。

## 產生未拼接的設定檔報表

您可以透過未拼接的設定檔報表，進一步洞察組織的設定檔存放區組成。 「未拼接」的設定檔是只包含一個設定檔片段的設定檔。 「未知」設定檔是與假名身分命名空間(例如 `ECID` 和 `AAID`. 未知的設定檔為非作用中狀態，這表示在指定時段內未新增事件。 未拼接的設定檔報表提供7、30、60、90和120天期間的設定檔劃分。

您可以對 `/previewsamplestatus/report/unstitchedProfiles` 端點。

**API格式**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**要求**

下列請求會傳回未拼接的設定檔報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的請求會傳回HTTP狀態200（確定）和未拼接的設定檔報表。

>[!NOTE]
>
>在本指南中，報表已截斷，僅包含 `"120days"` 和`7days`&quot;時段。 完整未拼接的設定檔報表提供7、30、60、90和120天期間的設定檔劃分。

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
| `data` | 此 `data` 物件包含為未拼接的設定檔報表傳回的資訊。 |
| `totalNumberOfProfiles` | 設定檔存放區中不重複設定檔的總數。 這等同於可定址的受眾計數。 其中包含已知和未匯整的設定檔。 |
| `totalNumberOfEvents` | 設定檔存放區中的ExperienceEvents總數。 |
| `unstitchedProfiles` | 包含依時段劃分未拼接描述檔的物件。 未拼接的設定檔報表提供7、30、60、90和120天時段的設定檔劃分。 |
| `countOfProfiles` | 時段的未連結設定檔計數，或命名空間的未連結設定檔計數。 |
| `eventsAssociated` | 時間範圍的ExperienceEvents數量或命名空間的事件數。 |
| `nsDistribution` | 一個物件，包含個別身分識別命名空間，以及每個命名空間未匯整的設定檔和事件的分佈。 注意：加總 `countOfProfiles` 中的每個身分命名空間 `nsDistribution` 物件等於 `countOfProfiles` 期間。 對於 `eventsAssociated` 每個命名空間及總計 `eventsAssociated` 每個時段。 |
| `reportTimestamp` | 報表的時間戳記。 |

### 解譯未拼接的設定檔報表

報表結果可讓您深入分析您的組織在其設定檔存放區中有多少未連結和非使用中的設定檔。

請考量下列摘自 `data` 物件：

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

此報告提供下列資訊：

* 有1,782個設定檔僅包含一個設定檔片段，且過去七天內沒有新事件。
* 有29,151個ExperienceEvents與1,782個未拼接的設定檔相關聯。
* 有1,734個未拼接的設定檔，包含ECID身分命名空間中的單一設定檔片段。
* 有28,591個事件與1,734個未拼接的設定檔相關聯，這些設定檔包含來自ECID身分識別命名空間的單一設定檔片段。

## 後續步驟

現在您知道如何在設定檔存放區中預覽範例資料，並對資料執行多個報表，您也可以使用分段服務API的預估和預覽端點來檢視關於區段定義的摘要層級資訊。 此資訊可協助確保您隔離區段中預期的對象。 若要進一步了解如何使用區段API來處理區段預覽和估計，請造訪 [預覽和預估端點指南](../../segmentation/api/previews-and-estimates.md).

