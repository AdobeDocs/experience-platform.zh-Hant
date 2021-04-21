---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 配置檔案系統作業API端點
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform可讓您從描述檔商店刪除資料集或批次，以移除不再需要或錯誤新增的即時客戶描述檔資料。 這需要使用描述檔API來建立描述檔系統工作或刪除請求。
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 2%

---

# 描述系統作業端點（刪除請求）

Adobe Experience Platform可讓您從多個來源擷取資料，並為個別客戶建立強穩的個人檔案。 收錄到[!DNL Platform]的資料會儲存在[!DNL Data Lake]中，如果資料集已啟用描述檔，該資料也會儲存在[!DNL Real-time Customer Profile]資料儲存中。 有時可能需要從描述檔存放區刪除資料集或批次，以移除不再需要或錯誤新增的資料。 這需要使用[!DNL Real-time Customer Profile] API來建立[!DNL Profile]系統工作，或`delete request`，如有需要，也可加以修改、監視或移除。

>[!NOTE]
>
>如果您嘗試從[!DNL Data Lake]刪除資料集或批處理，請訪問[目錄服務概述](../../catalog/home.md)以瞭解詳細資訊。

## 快速入門

本指南中使用的API端點是[[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 檢視刪除請求

刪除請求是長時間執行的非同步程式，這表示您的組織可能同時執行多個刪除請求。 為了查看您的組織當前正在運行的所有刪除請求，可以對`/system/jobs`端點執行GET請求。

您也可以使用選用的查詢參數來篩選回應中傳回的刪除請求清單。 若要使用多個參數，請使用&amp;符號(`&`)分隔每個參數。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 依照請求的建立時間傳回特定的結果頁面。 範例：`page=2` |
| `sort` | 依特定欄位的遞增(`asc`)或遞減(`desc`)順序排序結果。 傳回多頁結果時，排序參數無法運作。 範例：`sort=batchId:asc` |

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

回應包含「子系」陣列，每個刪除請求都包含該請求的詳細資料的物件。

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
| `_page.count` | 請求總數。 此回應已針對空間截斷。 |
| `_page.next` | 如果存在另一頁結果，請將[查閱請求](#view-a-specific-delete-request)中的ID值取代為提供的`"next"`值，以檢視下一頁結果。 |
| `jobType` | 要建立的作業類型。 在這種情況下，它將始終返回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值有`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 包含已處理的記錄數(`"recordsProcessed"`)和請求已處理的時間（以秒為單位），或請求完成所花的時間(`"timeTakenInSec"`)的對象。 |

## 建立刪除請求{#create-a-delete-request}

啟始新刪除請求是透過對`/systems/jobs`端點的POST請求完成的，在此處，要刪除的資料集或批次的ID在請求正文中提供。

### 刪除資料集

若要從描述檔商店刪除資料集，資料集ID必須包含在POST請求的正文中。 此動作會刪除指定資料集的ALL資料。 [!DNL Experience Platform] 允許您根據記錄和時間序列模式刪除資料集。

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
| `dataSetId` | **（必要）** 您要刪除之資料集的ID。 |

**回應**

成功的回應會傳回新建立之刪除要求的詳細資料，包括要求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 建立時請求的`status`是`"NEW"`，直到開始處理為止。 回應中的`dataSetId`應符合在請求中傳送的`dataSetId`。

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

若要刪除批，批ID必須包含在POST請求的正文中。 請注意，不能根據記錄結構描述刪除資料集的批處理。 只能刪除基於時間系列方案的資料集的批處理。

>[!NOTE]
>
> 無法根據記錄結構描述刪除資料集的批的原因是，記錄類型資料集批會覆蓋以前的記錄，因此無法「撤消」或刪除。 要根據記錄方案消除資料集錯誤批處理的影響，唯一的方法是使用正確的資料重新收錄批，以覆蓋錯誤的記錄。

有關記錄和時間序列行為的詳細資訊，請參閱[!DNL XDM System]概述中有關XDM資料行為](../../xdm/home.md#data-behaviors)的[部分。

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
| `batchId` | **（必要）** 您要刪除之批次的ID。 |

**回應**

成功的回應會傳回新建立之刪除要求的詳細資料，包括要求的唯一、系統產生的唯讀ID。 這可用來查詢請求並檢查其狀態。 建立時請求的`"status"`是`"NEW"`，直到開始處理為止。 回應中的`"batchId"`值應與請求中傳送的`"batchId"`值相符。

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

如果您嘗試為記錄資料集批次啟動刪除請求，將會遇到400級錯誤，類似下列：

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

## 查看特定的刪除請求{#view-a-specific-delete-request}

若要檢視特定的刪除請求，包括詳細資訊（例如其狀態），您可以對`/system/jobs`端點執行查閱(GET)請求，並在路徑中包含刪除請求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必要）** 您要檢視之刪除請求的ID。 |

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

回應會提供刪除請求的詳細資訊，包括其更新狀態。 回應中刪除請求的ID（`"id"`值）應與請求路徑中傳送的ID相符。

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
| `jobType` | 所建立作業的類型，在此情況下，它將始終返回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值：`"NEW"`、`"PROCESSING"`、`"COMPLETED"`、`"ERROR"`。 |
| `metrics` | 一種陣列，包括已處理的記錄數(`"recordsProcessed"`)和請求已處理的時間（以秒為單位），或請求完成所需的時間(`"timeTakenInSec"`)。 |

刪除請求狀態為`"COMPLETED"`後，您可以嘗試使用「資料存取API」存取已刪除的資料，以確認資料已刪除。 有關如何使用Data Access API訪問資料集和批次的說明，請查看[資料存取文檔](../../data-access/home.md)。

## 刪除刪除請求

[!DNL Experience Platform] 可讓您刪除先前的請求，這可能因為許多原因（包括刪除作業未完成或在處理階段卡住）而有用。為了刪除刪除請求，您可以對`/system/jobs`端點執行DELETE請求，並包括要刪除到請求路徑的刪除請求的ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| {DELETE_請求_ID} | 您要移除的刪除請求ID。 |

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

成功的刪除請求會傳回HTTP狀態200（確定）和空回應主體。 您可以執行GET請求以依其ID檢視刪除請求，以確認刪除請求。 這應該會傳回HTTP狀態404（找不到），表示刪除請求已移除。

## 後續步驟

現在，您已瞭解從[!DNL Experience Platform]內的[!DNL Profile Store]刪除資料集和批次時涉及的步驟，因此您可以安全地刪除已錯誤添加或您的組織不再需要的資料。 請注意，刪除請求無法撤消，因此您只應刪除您確信現在不需要且將來不需要的資料。
