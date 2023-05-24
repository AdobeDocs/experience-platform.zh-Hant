---
keywords: Experience Platform；首頁；熱門主題；批處理；批處理；接收；開發人員指南；api指南；上載；攝取Parket;ingest Parket;json;
solution: Experience Platform
title: 批量接收API指南
description: 本文檔為開發人員提供了一份全面的指南，這些開發人員使用針對Adobe Experience Platform的批量接收API。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 4%

---

# 批量攝取顯影劑指南

本文檔提供了使用的全面指南 [批處理接收API終結點](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 在Adobe Experience Platform。 有關批處理接收API的概述（包括先決條件和最佳實踐），請首先閱讀 [批處理接收API概述](overview.md)。

本文檔的附錄提供了 [格式化要用於攝取的資料](#data-transformation-for-batch-ingestion)，包括示例CSV和JSON資料檔案。

## 快速入門

本指南中使用的API端點是 [批處理接收API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)。 批處理是通過REST風格的API提供的，在該API中，您可以對支援的對象類型執行基本的CRUD操作。

在繼續之前，請查看 [批處理接收API概述](overview.md) 和 [入門指南](getting-started.md)。

## 正在接收JSON檔案

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更少）。 如果遇到網關超時或請求正文大小錯誤，則需要切換到大檔案上載。

### 建立批

首先，您需要建立以JSON為輸入格式的批。 建立批時，需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM架構。

>[!NOTE]
>
>以下示例用於單行JSON。 要接收多行JSON, `isMultiLineJson` 需要設定標誌。 有關詳細資訊，請閱讀 [批處理問題故障排除指南](./troubleshooting.md)。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用資料集的ID。 |

**回應**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |

### 上載檔案

現在您已建立了批，可以使用批建立響應中的批ID將檔案上載到批。 您可以將多個檔案上載到批。

>[!NOTE]
>
>請參閱附錄部分 [格式正確的JSON資料檔案示例](#data-transformation-for-batch-ingestion)。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要上載的檔案的名稱。 確保使用唯一的檔案名，以便它不會與正在提交的批檔案的其他檔案衝突。 |

**要求**

>[!NOTE]
>
>API支援單部件上載。 確保內容類型為application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上載的檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `acme/customers/campaigns/summer.json`。 |

**回應**

```http
200 OK
```

### 完成批

上載完檔案的所有不同部分後，您需要發出資料已完全上載且批已準備好進行升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## Ingest Parce檔案 {#ingest-parquet-files}

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更少）。 如果遇到網關超時或請求正文大小錯誤，則需要切換到大檔案上載。

### 建立批

首先，您需要建立一個批，其中輸入格式為Parce。 建立批時，需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM架構。

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| 參數 | 說明 |
| --------- | ------------ |
| `{DATASET_ID}` | 引用資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上載檔案

現在您已建立批，可以使用 `batchId` 將檔案上載到批。 您可以將多個檔案上載到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要上載的檔案的名稱。 確保使用唯一的檔案名，以便它不會與正在提交的批檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單部件上載。 確保內容類型為application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上載的檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `acme/customers/campaigns/summer.parquet`。 |

**回應**

```http
200 OK
```

### 完成批

上載完檔案的所有不同部分後，您需要發出資料已完全上載且批已準備好進行升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要發出信號的批的ID已準備好完成。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 攝取大型鑲木檔案

>[!NOTE]
>
>本部分詳細說明如何上載大於256 MB的檔案。 這些大檔案以塊形式上傳，然後通過API信號進行縫合。

### 建立批

首先，您需要建立一個批，其中輸入格式為Parce。 建立批時，需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM架構。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 初始化大檔案

建立批後，需要在將塊上載到批之前初始化大型檔案。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |
| `{FILE_NAME}` | 即將初始化的檔案的名稱。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
201 Created
```

### 上載大檔案塊

現在已建立檔案，可以通過重複的PATCH請求來上載所有後續的區塊，這對檔案的每個部分都是一個請求。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要上載的檔案的名稱。 確保使用唯一的檔案名，以便它不會與正在提交的批檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單部件上載。 確保內容類型為application/octet-stream。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 在整數中，請求範圍的開始和結束。 |
| `{FILE_PATH_AND_NAME}` | 您嘗試上載的檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `acme/customers/campaigns/summer.json`。 |


**回應**

```http
200 OK
```

### 完成大檔案

現在您已建立批，可以使用 `batchId` 將檔案上載到批。 您可以將多個檔案上載到批。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要指示完成的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要指示完成的檔案的名稱。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
201 Created
```

### 完成批

上載完檔案的所有不同部分後，您需要發出資料已完全上載且批已準備好進行升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要發出信號的批的ID已完成。 |


**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 正在接收CSV檔案

要接收CSV檔案，您需要建立一個支援CSV的類、模式和資料集。 有關如何建立必要類和架構的詳細資訊，請按照中提供的說明進行操作 [即席模式建立教程](../../xdm/api/ad-hoc.md)。

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更少）。 如果遇到網關超時或請求正文大小錯誤，則需要切換到大檔案上載。

### 建立資料集

按照上述說明建立必要的類和模式後，您需要建立可支援CSV的資料集。

**API格式**

```http
POST /catalog/dataSets
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TENANT_ID}` | 此ID用於確保您建立的資源與組織中的資源同名並包含在組織中。 |
| `{SCHEMA_ID}` | 已建立架構的ID。 |

### 建立批

接下來，您需要建立一個以CSV為輸入格式的批。 建立批時，需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到提供資料集的架構。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上載檔案

現在您已建立批，可以使用 `batchId` 將檔案上載到批。 您可以將多個檔案上載到批。

>[!NOTE]
>
>請參閱附錄部分 [格式正確的CSV資料檔案示例](#data-transformation-for-batch-ingestion)。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要上載的檔案的名稱。 確保使用唯一的檔案名，以便它不會與正在提交的批檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單部件上載。 確保內容類型為application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上載的檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `acme/customers/campaigns/summer.csv`。 |


**回應**

```http
200 OK
```

### 完成批

上載完檔案的所有不同部分後，您需要發出資料已完全上載且批已準備好進行升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## 取消批

在處理批時，仍可取消批。 但是，一旦批完成（如成功或失敗狀態），則無法取消該批。

**API格式**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要取消的批的ID。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 刪除批 {#delete-a-batch}

可通過以下POST請求刪除批 `action=REVERT` 查詢要刪除的批的ID的參數。 批標籤為「非活動」，使其符合垃圾收集的條件。 將非同步收集批，此時將標籤為「已刪除」。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要刪除的批的ID。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 修補批

有時可能需要更新組織的配置檔案儲存中的資料。 例如，您可能需要更正記錄或更改屬性值。 Adobe Experience Platform支援通過upsert操作或「修補批」更新或修補Profile Store資料。

>[!NOTE]
>
>這些更新僅允許在配置檔案記錄上，而不允許在體驗事件上。

為修補批處理，需要執行以下操作：

- **為配置檔案和屬性更新啟用的資料集。** 這是通過資料集標籤完成的，並且需要 `isUpsert:true` 將標籤添加到 `unifiedProfile` 陣列。 有關顯示如何建立資料集或配置用於upsert的現有資料集的詳細資訊步驟，請按照本教程瞭解 [啟用資料集以進行配置檔案更新](../../catalog/datasets/enable-upsert.md)。
- **包含要修補的欄位和配置檔案的標識欄位的Parfece檔案。** 用於修補批處理的資料格式與常規批處理接收過程類似。 所需的輸入是Parce檔案，除了要更新的欄位外，上載的資料必須包含標識欄位，以便與配置檔案儲存中的資料匹配。

在為配置檔案和upsert啟用了資料集，並且包含要修補的欄位和必需標識欄位的Parce檔案後，您可以按照 [正在插入鑲木地板檔案](#ingest-parquet-files) 以便通過批量攝取完成修補程式。

## 重播批

如果要替換已攝取的批，可以使用「批重播」進行替換 — 此操作等效於刪除舊批和插入新批。

### 建立批

首先，您需要建立以JSON為輸入格式的批。 建立批時，需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM架構。 此外，您還需要在重放部分中提供舊批作為參考。 在以下示例中，您正在重放具有ID的批 `batchIdA` 和 `batchIdB`。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| 參數 | 說明 |
| --------- | ----------- | 
| `{DATASET_ID}` | 引用資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 引用的資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |


### 上載檔案

現在您已建立批，可以使用 `batchId` 將檔案上載到批。 您可以將多個檔案上載到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上載到的批的ID。 |
| `{DATASET_ID}` | 批的引用資料集的ID。 |
| `{FILE_NAME}` | 要上載的檔案的名稱。 確保使用唯一的檔案名，以便它不會與正在提交的批檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單部件上載。 確保內容類型為application/octet-stream。 請勿使用curl -F選項，因為它預設為與API不相容的多部分請求。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上載的檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `acme/customers/campaigns/summer.json`。 |

**回應**

```http
200 OK
```

### 完成批

上載完檔案的所有不同部分後，您需要發出資料已完全上載且批已準備好進行升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要完成的批的ID。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## 附錄

以下部分包含使用批處理接收在Experience Platform中接收資料的附加資訊。

### 用於批量攝取的資料轉換

為了將資料檔案 [!DNL Experience Platform]，檔案的層次結構必須符合 [體驗資料模型(XDM)](../../xdm/home.md) 與要上載到的資料集關聯的架構。

有關如何映射CSV檔案以符合XDM架構的資訊，請參見 [樣本變換](../../etl/transformations.md) 文檔，以及格式正確的JSON資料檔案的示例。 文檔中提供的示例檔案可在以下位置找到：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
