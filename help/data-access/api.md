---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；spark sdk；資料存取api；匯出；匯出
solution: Experience Platform
title: Data Access API指南
description: 資料存取API為開發人員提供RESTful介面，著重於Experience Platform內擷取資料集的可發現性和可存取性，以支援Adobe Experience Platform。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: d8694c094ae4a7284e4a3ed0ae5bc3dc198e501a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---

# 資料存取API指南

資料存取API為使用者提供RESTful介面，著重於內擷取資料集的可發現性和可存取性，以支援Adobe Experience Platform [!DNL Experience Platform].

![此圖表說明資料存取如何協助在Experience Platform中探索及存取內嵌的資料集。](images/Data_Access_Experience_Platform.png)

## API規格參考

Swagger API參考檔案可在以下網址找到： [此處](https://developer.adobe.com/experience-platform-apis/references/data-access/).

## 術語 {#terminology}

此表格提供本檔案中一些常用字詞的說明。

| 詞語 | 說明 |
| ----- | ------------ |
| 資料集 | 包含結構和欄位的資料集合。 |
| 批次 | 一段時間內收集並當作單一單位一起處理的一組資料。 |

## 擷取批次中的檔案清單 {#retrieve-list-of-files-in-a-batch}

若要擷取屬於特定批次的檔案清單，請將批次識別碼(batchID)與資料存取API搭配使用。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 指定批次的識別碼。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

此 `"data"` 陣列包含指定批次中所有檔案的清單。 每個傳回的檔案都有自己的唯一ID (`{FILE_ID}`)內含於 `"dataSetFileId"` 欄位。 您可以使用此唯一ID來存取或下載檔案。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每個檔案的檔案識別碼。 |
| `data._links.self.href` | 存取檔案的URL。 |

## 存取和下載批次中的檔案

若要存取檔案的特定詳細資料，請使用檔案識別碼(`{FILE_ID}`)，包括其名稱、位元組大小及下載連結。

回應包含資料陣列。 根據ID指向的檔案是個別檔案還是目錄，傳回的資料陣列可能會包含單一專案或屬於該目錄的檔案清單。 每個檔案元素都包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 等於 `"dataSetFileId"`，要存取之檔案的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**單一檔案回應**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.name` | 檔案的名稱(例如， `profiles.csv`)。 |
| `data.length` | 檔案的大小（位元組）。 |
| `data._links.self.href` | 下載檔案的URL。 |

**目錄回應**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

傳回目錄時，該目錄會包含目錄中所有檔案的陣列。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.name` | 檔案的名稱(例如， `profiles.csv`)。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 存取檔案的內容 {#access-file-contents}

您也可以使用 [!DNL Data Access] 用於存取檔案內容的API。 然後，您可以將內容下載到外部來源。

**API格式**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_NAME}` | 您嘗試存取的檔案名稱。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 資料集中檔案的ID。 |
| `{FILE_NAME}` | 檔案的完整名稱(例如， `profiles.csv`)。 |

**回應**

`Contents of the file`

## 其他程式碼範例

如需其他範例，請參閱 [資料存取教學課程](tutorials/dataset-data.md).

## 訂閱資料擷取事件 {#subscribe-to-data-ingestion-events}

您可以透過以下方式訂閱特定的高價值事件： [Adobe Developer Console](https://developer.adobe.com/console/). 例如，您可以訂閱資料擷取事件，以接收潛在延遲和失敗的通知。 請參閱上的教學課程 [訂閱資料擷取通知](../ingestion/quality/subscribe-events.md) 以取得詳細資訊。
