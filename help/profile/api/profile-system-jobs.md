---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 配置檔案系統作業API終結點
type: Documentation
description: Adobe Experience Platform允許您從配置檔案儲存中刪除資料集或批處理，以刪除不再需要或錯誤添加的即時客戶配置檔案資料。 這要求使用配置檔案API建立配置檔案系統作業或刪除請求。
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 2%

---

# 配置系統作業終結點（刪除請求）

Adobe Experience Platform使您能夠從多個源中接收資料，並為單個客戶構建強健的配置檔案。 已接收到的資料 [!DNL Platform] 儲存在 [!DNL Data Lake]，如果已為Profile啟用資料集，則該資料儲存在 [!DNL Real-Time Customer Profile] 資料儲存。 有時可能需要從配置檔案儲存中刪除資料集或批處理，以刪除不再需要或錯誤添加的資料。 這要求使用 [!DNL Real-Time Customer Profile] 用於建立 [!DNL Profile] 系統作業，或 `delete request`，如果需要，也可以修改、監視或刪除。

>[!NOTE]
>
>如果嘗試從 [!DNL Data Lake]，請訪問 [目錄服務概述](../../catalog/home.md) 的子菜單。

## 快速入門

本指南中使用的API終結點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 查看刪除請求

刪除請求是一個長時間運行的非同步進程，這意味著您的組織可能同時運行多個刪除請求。 為了查看您的組織當前正在運行的所有刪除請求，您可以對 `/system/jobs` 端點。

您也可以使用可選的查詢參數篩選在響應中返回的刪除請求清單。 要使用多個參數，請使用「和號」(ampersand)分隔每個參數(`&`)。

**API格式**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `start` | 按請求的建立時間偏移返回的結果頁。 範例：`start=4` |
| `limit` | 限制返回的結果數。 範例：`limit=10` |
| `page` | 按照請求的建立時間返回特定結果頁。 範例：`page=2` |
| `sort` | 按特定欄位按升序對結果排序(`asc`)或降序(`desc`)順序。 返回多頁結果時，排序參數不起作用。 範例：`sort=batchId:asc` |

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

響應包括「子」陣列，每個刪除請求都包含該請求的詳細資訊，該陣列具有對象。

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
| `_page.count` | 請求總數。 此響應已被截斷為空間。 |
| `_page.next` | 如果存在其他結果頁，請通過替換 [查找請求](#view-a-specific-delete-request) 和 `"next"` 值。 |
| `jobType` | 正在建立的作業的類型。 在這種情況下，它總會 `"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值為 `"NEW"`。 `"PROCESSING"`。 `"COMPLETED"`。 `"ERROR"`。 |
| `metrics` | 包含已處理記錄數(`"recordsProcessed"`)和請求已處理的時間（以秒為單位），或請求完成所花的時間(`"timeTakenInSec"`)。 |

## 建立刪除請求 {#create-a-delete-request}

啟動新的刪除請求是通過POST請求 `/systems/jobs` 端點，其中在請求正文中提供要刪除的資料集或批的ID。

### 刪除資料集

為了從配置檔案儲存中刪除資料集，必須將資料集ID包括在POST請求的正文中。 此操作將刪除給定資料集的ALL資料。 [!DNL Experience Platform] 允許您基於記錄和時間系列架構刪除資料集。

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
| `dataSetId` | **（必需）** 要刪除的資料集的ID。 |

**回應**

成功的響應返回新建立的刪除請求的詳細資訊，包括該請求的唯一、系統生成的只讀ID。 這可用於查找請求並檢查其狀態。 的 `status` 在建立時請求 `"NEW"` 直到它開始處理。 的 `dataSetId` 在響應中應與 `dataSetId` 寄來的。

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
| `id` | 刪除請求的唯一、系統生成的只讀ID。 |
| `dataSetId` | 資料集的ID，如POST請求中指定。 |

### 刪除批

要刪除批，批ID必須包含在POST請求的正文中。 請注意，不能基於記錄架構刪除資料集的批處理。 只能刪除基於時間序列模式的資料集的批。

>[!NOTE]
>
> 無法基於記錄架構刪除資料集的批的原因是記錄類型資料集批覆蓋以前的記錄，因此無法「撤消」或刪除。 要消除基於記錄架構的資料集的錯誤批處理的影響，唯一的方法是用正確的資料重新接收批處理，以覆蓋錯誤的記錄。

有關記錄和時間序列行為的詳細資訊，請查看 [關於XDM資料行為的部分](../../xdm/home.md#data-behaviors) 的 [!DNL XDM System] 概述。

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
| `batchId` | **（必需）** 要刪除的批的ID。 |

**回應**

成功的響應返回新建立的刪除請求的詳細資訊，包括該請求的唯一、系統生成的只讀ID。 這可用於查找請求並檢查其狀態。 的 `"status"` 在建立時請求 `"NEW"` 直到它開始處理。 的 `"batchId"` 響應中的值應與 `"batchId"` 在請求中發送的值。

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
| `id` | 刪除請求的唯一、系統生成的只讀ID。 |
| `batchId` | 批的ID，如POST請求中指定。 |

如果嘗試為記錄資料集批啟動刪除請求，將遇到400級錯誤，類似於以下內容：

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

## 查看特定刪除請求 {#view-a-specific-delete-request}

要查看特定的刪除請求，包括詳細資訊（如其狀態），您可以對 `/system/jobs` 端點，並在路徑中包含刪除請求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| `{DELETE_REQUEST_ID}` | **（必需）** 要查看的刪除請求的ID。 |

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

響應提供刪除請求的詳細資訊，包括其更新狀態。 響應中刪除請求的ID( `"id"` 值)應與請求路徑中發送的ID匹配。

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
| `jobType` | 正在建立的作業的類型，在這種情況下，它將始終返回 `"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值： `"NEW"`。 `"PROCESSING"`。 `"COMPLETED"`。 `"ERROR"`。 |
| `metrics` | 包含已處理記錄數(`"recordsProcessed"`)和請求已處理的時間（以秒為單位），或請求完成所花的時間(`"timeTakenInSec"`)。 |

一旦刪除請求狀態為 `"COMPLETED"` 您可以通過嘗試使用資料存取API訪問已刪除的資料來確認資料已被刪除。 有關如何使用資料存取API訪問資料集和批處理的說明，請查看 [資料存取文檔](../../data-access/home.md)。

## 刪除刪除請求

[!DNL Experience Platform] 允許您刪除以前的請求，這可能有多種原因，包括刪除作業未完成或在處理階段被卡住。 為了刪除刪除請求，您可以對 `/system/jobs` 端點，並包括要刪除到請求路徑的刪除請求的ID。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
|---|---|
| {DELETE_請求_ID} | 要刪除的刪除請求的ID。 |

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

成功的刪除請求返回HTTP狀態200(OK)和空響應正文。 通過執行GET請求以按刪除請求的ID查看刪除請求，可以確認該請求已被刪除。 這應返回HTTP狀態404（未找到），表示刪除請求已被刪除。

## 後續步驟

現在，您已知道從中刪除資料集和批處理涉及的步驟 [!DNL Profile Store] 內 [!DNL Experience Platform]，您可以安全地刪除錯誤添加或您的組織不再需要的資料。 請注意，刪除請求無法撤消，因此您只應刪除您確信現在不需要並且將來不需要的資料。
