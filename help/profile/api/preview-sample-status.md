---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；預覽；範例
title: 預覽範例狀態（設定檔預覽） API端點
description: 即時客戶設定檔API的預覽範例狀態端點可讓您預覽設定檔資料的最新成功範例、依資料集和身分列出設定檔分佈，並產生顯示資料集重疊、身分重疊和未拼接設定檔的報告。
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: bb2cfb479031f9e204006ba489281b389e6c6c04
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 1%

---

# 預覽樣本狀態端點（設定檔預覽）

Adobe Experience Platform可讓您從多個來源擷取客戶資料，以便為每個個別客戶建立強大且統一的設定檔。 將資料內嵌至Experience Platform後，會執行範例工作以更新設定檔計數和其他即時客戶設定檔資料相關量度。

此範例工作的結果可以使用`/previewsamplestatus`端點（即時客戶設定檔API的一部分）進行檢視。 此端點也可用來根據資料集和身分名稱空間列出設定檔分佈，以及產生多個報表，以瞭解您組織設定檔存放區的構成。 本指南會逐步說明使用`/previewsamplestatus` API端點檢視這些量度所需的步驟。

>[!NOTE]
>
>Adobe Experience Platform Segmentation Service API提供預估和預覽端點，可讓您檢視關於區段定義的摘要層級資訊，以協助您隔離預期對象。 若要尋找使用預覽和估計端點的詳細步驟，請瀏覽[預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md) （屬於[!DNL Segmentation] API開發人員指南的一部分）。

## 快速入門

本指南中使用的API端點是[[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en)的一部分。 繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 設定檔片段與合併的設定檔

本指南會同時參照「設定檔片段」和「合併的設定檔」。 在繼續之前，請務必瞭解這些辭彙之間的差異。

每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以構成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，則您的組織可能會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。

將設定檔片段擷取至Experience Platform時，會合併在一起（根據合併原則），以為該客戶建立單一設定檔。 因此，由於每個設定檔都是由多個片段組成，因此設定檔片段的總數可能會永遠高於合併的設定檔總數。

若要進一步瞭解設定檔及其在Experience Platform中的角色，請先閱讀[即時客戶設定檔總覽](../home.md)。

## 如何觸發範例作業

啟用即時客戶個人檔案的資料擷取到[!DNL Experience Platform]後，會儲存在個人檔案資料存放區中。 當將記錄擷取至設定檔存放區後，設定檔總數增加或減少超過3%，則會觸發取樣工作以更新計數。 範例的觸發方式取決於所使用的擷取型別：

* 對於&#x200B;**串流資料工作流程**，會每小時進行一次檢查，以判斷是否已達到3%的增加或減少臨界值。 如果有，則會自動觸發範例工作以更新計數。
* 對於&#x200B;**批次擷取**，在成功將批次擷取到設定檔存放區後15分鐘內，如果符合3%的增加或減少臨界值，則會執行工作以更新計數。 使用設定檔API，您可以預覽最新成功的範例作業，以及依資料集和身分名稱空間列出設定檔分佈。

在Experience Platform UI的[!UICONTROL Profiles]區段中，也可使用依名稱空間量度的設定檔計數和設定檔。 如需有關如何使用UI存取設定檔資料的資訊，請瀏覽[[!DNL Profile] UI指南](../ui/user-guide.md)。

## 檢視上一個範例狀態 {#view-last-sample-status}

您可以透過向`/previewsamplestatus`端點發出GET要求，檢視貴組織上次成功執行之範例工作的詳細資料。 此報表包含範例中的設定檔總數，以及設定檔計數量度，或您的組織在Experience Platform中的設定檔總數。

個人資料計數是在合併個人資料片段以針對每個個別客戶形成單一個人資料後產生的。 換言之，當設定檔片段合併在一起時，它們會傳回「1」設定檔計數，因為它們都與同一個人相關。

設定檔計數也包含具有屬性的設定檔（記錄資料），以及僅包含時間序列（事件）資料(例如Adobe Analytics設定檔)的設定檔。 範例工作會在擷取設定檔資料時定期更新，以便在Experience Platform中提供最新的設定檔總數。

**API格式**

```http
GET /previewsamplestatus
```

**要求**

+++ 檢視上一個範例狀態的範例要求。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**回應**

成功的回應會傳回HTTP狀態200，並包含上次為組織執行的成功範例工作的詳細資料。

+++ 包含最後一個範例狀態的範例回應。

>[!NOTE]
>
>在此範例回應中，`numRowsToRead`和`totalRows`彼此相等。 根據您的組織在Experience Platform中的設定檔數量，情況可能會如此。 不過，通常這兩個數字是不同的，`numRowsToRead`是較小的數字，因為它代表範例為設定檔總數(`totalRows`)的子集。

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | 範例中合併的設定檔總數。 |
| `sampleJobRunning` | 當範例工作正在進行時，傳回`true`的布林值。 將批次檔案實際新增至設定檔存放區時，針對該檔案上傳至時發生的延遲提供透明度。 |
| `docCount` | 資料庫中的檔案總數。 |
| `totalFragmentCount` | 設定檔存放區中的設定檔片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次擷取時間戳記。 |
| `streamingDriven` | *此欄位已過時，而且未包含回應的重要意義。* |
| `totalRows` | Experience Platform中合併的設定檔總數，也稱為設定檔計數。 |
| `lastBatchId` | 上一個批次擷取ID。 |
| `status` | 上一個範例的狀態。 |
| `samplingRatio` | 抽樣合併的設定檔(`numRowsToRead`)與合併的設定檔總數(`totalRows`)的比率，以小數格式表示。 |
| `mergeStrategy` | 範例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的範例時間戳記。 |

+++

## 依資料集列出設定檔分佈

您可以透過向`/previewsamplestatus/report/dataset`端點發出GET要求，依資料集檢視設定檔的分佈。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `date` | 指定要傳回的報表日期。 如果在當天執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 若未指定日期，則會傳回最近的報告。 格式： YYYY-MM-DD。 | `date=2024-12-31` |

**要求**

下列要求使用`date`引數傳回指定日期的最新報告。

+++ 依資料集擷取設定檔分佈的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**回應**

>[!NOTE]
>
>如果日期存在多個報表，則僅傳回最新的報表。 如果提供的日期不存在資料集報告，則會傳回HTTP狀態404 （找不到）。

成功的回應會傳回HTTP狀態200，並包含包含資料集物件清單的`data`陣列。

+++ 包含最新資料集物件的範例回應。

>[!NOTE]
>
>下列顯示的回應已截斷，以顯示三個資料集。

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
| -------- | ----------- |
| `sampleCount` | 使用此資料集ID的取樣合併設定檔總數。 |
| `samplePercentage` | `sampleCount`佔抽樣合併設定檔總數（在`numRowsToRead`上次樣本狀態[中傳回的](#view-last-sample-status)值）的百分比，以十進位格式表示。 |
| `fullIDsCount` | 具有此資料集ID的合併設定檔總數。 |
| `fullIDsPercentage` | `fullIDsCount`佔合併的設定檔總數（在`totalRows`最後一個範例狀態[中傳回的](#view-last-sample-status)值）的百分比，以十進位格式表示。 |
| `name` | 資料集的名稱，在資料集建立期間提供。 |
| `description` | 資料集的說明，在資料集建立期間提供。 |
| `value` | 資料集的識別碼。 |
| `streamingIngestionEnabled` | 資料集是否已啟用串流擷取。 |
| `createdUser` | 建立資料集之使用者的使用者ID。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請求期間提供了`date`引數，則傳回的報告會用於提供的日期。 如果未提供`date`引數，則會傳回最近的報告。 |

+++

## 依身分名稱空間列出設定檔分佈

您可以對`/previewsamplestatus/report/namespace`端點執行GET要求，以檢視個人資料存放區中所有合併個人資料中依身分名稱空間區分的劃分。 這包括Adobe提供的標準身分識別，以及貴組織定義的自訂身分識別。

身分識別名稱空間是Adobe Experience Platform Identity Service的重要元件，用途是作為客戶資料相關內容的指標。 若要深入瞭解，請先閱讀[身分名稱空間概觀](../../identity-service/features/namespaces.md)。

>[!NOTE]
>
>依名稱空間區分的設定檔總數（加總針對每個名稱空間顯示的值），可能會高於設定檔計數量度，因為一個設定檔可能會與多個名稱空間建立關聯。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 查詢參數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `date` | 指定要傳回的報表日期。 如果在當天執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 若未指定日期，則會傳回最近的報告。 格式： `YYYY-MM-DD`。 | `date=2025-6-20` |

**要求**

下列請求未指定`date`引數，將傳回最新報告。

+++ 傳回依名稱空間之設定檔分佈最新報表的範例要求。 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**回應**

成功的回應會傳回HTTP狀態200，並包含`data`陣列，以及包含每個名稱空間詳細資料的個別物件。 顯示的回應已截斷，顯示四個名稱空間。

+++ 範例回應包含依名稱空間區分的設定檔分佈相關資訊。

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
| -------- | ----------- |
| `sampleCount` | 名稱空間中取樣合併的設定檔總數。 |
| `samplePercentage` | `sampleCount`以抽樣合併設定檔的百分比表示（在`numRowsToRead`上次樣本狀態[中傳回的](#view-last-sample-status)值），以十進位格式表示。 |
| `reportTimestamp` | 報表的時間戳記。 如果在請求期間提供了`date`引數，則傳回的報告會用於提供的日期。 如果未提供`date`引數，則會傳回最近的報告。 |
| `fullIDsFragmentCount` | 名稱空間中的設定檔片段總數。 |
| `fullIDsCount` | 名稱空間中合併的設定檔總數。 |
| `fullIDsPercentage` | `fullIDsCount`佔合併的設定檔總數的百分比（在`totalRows`最後一個範例狀態[中傳回的](#view-last-sample-status)值），以十進位格式表示。 |
| `code` | 名稱空間的`code`。 使用[Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md)處理名稱空間時，可找到此專案，在Experience Platform UI中也稱為[!UICONTROL Identity symbol]。 若要深入瞭解，請造訪[身分名稱空間概觀](../../identity-service/features/namespaces.md)。 |
| `value` | 名稱空間的`id`值。 使用[Identity Service API](../../identity-service/api/list-namespaces.md)處理名稱空間時，可以找到此專案。 |

+++

## 列出資料集統計資料 {#dataset-stats}

您可以藉由對`/previewsamplestatus/report/dataset_stats`端點發出GET要求，產生可提供資料集相關統計資料的報表。

**API格式**

```http
GET /previewsamplestatus/report/dataset_stats
```

**要求**

+++ 產生資料集統計報表的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含資料集統計資料的相關資訊。

+++ 包含資料集統計資料相關資訊的範例回應。

>[!NOTE]
>
>下列回應已截斷，顯示三個資料集。

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `120days` | 120天資料過期後仍會保留在資料集中的記錄數。 |
| `14days` | 資料過期14天後仍會保留在資料集中的記錄數。 |
| `30days` | 30天資料過期後仍會保留在資料集中的記錄數。 |
| `365days` | 365天資料到期後仍會保留在資料集中的記錄數。 |
| `60days` | 資料過期60天後仍會保留在資料集中的記錄數。 |
| `7days` | 資料過期7天後仍會保留在資料集中的記錄數。 |
| `90days` | 資料過期90天後仍會保留在資料集中的記錄數。 |
| `datasetId` | 資料集的識別碼。 |
| `datasetType` | 資料集型別。 此值可以是`Profiles`或`ExperienceEvents`。 |
| `percentEvents` | 資料集內的體驗事件記錄百分比。 |
| `percentProfiles` | 資料集中的設定檔記錄的百分比。 |
| `profileFragments` | 資料集中存在的設定檔片段總數。 |
| `records` | 擷取到資料集中的設定檔記錄總數。 |
| `totalProfiles` | 擷取到資料集中的設定檔總數。 |

+++

## 取得資料集大小 {#character-count}

您可以使用此端點每週取得資料集的大小（以位元組為單位）。

**API格式**

```http
GET /previewsamplestatus/report/character_count
```

**要求**

+++產生字元計數報表的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/character_count \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含整週資料集大小的相關資訊。

+++ 包含資料過期後資料集大小相關資訊的範例回應。

>[!NOTE]
>
>下列回應已截斷，顯示三個資料集。

```json
{
    "data": [
        {
            "datasetIds": [
                {
                    "datasetId": "67aba91a453f7d298cd2a643",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 107773533894,
                            "week": "2025-10-26"
                        }
                    ]
                },
                {
                    "datasetId": "67aa6c867c3110298b017f0e",
                    "recordType": "timeseries",
                    "weeks": [
                        {
                            "size": 242902062440,
                            "week": "2025-10-26"
                        },
                        {
                            "size": 837539413062,
                            "week": "2025-10-19"
                        },
                        {
                            "size": 479253986484,
                            "week": "2025-10-12"
                        },
                        {
                            "size": 358911988990,
                            "week": "2025-10-05"
                        },
                        {
                            "size": 349701073042,
                            "week": "2025-09-28"
                        }
                    ]
                },
                {
                    "datasetId": "680c043667c0d7298c9ea275",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 18392459832,
                            "week": "2025-10-26"
                        }
                    ]
                }
            ],
            "modelName": "_xdm.context.profile",
            "reportTimestamp": "2025-10-30T00:28:30.069Z"
        }
    ],
    "reportTimestamp": "2025-10-30T00:28:30.069Z"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 資料集的識別碼。 |
| `recordType` | 資料集中的資料型別。 記錄型別會影響`weeks`變數的值。 支援的值包括`keyvalue`和`timeseries`。 |
| `weeks` | 包含資料集大小資訊的陣列。 對於記錄型別`keyvalue`的資料集，這會包含最近一週以及資料集的總大小（位元組）。 對於記錄型別`timeseries`的資料集，這會包含從資料集擷取到最近一週的每一週，以及這些周中每一週的資料集總大小（位元組）。 |
| `modelName` | 資料集的模型名稱。 可能的值包括`_xdm.context.profile`和`_xdm.context.experienceevent`。 |
| `reportTimestamp` | 產生報表的日期和時間。 |

+++

## 後續步驟

現在您知道如何在設定檔存放區中預覽範例資料，並對資料執行多個報告，您還可以使用分段服務API的估計和預覽端點，檢視有關您區段定義的摘要層級資訊。 此資訊可協助您確保隔離預期的對象。 若要進一步瞭解如何使用分段API來處理預覽和預估，請造訪[預覽和預估端點指南](../../segmentation/api/previews-and-estimates.md)。

