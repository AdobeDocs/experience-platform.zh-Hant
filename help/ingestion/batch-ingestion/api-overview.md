---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;ingestion;developer guide;api guide;upload;ingest parquet;ingest json;
solution: Experience Platform
title: Adobe Experience Platform批次擷取開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '2670'
ht-degree: 5%

---


# 批次擷取開發人員指南

本檔案提供使用批次擷取API [的完整概觀](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。

本檔案的附錄提供格式化資 [料以用於擷取的資訊](#data-transformation-for-batch-ingestion)，包括範例CSV和JSON資料檔案。

## 快速入門

資料擷取提供REST風格的API，您可透過此API對支援的物件類型執行基本的CRUD作業。

以下章節提供您必須知道或掌握的額外資訊，才能成功呼叫「批次擷取API」。

本指南需要有效瞭解Adobe Experience Platform的下列元件：

- [批次擷取](./overview.md):可讓您將資料以批次檔案的形式內嵌至Adobe Experience Platform。
- [[!DNL Experience Data Model] (XDM)系統](../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
- [[!DNL沙盒]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的請求可能需要額外的標 `Content-Type` 題。 在呼叫參數中提供每個呼叫的接受值。

## 類型

在擷取資料時，請務必瞭解(XDM) [!DNL Experience Data Model] 架構的運作方式。 有關XDM欄位類型如何映射到不同格式的詳細資訊，請閱讀 [Schema Registry Developer Guide](../../xdm/api/getting-started.md)。

在擷取資料時有一些彈性——如果某個類型不符合目標架構中的內容，資料將會轉換為表示的目標類型。 如果無法，則批次將失敗，並帶有 `TypeCompatibilityException`。

例如，JSON或CSV都沒有日期或日期時間類型。 因此，這些值是使用 [ISO 8061格式字串](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;)或以毫秒(153126395&quot;)格式化的Unix時間來表示9000)，並在擷取時轉換為目標XDM類型。

下表顯示在擷取資料時支援的轉換。

| 入站（行）與目標（列） | 字串 | 位元組 | 簡短 | 整數 | 長 | 雙倍 | 日期 | 日期——時間 | 物件 | 地圖 |
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
>以下範例適用於單行JSON。 若要收錄多行JSON, `isMultiLineJson` 必須設定旗標。 如需詳細資訊，請閱讀批次擷 [取疑難排解指南](./troubleshooting.md)。

**API格式**

```http
POST /batches
```

**請求**

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

現在您已建立批次，您可以使用之 `batchId` 前的開始，將檔案上傳至批次。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>如需格式正確的JSON資 [料檔案範例，請參閱附錄一節](#data-transformation-for-batch-ingestion)。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將儲存在Adobe端的位置。 |

**請求**

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `Users/sample-user/Downloads/sample.json`。 |

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

**請求**

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

**請求**

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

現在您已建立批次，您可以使用之 `batchId` 前的開始，將檔案上傳至批次。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將儲存在Adobe端的位置。 |

**請求**

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `Users/sample-user/Downloads/sample.json`。 |

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

**請求**

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

**請求**

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

**請求**

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

現在已建立檔案，可以通過重複的PATCH請求來上載所有後續的塊，對檔案的每個部分都可以一個。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將儲存在Adobe端的位置。 |

**請求**

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `Users/sample-user/Downloads/sample.json`。 |


**回應**

```http
200 OK
```

### 完整的大型檔案

現在您已建立批次，您可以使用之 `batchId` 前的開始，將檔案上傳至批次。 您可以上傳多個檔案至批次。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要指示完成的批的ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 要指示完成的檔案的名稱。 |

**請求**

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


**請求**

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

若要收錄CSV檔案，您必須建立支援CSV的類別、結構和資料集。 有關如何建立必要類和架構的詳細資訊，請遵循臨機架構建立教 [程中提供的說明](../../xdm/api/ad-hoc.md)。

>[!NOTE]
>
>以下步驟適用於小型檔案（256 MB或以下）。 如果您遇到閘道逾時或要求內文大小錯誤，則需要切換至大型檔案上傳。

### 建立資料集

依照上述指示建立必要的類別和架構後，您將需要建立可支援CSV的資料集。

**API格式**

```http
POST /catalog/dataSets
```

**請求**

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
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TENANT_ID}` | 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 |
| `{SCHEMA_ID}` | 您所建立之架構的ID。 |

以下說明JSON內文「fileDescription」區段的不同部分：

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `format` | 已掌握檔案的格式，而不是輸入檔案的格式。 |
| `delimiters` | 用作分隔字元的字元。 |
| `quotes` | 用於引號的字元。 |
| `escapes` | 用作轉義字元的字元。 |
| `header` | 上傳的檔案 **必須** 包含標題。 由於架構驗證已完成，因此必須將其設定為true。 此外，標題不得 **包含** 任何空格——如果您的標題中有任何空格，請改用底線取代。 |
| `charset` | 選填欄位。 其他支援的字元包括「US-ASCII」和「ISO-8869-1」。 如果保留空白，預設會使用UTF-8。 |

引用的資料集必須具有上面列出的檔案說明塊，並且必須指向註冊表中的有效模式。 否則，檔案將不會被控制為鑲木地板。

### 建立批次

接下來，您需要建立以CSV為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批次的一部分上載的所有檔案都符合連結到提供資料集的模式。

**API格式**

```http
POST /batches
```

**請求**

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

現在您已建立批次，您可以使用之 `batchId` 前的開始，將檔案上傳至批次。 您可以上傳多個檔案至批次。

>[!NOTE]
>
>如需格式正確的CSV資 [料檔案範例，請參閱附錄一節](#data-transformation-for-batch-ingestion)。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將儲存在Adobe端的位置。 |

**請求**

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `Users/sample-user/Downloads/sample.json`。 |


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

**請求**

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

**請求**

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

對要刪除的批的ID執行以下具有查詢參數的 `action=REVERT` POST請求，可以刪除批。 批標籤為「非活動」，使其符合垃圾回收的條件。 批將非同步收集，此時將標籤為「已刪除」。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要刪除的批的ID。 |

**請求**

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

首先，您需要建立以JSON為輸入格式的批次。 建立批次時，您需要提供資料集ID。 您還需要確保作為批處理的一部分上載的所有檔案都符合連結到所提供的資料集的XDM模式。 此外，您還需要在重放部分中提供舊批作為參考。 在以下範例中，您正在重新播放具有ID和的 `batchIdA` 批次 `batchIdB`。

**API格式**

```http
POST /batches
```

**請求**

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

現在您已建立批次，您可以使用之 `batchId` 前的開始，將檔案上傳至批次。 您可以上傳多個檔案至批次。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要上傳至的批次ID。 |
| `{DATASET_ID}` | 批次參考資料集的ID。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 此檔案路徑是檔案將儲存在Adobe端的位置。 |

**請求**

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
| `{FILE_PATH_AND_NAME}` | 您嘗試上傳之檔案的完整路徑和名稱。 此檔案路徑是本地檔案路徑，如 `Users/sample-user/Downloads/sample.json`。 |

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

**請求**

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

為了將資料檔案內嵌至其中 [!DNL Experience Platform]，檔案的階層結構必須符合與上傳資料集相關的 [Experience Data Model(XDM)](../../xdm/home.md) 架構。

有關如何映射CSV檔案以符合XDM架構的資訊，請參閱範例轉換文 [件](../../etl/transformations.md) ，以及格式正確的JSON資料檔案範例。 可在以下位置找到文檔中提供的示例檔案：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)