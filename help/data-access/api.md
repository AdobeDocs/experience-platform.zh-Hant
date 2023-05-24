---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk;spark sdk；資料存取api；導出；導出
solution: Experience Platform
title: 《資料存取API指南》
description: Data Access API支援Adobe Experience Platform，它為開發人員提供了REST風格的介面，重點關注在Experience Platform內接收的資料集的可發現性和可訪問性。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---

# 資料存取API指南

Data Access API支援Adobe Experience Platform，它為用戶提供了REST風格的介面，重點關注所攝取資料集在內的可發現性和可訪問性 [!DNL Experience Platform]。

![資料存取Experience Platform](images/Data_Access_Experience_Platform.png)

## API規範參考

可以找到Swagger API參考文檔 [這裡](https://www.adobe.io/experience-platform-apis/references/data-access/)。

## 術語

本文檔中一些常用術語的說明。

| 詞語 | 說明 |
| ----- | ------------ |
| 資料集 | 包括架構和欄位的資料集合。 |
| 批 | 一組在一段時間內收集並作為單個單元一起處理的資料。 |

## 檢索批處理中的檔案清單

通過使用批標識符(batchID)，資料存取API可以檢索屬於該特定批的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 指定批的ID。 |

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

的 `"data"` 陣列包含指定批處理中所有檔案的清單。 返回的每個檔案都有其自己的唯一ID(`{FILE_ID}`) `"dataSetFileId"` 的子菜單。 此唯一ID可用於訪問或下載檔案。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批中每個檔案的檔案ID。 |
| `data._links.self.href` | 訪問檔案的URL。 |

## 訪問和下載批處理中的檔案

使用檔案標識符(`{FILE_ID}`)，資料存取API可用於訪問檔案的特定詳細資訊，包括其名稱、大小（以位元組為單位）以及要下載的連結。

響應將包含一個資料陣列。 根據ID所指向的檔案是單個檔案還是目錄，返回的資料陣列可能包含一個條目或屬於該目錄的檔案清單。 每個檔案元素都將包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 等於 `"dataSetFileId"`，要訪問的檔案的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**單個檔案響應**

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
| `data.name` | 檔案的名稱（例如profiles.csv）。 |
| `data.length` | 檔案大小（位元組）。 |
| `data._links.self.href` | 下載檔案的URL。 |

**目錄響應**

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

返回目錄時，它包含目錄內所有檔案的陣列。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.name` | 檔案的名稱（例如profiles.csv）。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 訪問檔案的內容

的 [!DNL Data Access] API還可用於訪問檔案的內容。 然後，可以使用此功能將內容下載到外部源。

**API格式**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_NAME}` | 您嘗試訪問的檔案的名稱。 |

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
| `{FILE_ID}` | 資料集內檔案的ID。 |
| `{FILE_NAME}` | 檔案的全名（例如profiles.csv）。 |

**回應**

`Contents of the file`

## 其他代碼示例

有關其他示例，請參閱 [資料存取教程](tutorials/dataset-data.md)。

## 訂閱資料接收事件

[!DNL Platform] 使特定高價值事件可通過 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui)。 例如，您可以訂閱資料接收事件，以通知可能的延遲和故障。 請參閱上的教程 [訂閱資料接收通知](../ingestion/quality/subscribe-events.md) 的子菜單。
