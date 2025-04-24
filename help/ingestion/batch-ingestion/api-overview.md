---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；開發人員指南；api指南；上傳；擷取Parquet；擷取json；
solution: Experience Platform
title: 批次擷取API指南
description: 本檔案為使用Adobe Experience Platform批次擷取API的開發人員提供完整指南。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '2435'
ht-degree: 4%

---

# 批次內嵌開發人員指南

本檔案提供在Adobe Experience Platform中使用[批次擷取API端點](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)的完整指南。 如需批次擷取API的概觀，包括必要條件和最佳實務，請先閱讀[批次擷取API概觀](overview.md)。

本檔案的附錄提供[格式化要用於內嵌](#data-transformation-for-batch-ingestion)的資料的資訊，包括範例CSV和JSON資料檔案。

## 快速入門

本指南中使用的API端點是[批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)的一部分。 批次內嵌是透過RESTful API提供，您可在此針對支援的物件型別執行基本CRUD作業。

在繼續之前，請檢閱[批次擷取API總覽](overview.md)和[快速入門手冊](getting-started.md)。

## 擷取JSON檔案

>[!NOTE]
>
>- 下列步驟適用於小型檔案（256 MB或更小）。 如果您遇到閘道逾時或請求內文大小錯誤，您必須切換到大型檔案上傳。
>
>- 使用單行JSON而非多行JSON作為批次擷取的輸入。 單行JSON可提供較佳的效能，因為系統可以將一個輸入檔案分割成多個區塊並平行處理，而多行JSON無法分割。 這可以大幅降低資料處理成本並改善批次處理延遲。

### 建立批次

首先，您需要建立批次，以JSON作為輸入格式。 建立批次時，您需要提供資料集ID。 您也必須確保批次中上傳的所有檔案都符合連結至所提供資料集的XDM結構。

>[!NOTE]
>
>以下範例適用於單行JSON。 若要內嵌多行JSON，需要設定`isMultiLineJson`標幟。 如需詳細資訊，請參閱[批次擷取疑難排解指南](./troubleshooting.md)。

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
| `{DATASET_ID}` | 參考資料集的ID。 |

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
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |

### 上傳檔案

現在您已建立批次，可以使用批次建立回應中的批次ID將檔案上傳到批次。 您可以將多個檔案上傳到批次中。

>[!NOTE]
>
>請參閱附錄一節，以取得正確格式化的JSON資料檔](#data-transformation-for-batch-ingestion)的[範例。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 請確定您使用唯一的檔案名稱，這樣它就不會與要提交之批次檔案的其他檔案衝突。 |

**要求**

>[!NOTE]
>
>API支援單一部分上傳。 確保內容型別是application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本機檔案路徑，例如`acme/customers/campaigns/summer.json`。 |

**回應**

```http
200 OK
```

### 完成批次

上傳完檔案的所有不同部分後，您需要指出資料已完全上傳，且批次已準備好進行升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |

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

## 擷取Parquet檔案 {#ingest-parquet-files}

>[!NOTE]
>
>下列步驟適用於小型檔案（256 MB或更小）。 如果您遇到閘道逾時或請求內文大小錯誤，您將需要切換到大型檔案上傳。

### 建立批次

首先，您需要建立批次，以Parquet作為輸入格式。 建立批次時，您需要提供資料集ID。 您也必須確保批次中上傳的所有檔案都符合連結至所提供資料集的XDM結構。

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
| `{DATASET_ID}` | 參考資料集的ID。 |

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
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批次的使用者ID。 |

### 上傳檔案

現在您已建立批次，可以使用之前的`batchId`將檔案上傳到批次。 您可以將多個檔案上傳到批次中。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 請確定您使用唯一的檔案名稱，這樣它就不會與要提交之批次檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 確保內容型別是application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本機檔案路徑，例如`acme/customers/campaigns/summer.parquet`。 |

**回應**

```http
200 OK
```

### 完成批次

上傳完檔案的所有不同部分後，您需要指出資料已完全上傳，且批次已準備好進行升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要訊號之批次的ID已準備好完成。 |

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

## 擷取大型Parquet檔案

>[!NOTE]
>
>本節詳細說明如何上傳大於256 MB的檔案。 大型檔案會以區塊上傳，然後透過API訊號拼接。

### 建立批次

首先，您需要建立批次，以Parquet作為輸入格式。 建立批次時，您需要提供資料集ID。 您也必須確保批次中上傳的所有檔案都符合連結至所提供資料集的XDM結構。

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
| `{DATASET_ID}` | 參考資料集的ID。 |

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
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批次的使用者ID。 |

### 初始化大型檔案

建立批次後，您必須先初始化大型檔案，才能將區塊上傳至批次。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{FILE_NAME}` | 即將初始化的檔案名稱。 |

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

### 上傳大型檔案區塊

現在檔案已建立，您可以進行重複的PATCH請求（檔案的每個區段各一個），上傳所有後續的區塊。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 請確定您使用唯一的檔案名稱，這樣它就不會與要提交之批次檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 確保內容型別是application/octet-stream。

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
| `{CONTENT_RANGE}` | 以整數表示請求範圍的開始和結束。 |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本機檔案路徑，例如`acme/customers/campaigns/summer.json`。 |


**回應**

```http
200 OK
```

### 完成大型檔案

現在您已建立批次，可以使用之前的`batchId`將檔案上傳到批次。 您可以將多個檔案上傳到批次中。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要表示完成的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 要表示完成的檔案名稱。 |

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

### 完成批次

上傳完檔案的所有不同部分後，您需要指出資料已完全上傳，且批次已準備好進行升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要訊號為完成的批次ID。 |


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

## 擷取CSV檔案

若要內嵌CSV檔案，您需要建立支援CSV的類別、結構描述和資料集。 如需有關如何建立必要類別和結構描述的詳細資訊，請依照[臨機結構描述建立教學課程](../../xdm/api/ad-hoc.md)中提供的指示操作。

>[!NOTE]
>
>下列步驟適用於小型檔案（256 MB或更小）。 如果您遇到閘道逾時或請求內文大小錯誤，您將需要切換到大型檔案上傳。

### 建立資料集

依照上述指示建立必要的類別和結構描述後，您需要建立可支援CSV的資料集。

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
| `{TENANT_ID}` | 此ID可用來確保您建立的資源能正確進行名稱空間，並包含在您的組織內。 |
| `{SCHEMA_ID}` | 您已建立的結構描述ID。 |

### 建立批次

接下來，您需要以CSV作為輸入格式建立批次。 建立批次時，您需要提供資料集ID。 您也必須確保批次中上傳的所有檔案都與連結至所提供資料集的結構描述相符。

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
| `{DATASET_ID}` | 參考資料集的ID。 |

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
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批次的使用者ID。 |

### 上傳檔案

現在您已建立批次，可以使用之前的`batchId`將檔案上傳到批次。 您可以將多個檔案上傳到批次中。

>[!NOTE]
>
>請參閱附錄一節，以取得[正確格式化的CSV資料檔範例](#data-transformation-for-batch-ingestion)。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 請確定您使用唯一的檔案名稱，這樣它就不會與要提交之批次檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 確保內容型別是application/octet-stream。

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本機檔案路徑，例如`acme/customers/campaigns/summer.csv`。 |


**回應**

```http
200 OK
```

### 完成批次

上傳完檔案的所有不同部分後，您需要指出資料已完全上傳，且批次已準備好進行升級。

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

## 取消批次

批次處理期間，仍可取消。 不過，一旦批次完成（例如成功或失敗狀態），就無法取消批次。

**API格式**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要取消的批次識別碼。 |

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

## 刪除批次 {#delete-a-batch}

若要刪除批次，請對要刪除之批次的ID使用下列POST要求`action=REVERT`查詢引數。 該批次被標籤為「非使用中」，因此符合記憶體回收的資格。 系統會以非同步方式收集批次，然後將收集到的批次標示為「已刪除」。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要刪除之批次的ID。 |

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

## 修補批次

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 Adobe Experience Platform支援透過更新插入動作或「修補批次」來更新或修補設定檔存放區資料。

>[!NOTE]
>
>這些更新僅允許在設定檔記錄上進行，不允許在體驗事件上進行。

若要修補批次，需要下列專案：

- **已啟用設定檔和屬性更新的資料集。**&#x200B;這是透過資料集標籤完成的，並需要將特定的`isUpsert:true`標籤新增到`unifiedProfile`陣列。 如需詳細步驟，說明如何建立資料集或設定現有資料集以進行更新插入，請遵循[啟用資料集以進行設定檔更新的教學課程](../../catalog/datasets/enable-upsert.md)。
- **包含要修補的欄位和設定檔識別欄位的Parquet檔案。**&#x200B;修補批次的資料格式與一般批次擷取程式類似。 需要的輸入是Parquet檔案，除了要更新的欄位之外，上傳的資料必須包含身分欄位，以便與設定檔存放區中的資料相符。

一旦您啟用了設定檔和upsert的資料集，以及包含您要修補的欄位以及必要的身分欄位的Parquet檔案，您可以依照[擷取Parquet檔案](#ingest-parquet-files)的步驟，透過批次擷取完成修補。

## 重播批次

如果您想要取代已擷取的批次，可以使用「批次重播」來執行此操作，此動作等同於刪除舊批次並擷取新批次。

### 建立批次

首先，您需要建立批次，以JSON作為輸入格式。 建立批次時，您需要提供資料集ID。 您也必須確保批次中上傳的所有檔案都符合連結至所提供資料集的XDM結構。 此外，您還需要在重播區段中提供舊批次作為參考。 在下列範例中，您正在重播識別碼為`batchIdA`和`batchIdB`的批次。

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
| `{DATASET_ID}` | 參考資料集的ID。 |

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
| `{BATCH_ID}` | 新建立批次的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批次的使用者ID。 |


### 上傳檔案

現在您已建立批次，可以使用之前的`batchId`將檔案上傳到批次。 您可以將多個檔案上傳到批次中。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳之批次的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 請確定您使用唯一的檔案名稱，這樣它就不會與要提交之批次檔案的其他檔案衝突。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 確保內容型別是application/octet-stream。 請勿使用curl -F選項，因為該選項預設為與API不相容的多部分請求。

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本機檔案路徑，例如`acme/customers/campaigns/summer.json`。 |

**回應**

```http
200 OK
```

### 完成批次

上傳完檔案的所有不同部分後，您需要指出資料已完全上傳，且批次已準備好進行升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要完成的批次識別碼。 |

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

下節包含使用批次擷取在Experience Platform中擷取資料的其他資訊。

### 批次擷取的資料轉換

為了將資料檔案擷取到[!DNL Experience Platform]，該檔案的階層結構必須符合與要上傳到的資料集相關聯的[體驗資料模型(XDM)](../../xdm/home.md)結構描述。

有關如何對應CSV檔案以符合XDM結構描述的資訊，請參閱[範例轉換](../../etl/transformations.md)檔案，以及正確格式化的JSON資料檔案範例。 您可以在此處找到檔案中提供的範例檔案：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
