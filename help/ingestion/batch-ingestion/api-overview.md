---
keywords: Experience Platform；首頁；熱門主題；批次內嵌；批次內嵌；內嵌；開發人員指南；api指南；上傳；內嵌Parquet；內嵌json;
solution: Experience Platform
title: 批次內嵌API指南
description: 本檔案為開發人員提供使用適用於Adobe Experience Platform的批次擷取API的完整指南。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 087a714c579c4c3b95feac3d587ed13589b6a752
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 4%

---

# 批次內嵌開發人員指南

本檔案提供在Adobe Experience Platform中使用[批次擷取API端點](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion)的完整指南。 如需批次擷取API的概觀，包括必要條件和最佳實務，請從閱讀[批次擷取API概觀](overview.md)開始。

本檔案附錄提供用於擷取](#data-transformation-for-batch-ingestion)之[格式化資料的資訊，包括範例CSV和JSON資料檔案。

## 快速入門

本指南中使用的API端點屬於[資料擷取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)的一部分。 資料擷取提供RESTful API，您可透過此API對支援的物件類型執行基本CRUD作業。

繼續操作之前，請查看[批次擷取API概述](overview.md)和[快速入門手冊](getting-started.md)。

## 內嵌JSON檔案

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更小）。 如果您遇到閘道逾時或要求內文大小錯誤，則需切換至大型檔案上傳。

### 建立批次

首先，您需要建立以JSON為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您也需要確定，隨著批次上傳的所有檔案，都符合連結至所提供資料集的XDM架構。

>[!NOTE]
>
>以下範例適用於單行JSON。 若要內嵌多行JSON，需要設定`isMultiLineJson`標幟。 如需詳細資訊，請參閱[批次內嵌疑難排解指南](./troubleshooting.md)。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 參考資料集的ID。 |

**回應**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | 參考資料集的ID。 |

### 上傳檔案

現在您已建立批處理，可以使用批處理建立響應中的批處理ID將檔案上載到批處理。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>如需格式正確的JSON資料檔案](#data-transformation-for-batch-ingestion)範例，請參閱附錄一節。[

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案在Adobe端儲存的位置。 |

**要求**

>[!NOTE]
>
>API支援單一部分上傳。 請確定content-type為application/oct-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |

**回應**

```http
200 OK
```

### 完成批

上傳完檔案的所有不同部分後，您需要發出信號，指出資料已完全上傳，且批次已準備好升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## 內嵌鑲木檔案 {#ingest-parquet-files}

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更小）。 如果您遇到閘道逾時或要求內文大小錯誤，則需切換至大型檔案上傳。

### 建立批次

首先，您需要建立以Parquet為輸入格式的批。 建立批次時，您需要提供資料集ID。 您也需要確定，隨著批次上傳的所有檔案，都符合連結至所提供資料集的XDM架構。

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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
| `{DATASET_ID}` | 參考資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上傳檔案

現在您已建立批處理，可以使用之前的`batchId`將檔案上載到該批處理。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案在Adobe端儲存的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定content-type為application/oct-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |

**回應**

```http
200 OK
```

### 完成批

上傳完檔案的所有不同部分後，您需要發出信號，指出資料已完全上傳，且批次已準備好升級。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 內嵌大型鑲木檔案

>[!NOTE]
>
>本節詳細說明如何上傳大於256 MB的檔案。 大型檔案會以區塊上傳，然後透過API訊號匯整。

### 建立批次

首先，您需要建立以Parquet為輸入格式的批。 建立批次時，您需要提供資料集ID。 您也需要確定，隨著批次上傳的所有檔案，都符合連結至所提供資料集的XDM架構。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 參考資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 初始化大檔案

建立批次後，您必須先初始化大型檔案，才能將區塊上傳至批次。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立的批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{FILE_NAME}` | 即將初始化的檔案的名稱。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
201 Created
```

### 上傳大型檔案區塊

現在檔案已建立完畢，您可以透過重複的PATCH要求來上傳所有後續區塊，檔案的每個區段各一個。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案在Adobe端儲存的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定content-type為application/oct-stream。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 在整數中，請求範圍的開頭和結尾。 |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |


**回應**

```http
200 OK
```

### 完整大檔案

現在您已建立批處理，可以使用之前的`batchId`將檔案上載到該批處理。 您可以上傳多個檔案至批次。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要指示完成的批的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 要指示完成的檔案的名稱。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
201 Created
```

### 完成批

上傳完檔案的所有不同部分後，您需要發出信號，指出資料已完全上傳，且批次已準備好升級。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 內嵌CSV檔案

若要內嵌CSV檔案，您需要建立支援CSV的類別、結構和資料集。 有關如何建立必要類和架構的詳細資訊，請按照[ad-hoc架構建立教程](../../xdm/api/ad-hoc.md)中提供的說明操作。

>[!NOTE]
>
>以下步驟適用於小檔案（256 MB或更小）。 如果您遇到閘道逾時或要求內文大小錯誤，則需切換至大型檔案上傳。

### 建立資料集

依照上述指示建立必要的類別和結構後，您將需要建立可支援CSV的資料集。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{TENANT_ID}` | 此ID可確保您建立的資源與IMS組織中的資源命名正確，且完整無缺。 |
| `{SCHEMA_ID}` | 您建立的架構ID。 |

### 建立批次

接下來，您需要建立以CSV為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您也必須確保隨批次上傳的所有檔案都符合連結至所提供資料集的結構。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 參考資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上傳檔案

現在您已建立批處理，可以使用之前的`batchId`將檔案上載到該批處理。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>請參閱附錄中的[格式正確的CSV資料檔案範例](#data-transformation-for-batch-ingestion)一節。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案在Adobe端儲存的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定content-type為application/oct-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |


**回應**

```http
200 OK
```

### 完成批

上傳完檔案的所有不同部分後，您需要發出資料已完全上傳，且批次已準備好升級的信號。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## 取消批

在處理批時，仍可取消該批。 但是，一旦批完成（如成功或失敗狀態），則無法取消該批。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 刪除批 {#delete-a-batch}

可以刪除批，方法是使用`action=REVERT`查詢參數執行以下POST請求，該參數為要刪除的批的ID。 該批被標籤為「非活動」，因此符合垃圾收集資格。 系統會以非同步方式收集批次，並在該時間將其標示為「已刪除」。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

```http
200 OK
```

## 修補批次

有時候，您可能需要更新組織的設定檔存放區中的資料。 例如，您可能需要更正記錄或更改屬性值。 Adobe Experience Platform支援透過更新動作或「修補批次」來更新或修補設定檔存放區資料。

>[!NOTE]
>
>只允許設定檔記錄進行這些更新，不允許體驗事件。

要修補批處理，需要以下操作：

- **啟用設定檔和屬性更新的資料集。** 這需透過資料集標籤完成，且需要將 `isUpsert:true` 特定標籤新增至 `unifiedProfile` 陣列。如需如何建立資料集或設定現有資料集以供上傳的詳細步驟，請依照[啟用資料集以進行設定檔更新](../../catalog/datasets/enable-upsert.md)的教學課程進行。
- **包含要修補的欄位和配置檔案標識欄位的Parquet檔案。** 用於修補批的資料格式與常規批處理獲取過程類似。所需的輸入為Parquet檔案，除了要更新的欄位外，上傳的資料還必須包含身分欄位，才能符合設定檔存放區中的資料。

在為「配置檔案」和「上插」啟用資料集，並且包含要修補的欄位和必要標識欄位的Parquet檔案後，您可以按照[內嵌Parquet檔案](#ingest-parquet-files)的步驟操作，通過批次內嵌完成修補。

## 重播批

如果要替換已導入的批，可以使用「批重播」來替換，此操作相當於刪除舊批，並改為導入新批。

### 建立批次

首先，您需要建立以JSON為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您也需要確定，隨著批次上傳的所有檔案，都符合連結至所提供資料集的XDM架構。 此外，您還需要提供舊批次作為重播部分中的參考。 在以下示例中，您正在重播ID為`batchIdA`和`batchIdB`的批。

**API格式**

```http
POST /batches
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{DATASET_ID}` | 參考資料集的ID。 |

**回應**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
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
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |


### 上傳檔案

現在您已建立批處理，可以使用之前的`batchId`將檔案上載到該批處理。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案在Adobe端儲存的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定content-type為application/oct-stream。 請勿使用curl -F選項，因為它預設為與API不相容的多部分請求。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |

**回應**

```http
200 OK
```

### 完成批

上傳完檔案的所有不同部分後，您需要發出信號，指出資料已完全上傳，且批次已準備好升級。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```http
200 OK
```

## 附錄

以下章節包含使用批次內嵌在Experience Platform中擷取資料的其他資訊。

### 批次內嵌的資料轉換

若要將資料檔案內嵌至[!DNL Experience Platform]，檔案的階層結構必須符合與上傳至之資料集相關聯的[Experience Data Model(XDM)](../../xdm/home.md)架構。

有關如何對應CSV檔案以符合XDM架構的資訊，請參閱[範例轉換](../../etl/transformations.md)檔案，以及格式正確的JSON資料檔案範例。 可在以下位置找到文檔中提供的示例檔案：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
