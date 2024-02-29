---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 設定檔系統作業API端點
type: Documentation
description: Adobe Experience Platform可讓您從設定檔存放區中刪除資料集或批次，以移除不再需要或錯誤新增的即時客戶設定檔資料。 這需要使用設定檔API來建立設定檔系統作業或刪除請求。
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 2%

---

# 設定檔系統作業端點（刪除請求）

Adobe Experience Platform可讓您從多個來源擷取資料，並為個別客戶建立強大的設定檔。 資料已擷取到 [!DNL Platform] 儲存在 [!DNL Data Lake]，而且如果資料集已啟用設定檔功能，該資料會儲存在 [!DNL Real-Time Customer Profile] 資料存放區。 有時候，您可能需要從設定檔存放區中刪除資料集或批次，以移除不再需要或新增錯誤的資料。 這需要使用 [!DNL Real-Time Customer Profile] 建立API [!DNL Profile] 系統工作，或 `delete request`，您也可以在需要時修改、監控或移除這些專案。

>[!NOTE]
>
>如果您嘗試刪除資料集或批次 [!DNL Data Lake]，請造訪 [目錄服務總覽](../../catalog/home.md) 以取得詳細資訊。

## 快速入門

本指南中使用的API端點屬於 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

## 檢視刪除請求

刪除請求是長期執行的非同步程式，這表示您的組織可能同時執行多個刪除請求。 GET若要檢視貴組織目前執行的所有刪除請求，您可以對 `/system/jobs` 端點。

您也可以使用選用的查詢引數，以篩選回應中傳回的刪除請求清單。 若要使用多個引數，請使用&amp;符號(`&`)。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `start` | 根據請求的建立時間，位移傳回結果的頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 根據請求的建立時間，傳回結果的特定頁面。 範例：`page=2` |
| `sort` | 依特定欄位遞增排序結果(`asc`)或降序(`desc`)順序。 傳回多個結果頁面時，排序引數無法運作。 範例：`sort=batchId:asc` |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應中包含「children」陣列，針對每個包含該請求詳細資訊的刪除請求而提供一個物件。

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
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
| `_page.count` | 要求總數。 此回應已因空間而遭截斷。 |
| `_page.next` | 如果存在其他結果頁面，請取代中的ID值來檢視結果的下一頁 [查詢請求](#view-a-specific-delete-request) 使用 `"next"` 提供的值。 |
| `jobType` | 正在建立的工作型別。 在此情況下，會一律傳回 `"DELETE"`. |
| `status` | 刪除請求的狀態。 可能的值包括 `"NEW"`， `"PROCESSING"`， `"COMPLETED"`， `"ERROR"`. |
| `metrics` | 包含已處理記錄數的物件(`"recordsProcessed"`)以及處理請求所需的時間（以秒為單位），或是完成請求所需的時間(`"timeTakenInSec"`)。 |

## 建立刪除請求 {#create-a-delete-request}

透過向發出的POST請求，可起始新的刪除請求 `/systems/jobs` 端點，要求內文中提供要刪除的資料集或批次的ID。

### 刪除資料集

若要從設定檔存放區中刪除資料集，資料集ID必須包含在POST請求內文中。 此動作將會刪除指定資料集的所有資料。 [!DNL Experience Platform] 可讓您根據記錄和時間序列結構描述刪除資料集。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| 屬性 | 說明 |
|---|---|
| `dataSetId` | **（必要）** 您要刪除的資料集ID。 |

**回應**

成功的回應會傳回新建立的刪除請求的詳細資料，包括請求的不重複、系統產生的唯讀ID。 這可用來查閱請求並檢查其狀態。 此 `status` 對於建立時的請求，為 `"NEW"` 直到開始處理為止。 此 `dataSetId` 在回應中應符合 `dataSetId` 已在要求中傳送。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 系統產生的唯一刪除請求唯讀ID。 |
| `dataSetId` | 資料集的ID，如POST請求中所指定。 |

### 刪除批次

為了刪除批次，批次ID必須包含在POST請求正文中。 請注意，您無法刪除以記錄結構描述為基礎的資料集批次。 只能刪除以時間序列結構描述為基礎的資料集批次。

>[!NOTE]
>
> 您無法刪除根據記錄結構描述之資料集的批次，因為記錄型別資料集批次會覆寫先前的記錄，因此無法「復原」或刪除。 根據記錄結構描述移除資料集錯誤批次影響的唯一方法是，使用正確的資料重新內嵌批次，以覆寫不正確的記錄。

如需有關記錄和時間序列行為的詳細資訊，請查閱 [有關XDM資料行為的區段](../../xdm/home.md#data-behaviors) 在 [!DNL XDM System] 概述。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| 屬性 | 說明 |
|---|---|
| `batchId` | **（必要）** 您要刪除之批次的ID。 |

**回應**

成功的回應會傳回新建立的刪除請求的詳細資料，包括請求的不重複、系統產生的唯讀ID。 這可用來查閱請求並檢查其狀態。 此 `"status"` 對於建立時的請求，為 `"NEW"` 直到開始處理為止。 此 `"batchId"` 回應中的值應符合 `"batchId"` 請求中傳送的值。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 屬性 | 說明 |
|---|---|
| `id` | 系統產生的唯一刪除請求唯讀ID。 |
| `batchId` | 批次的ID，如POST請求中所指定。 |

如果您嘗試起始記錄資料集批次的刪除請求，您將會遇到400層級的錯誤，類似以下情況：

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

## 檢視特定的刪除請求 {#view-a-specific-delete-request}

若要檢視特定刪除請求（包括其狀態等詳細資訊），您可以對執行查詢(GET)請求 `/system/jobs` 端點並在路徑中包含刪除請求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必要）** 您要檢視之刪除請求的ID。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應會提供刪除請求的詳細資訊，包括其更新狀態。 回應中刪除請求的ID (回應中的 `"id"` 值)應與請求路徑中傳送的ID相符。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
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
| `jobType` | 正在建立的工作型別，在此情況下，一律會傳回 `"DELETE"`. |
| `status` | 刪除請求的狀態。 可能的值： `"NEW"`， `"PROCESSING"`， `"COMPLETED"`， `"ERROR"`. |
| `metrics` | 包含已處理記錄數的陣列(`"recordsProcessed"`)以及處理請求所需的時間（以秒為單位），或是完成請求所需的時間(`"timeTakenInSec"`)。 |

一旦刪除請求狀態為 `"COMPLETED"` 您可以透過嘗試使用資料存取API存取已刪除的資料來確認資料已刪除。 如需如何使用資料存取API存取資料集和批次的說明，請檢閱 [資料存取檔案](../../data-access/home.md).

## 移除刪除請求

[!DNL Experience Platform] 可讓您刪除先前的請求，這可能對許多原因很有用，包括刪除工作未完成或卡在處理階段。 DELETE若要移除刪除請求，您可以對 `/system/jobs` 端點，並包含您要移除至請求路徑的刪除請求ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| {DELETE_REQUEST_ID} | 您要移除之刪除請求的ID。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的刪除請求會傳回HTTP狀態200 （確定）和空白的回應內文。 您可以透過執行GET請求來確認請求已刪除，以按其ID檢視刪除請求。 這會傳回HTTP狀態404 （找不到），指出刪除請求已移除。

## 後續步驟

現在您已經知道從刪除資料集和批次的步驟 [!DNL Profile Store] 範圍 [!DNL Experience Platform]，您可以安全地刪除已錯誤新增或您的組織不再需要的資料。 請注意，刪除請求無法復原，因此您應該僅刪除確信現在不需要且未來不需要的資料。
