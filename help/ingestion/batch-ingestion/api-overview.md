---
keywords: Experience Platform;home；熱門主題；批次擷取；批次擷取；ingestion;developer guide;api guide;upload;ingest Parce;ingestjson;
solution: Experience Platform
title: 批次擷取API指南
topic: 開發人員指南
description: 本檔案提供使用批次擷取API的完整概觀。
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 6%

---

# 批次擷取API指南

本檔案提供使用[批次擷取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)的完整概觀。

本檔案的附錄提供用於擷取[的](#data-transformation-for-batch-ingestion)格式化資料的資訊，包括範例CSV和JSON資料檔案。

## 快速入門

資料擷取提供REST風格的API，您可透過此API對支援的物件類型執行基本的CRUD作業。

以下章節提供您必須知道或掌握的額外資訊，才能成功呼叫「批次擷取API」。

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [批次擷取](./overview.md):可讓您將資料以批次檔案的形式收錄到Adobe Experience Platform。
- [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的請求可能需要額外的`Content-Type`標題。 在呼叫參數中提供每個呼叫的接受值。

## 類型

在擷取資料時，請務必瞭解[!DNL Experience Data Model](XDM)結構如何運作。 有關XDM欄位類型如何映射到不同格式的詳細資訊，請閱讀[方案註冊表開發人員指南](../../xdm/api/getting-started.md)。

在擷取資料時有一些彈性——如果某個類型不符合目標架構中的內容，資料將會轉換為表示的目標類型。 如果無法，則會失敗具有`TypeCompatibilityException`的批。

例如，JSON或CSV都沒有日期或日期時間類型。 因此，這些值是使用[ISO 8061格式化字串](https://www.iso.org/iso-8601-date-and-time-format.html)(&quot;2018-07-10T15:05:59.000-08:00&quot;)或以毫秒為單位的Unix時間(153126&quot;)來表示3959000)，並在擷取時轉換為目標XDM類型。

下表顯示在擷取資料時支援的轉換。

| 入站（行）與目標（列） | 字串 | 位元組 | 簡短 | 整數 | 長 | 雙倍 | Date | 日期——時間 | 物件 | 地圖 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字串 | X | X | X | X | X | X | X | X |  |  |
| 位元組 | X | X | X | X | X | X |  |  |  |  |
| 簡短 | X | X | X | X | X | X |  |  |  |  |
| 整數 | X | X | X | X | X | X |  |  |  |  |
| 長 | X | X | X | X | X | X | X | X |  |  |
| 雙倍 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期——時間 |  |  |  |  |  |  |  | X |  |  |
| 物件 |  |  |  |  |  |  |  |  | X | X |
| 地圖 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Boolean和陣列不能轉換為其他類型。

## 擷取限制

批次資料擷取有一些限制：
- 每批檔案的最大數量：1500
- 最大批大小：100 GB
- 每列的屬性或欄位數上限：10000
- 每位使用者每分鐘的批次數上限：138

## 收錄JSON檔案

>[!NOTE]
>
>以下步驟適用於小型檔案（256 MB或以下）。 如果您遇到閘道逾時或要求內文大小錯誤，則需要切換至大型檔案上傳。

### 建立批次

首先，您需要建立以JSON為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM模式。

>[!NOTE]
>
>以下範例適用於單行JSON。 若要收錄多行JSON，必須設定`isMultiLineJson`旗標。 如需詳細資訊，請閱讀[批次擷取疑難排解指南](./troubleshooting.md)。

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
| `{BATCH_ID}` | 新建立批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |

### 上傳檔案

現在您已建立批次，您可以使用之前的`batchId`將檔案上傳至批次。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>請參閱附錄一節，以取得格式正確的JSON資料檔案](#data-transformation-for-batch-ingestion)範例。[

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將保存在Adobe端的位置。 |

**要求**

>[!NOTE]
>
>API支援單一部分上傳。 請確定內容類型為application/octet-stream。

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

上傳完檔案的所有不同部分後，您需要傳訊資料已完全上傳，且批次已準備好升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |

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

## 收錄Parce檔案

>[!NOTE]
>
>以下步驟適用於小型檔案（256 MB或以下）。 如果您遇到閘道逾時或要求內文大小錯誤，則需要切換至大型檔案上傳。

### 建立批次

首先，您需要建立以Parce為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM模式。

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
| `{BATCH_ID}` | 新建立批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上傳檔案

現在您已建立批次，您可以使用之前的`batchId`將檔案上傳至批次。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將保存在Adobe端的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定內容類型為application/octet-stream。

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

上傳完檔案的所有不同部分後，您需要傳訊資料已完全上傳，且批次已準備好升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要傳送訊號的批次ID已準備就緒，可供完成。 |

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

## 收錄大型拼花檔案

>[!NOTE]
>
>本節詳細說明如何上傳大於256 MB的檔案。 大型檔案會以區塊上傳，然後透過API訊號加以銜接。

### 建立批次

首先，您需要建立以Parce為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM模式。

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
| `{BATCH_ID}` | 新建立批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 初始化大型檔案

在建立批後，您需要先初始化大型檔案，然後再將塊上傳到批。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 新建立批的ID。 |
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

現在已建立檔案，所有後續區塊都可以透過重複的PATCH要求上傳，這是檔案每個區段的一個要求。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將保存在Adobe端的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定內容類型為application/octet-stream。

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
| `{CONTENT_RANGE}` | 在整數中，請求範圍的開始和結束。 |
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如`Users/sample-user/Downloads/sample.json`。 |


**回應**

```http
200 OK
```

### 完整的大型檔案

現在您已建立批次，您可以使用之前的`batchId`將檔案上傳至批次。 您可以上傳多個檔案至批次。

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

上傳完檔案的所有不同部分後，您需要傳訊資料已完全上傳，且批次已準備好升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要傳送訊號的批次ID已完成。 |


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

## 收錄CSV檔案

若要收錄CSV檔案，您必須建立支援CSV的類別、結構和資料集。 有關如何建立必要類和模式的詳細資訊，請按照[ad-hoc模式建立教程](../../xdm/api/ad-hoc.md)中提供的說明操作。

>[!NOTE]
>
>以下步驟適用於小型檔案（256 MB或以下）。 如果您遇到閘道逾時或要求內文大小錯誤，則需要切換至大型檔案上傳。

### 建立資料集

依照上述指示建立必要的類別和架構後，您將需要建立可支援CSV的資料集。

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
| `{TENANT_ID}` | 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 |
| `{SCHEMA_ID}` | 您所建立之架構的ID。 |

### 建立批次

接下來，您需要建立以CSV為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批次的一部分上載的所有檔案都符合連結到提供資料集的模式。

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
| `{BATCH_ID}` | 新建立批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |

### 上傳檔案

現在您已建立批次，您可以使用之前的`batchId`將檔案上傳至批次。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>請參閱附錄部分，瞭解格式正確的CSV資料檔案](#data-transformation-for-batch-ingestion)範例。[

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將保存在Adobe端的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定內容類型為application/octet-stream。

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

上傳完檔案的所有不同部分後，您需要傳訊資料已完全上傳，且批次已準備好升級。

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

在處理批時，仍可以取消批。 不過，一旦完成批次（例如成功或失敗狀態），便無法取消該批次。

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

## 刪除批{#delete-a-batch}

對要刪除的批的ID執行以下POST請求並使用`action=REVERT`查詢參數來刪除批。 批標籤為「非活動」，使其符合垃圾回收的條件。 批將非同步收集，此時將標籤為「已刪除」。

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

## 重放批次

如果要替換已提取的批，可以使用「批重放」來替換，此操作相當於刪除舊批並改用新批。

### 建立批次

首先，您需要建立以JSON為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM模式。 此外，您還需要在重放部分中提供舊批作為參考。 在以下範例中，您正在重新播放ID為`batchIdA`和`batchIdB`的批。

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
| `{BATCH_ID}` | 新建立批的ID。 |
| `{DATASET_ID}` | 參考資料集的ID。 |
| `{USER_ID}` | 建立批的用戶的ID。 |


### 上傳檔案

現在您已建立批次，您可以使用之前的`batchId`將檔案上傳至批次。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將保存在Adobe端的位置。 |

**要求**

>[!CAUTION]
>
>此API支援單一部分上傳。 請確定內容類型為application/octet-stream。 請勿使用curl -F選項，因為它預設為與API不相容的多部分請求。

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

上傳完檔案的所有不同部分後，您需要傳訊資料已完全上傳，且批次已準備好升級。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要完成的批次的ID。 |

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

### 批次擷取的資料轉換

為了將資料檔案嵌入[!DNL Experience Platform]中，檔案的分層結構必須符合與上載到的資料集相關聯的[體驗資料模型(XDM)](../../xdm/home.md)模式。

有關如何映射CSV檔案以符合XDM架構的資訊，請參閱[範例轉換](../../etl/transformations.md)檔案，以及格式正確的JSON資料檔案範例。 可在以下位置找到文檔中提供的示例檔案：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
