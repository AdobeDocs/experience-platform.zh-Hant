---
keywords: Experience Platform；首頁；熱門主題；批次內嵌；批次內嵌；內嵌；開發人員指南；api指南；上傳；內嵌Parquet；內嵌json;
solution: Experience Platform
title: 批次內嵌API指南
topic-legacy: developer guide
description: 本檔案提供使用批次擷取API的完整概述。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 6%

---

# 批次內嵌API指南

本檔案提供使用[批次擷取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)的完整概述。

本檔案附錄提供用於擷取](#data-transformation-for-batch-ingestion)之[格式化資料的資訊，包括範例CSV和JSON資料檔案。

## 快速入門

資料擷取提供RESTful API，您可透過此API對支援的物件類型執行基本CRUD作業。

以下小節提供您需要知道或已有的其他資訊，以便成功呼叫批次擷取API。

本指南需要妥善了解下列Adobe Experience Platform元件：

- [批次內嵌](./overview.md):可讓您將資料以批次檔案的形式內嵌至Adobe Experience Platform。
- [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的請求可能需要額外的`Content-Type`標題。 每個呼叫的接受值都會在呼叫參數中提供。

## 類型

擷取資料時，請務必了解[!DNL Experience Data Model](XDM)結構的運作方式。 有關XDM欄位類型如何映射到不同格式的詳細資訊，請參閱[Schema Registry開發人員指南](../../xdm/api/getting-started.md)。

擷取資料時有一些彈性 — 如果類型與目標架構中的內容不符，則資料會轉換為表示的目標類型。 如果無法，則會以`TypeCompatibilityException`失敗批次處理。

例如，JSON或CSV都沒有日期或日期時間類型。 因此，這些值是使用[ISO 8061格式化字串](https://www.iso.org/iso-8601-date-and-time-format.html)(&quot;2018-07-10T15:05:59.000-08:00&quot;)或Unix時間(以毫秒(1531263959000)為格式)表示，並在擷取時轉換為目標XDM類型。

下表顯示擷取資料時支援的轉換。

| 入站（列）與目標（列） | 字串 | 位元組 | 簡短 | 整數 | 長 | 雙倍 | Date | 日期時間 | 物件 | 地圖 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字串 | X | X | X | X | X | X | X | X |  |  |
| 位元組 | X | X | X | X | X | X |  |  |  |  |
| 簡短 | X | X | X | X | X | X |  |  |  |  |
| 整數 | X | X | X | X | X | X |  |  |  |  |
| 長 | X | X | X | X | X | X | X | X |  |  |
| 雙倍 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期時間 |  |  |  |  |  |  |  | X |  |  |
| 物件 |  |  |  |  |  |  |  |  | X | X |
| 地圖 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布林值和陣列無法轉換為其他類型。

## 擷取限制

批次資料內嵌有一些限制：
- 每批檔案的最大數量：1500
- 最大批大小：100 GB
- 每列的屬性或欄位數上限：10000
- 每用戶每分鐘的最大批次數：138

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

現在您已建立批處理，可以使用之前的`batchId`將檔案上載到該批處理。 您可以上傳多個檔案至批次。

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

## 內嵌鑲木檔案

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

上傳完檔案的所有不同部分後，您需要發出信號，指出資料已完全上傳，且批次已準備好升級。

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

### 批次內嵌的資料轉換

若要將資料檔案內嵌至[!DNL Experience Platform]，檔案的階層結構必須符合與上傳至之資料集相關聯的[Experience Data Model(XDM)](../../xdm/home.md)架構。

有關如何對應CSV檔案以符合XDM架構的資訊，請參閱[範例轉換](../../etl/transformations.md)檔案，以及格式正確的JSON資料檔案範例。 可在以下位置找到文檔中提供的示例檔案：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
