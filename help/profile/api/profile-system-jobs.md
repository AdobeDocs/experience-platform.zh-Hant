---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 配置檔案系統作業API端點
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform可讓您從設定檔存放區刪除資料集或批次資料，以移除不再需要或錯誤新增的即時客戶設定檔資料。 這需要使用設定檔API來建立設定檔系統作業或刪除請求。
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 2%

---

# 配置檔案系統作業終結點（刪除請求）

Adobe Experience Platform可讓您內嵌來自多個來源的資料，並為個別客戶建立強大的設定檔。 內嵌至[!DNL Platform]的資料會儲存在[!DNL Data Lake]中，如果已為設定檔啟用資料集，該資料也會儲存在[!DNL Real-time Customer Profile]資料存放區中。 有時候，您可能需要從設定檔存放區刪除資料集或批次資料，才能移除不再需要或錯誤新增的資料。 這需要使用[!DNL Real-time Customer Profile] API來建立[!DNL Profile]系統作業或`delete request`，如有需要，也可以修改、監控或移除。

>[!NOTE]
>
>如果您嘗試從[!DNL Data Lake]中刪除資料集或批次，請訪問[目錄服務概述](../../catalog/home.md)以了解詳細資訊。

## 快速入門

本指南中使用的API端點是[[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 繼續之前，請檢閱[快速入門手冊](getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭的重要資訊。

## 檢視刪除請求

刪除請求是長時間執行的非同步程式，這表示您的組織可能同時執行多個刪除請求。 若要檢視您的組織目前執行的所有刪除請求，您可以對`/system/jobs`端點執行GET請求。

您也可以使用選用的查詢參數來篩選回應中傳回的刪除請求清單。 若要使用多個參數，請使用&amp;符號(`&`)將每個參數分隔開。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 根據請求的建立時間，傳回特定的結果頁面。 範例：`page=2` |
| `sort` | 按特定欄位的遞增(`asc`)或遞減(`desc`)順序排序結果。 傳回多個結果頁面時，排序參數無法運作。 範例：`sort=batchId:asc` |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含「子項」陣列，每個刪除請求都包含該請求的詳細資訊，且包含物件。

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| 屬性 | 說明 |
|---|---|
| `_page.count` | 請求總數。 此回應已因空間而截斷。 |
| `_page.next` | 如果有其他結果頁面存在，請將[查閱請求](#view-a-specific-delete-request)中的ID值取代為提供的`"next"`值，以檢視結果下一頁。 |
| `jobType` | 要建立的作業類型。 在這種情況下，它將始終返回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值為`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 一個物件，包含已處理的記錄數(`"recordsProcessed"`)、請求已處理的時間（以秒為單位），或請求完成所花的時間(`"timeTakenInSec"`)。 |

## 建立刪除請求 {#create-a-delete-request}

系統會透過向`/systems/jobs`端點提出POST請求，以起始新的刪除請求，請求內文中會提供要刪除的資料集或批次ID。

### 刪除資料集

若要從設定檔存放區刪除資料集，資料集ID必須包含在POST請求內文中。 此動作會刪除指定資料集的「全部」資料。 [!DNL Experience Platform] 可讓您根據記錄和時間系列結構來刪除資料集。

**API格式**

```http
POST /system/jobs
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 屬性 | 說明 |
|---|---|
| `dataSetId` | **（必要）** 您要刪除的資料集ID。 |

**回應**

成功的回應會傳回新建立之刪除請求的詳細資訊，包括請求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 建立時請求的`status`為`"NEW"`，直到開始處理為止。 回應中的`dataSetId`應符合要求中傳送的`dataSetId`。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 刪除請求的唯一、系統產生的唯讀ID。 |
| `dataSetId` | 資料集的ID，如POST請求中所指定。 |

### 刪除批

若要刪除批次，批次ID必須包含在POST請求的正文中。 請注意，您無法根據記錄結構刪除資料集的批次。 只能刪除根據時間系列結構的資料集批次。

>[!NOTE]
>
> 無法根據記錄結構刪除資料集的批是因為記錄類型資料集批覆蓋以前的記錄，因此無法「撤消」或刪除。 要根據記錄結構移除資料集錯誤批次的影響，唯一的方法是重新內嵌具有正確資料的批次，以覆寫錯誤的記錄。

有關記錄和時間序列行為的詳細資訊，請查看[!DNL XDM System]概述中有關XDM資料行為](../../xdm/home.md#data-behaviors)的[部分。

**API格式**

```http
POST /system/jobs
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 屬性 | 說明 |
|---|---|
| `batchId` | **（必要）** 您要刪除的批次ID。 |

**回應**

成功的回應會傳回新建立之刪除請求的詳細資訊，包括請求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 建立時請求的`"status"`為`"NEW"`，直到開始處理為止。 回應中的`"batchId"`值應符合要求中傳送的`"batchId"`值。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 刪除請求的唯一、系統產生的唯讀ID。 |
| `batchId` | 批的ID，如POST請求中指定。 |

如果您嘗試起始記錄資料集批次的刪除請求，將會遇到400層級的錯誤，如下所示：

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## 檢視特定刪除請求 {#view-a-specific-delete-request}

若要檢視特定刪除請求，包括其狀態等詳細資訊，您可以對`/system/jobs`端點執行查閱(GET)請求，並在路徑中包含刪除請求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必要）** 您要檢視的刪除請求ID。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應會提供刪除請求的詳細資訊，包括其更新狀態。 回應中刪除請求的ID（`"id"`值）應符合請求路徑中傳送的ID。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| 屬性 | 說明 |
|---|---|
| `jobType` | 要建立的作業類型，在這種情況下，它將始終返回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值：`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 一個陣列，包含已處理的記錄數(`"recordsProcessed"`)和請求已處理的時間（秒），或請求完成所花的時間(`"timeTakenInSec"`)。 |

一旦刪除請求狀態為`"COMPLETED"`，您就可以嘗試使用資料存取API存取已刪除的資料，以確認資料已刪除。 有關如何使用資料存取API來存取資料集和批次資料的說明，請參閱[資料存取檔案](../../data-access/home.md)。

## 移除刪除請求

[!DNL Experience Platform] 可讓您刪除先前的請求，這可能因多項原因而有用，包括刪除工作是否未完成或卡在處理階段。若要移除刪除請求，您可以對`/system/jobs`端點執行DELETE請求，並納入您要移除至請求路徑的刪除請求ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| {DELETE_REQUEST_ID} | 要刪除的刪除請求的ID。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200(OK)和空的回應內文。 您可以執行GET請求以依ID檢視刪除請求，以確認請求已刪除。 這應會傳回HTTP狀態404（找不到），指出刪除請求已移除。

## 後續步驟

現在您已了解從[!DNL Experience Platform]內的[!DNL Profile Store]刪除資料集和批次時所涉及的步驟，因此您可以安全地刪除已錯誤新增或貴組織不再需要的資料。 請留意刪除請求無法還原，因此您只應刪除您確信目前不需要且日後不需要的資料。
