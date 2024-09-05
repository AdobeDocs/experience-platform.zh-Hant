---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；spark sdk；資料存取api；匯出；匯出
solution: Experience Platform
title: Data Access API指南
description: 資料存取API為開發人員提供RESTful介面，著重於Experience Platform內擷取資料集的可發現性和可存取性，以支援Adobe Experience Platform。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 1070c34bcd4577fcc5f0ac160196450db3aab9b0
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 4%

---

# 資料存取API指南

>[!IMPORTANT]
>
>資料存取API現在&#x200B;**已棄用**。 建議您使用目的地從Adobe Experience Platform匯出資料。 如需詳細資訊，請參閱[資料集匯出目的地檔案](../destinations/destination-types.md#dataset-export-destinations)。

資料存取API透過為使用者提供RESTful介面來支援Adobe Experience Platform，該介面著重於[!DNL Experience Platform]內擷取資料集的可發現性和可存取性。

![資料存取如何協助Experience Platform內擷取資料集的可發現性和可存取性的圖表。](images/Data_Access_Experience_Platform.png)

## API規格參考

您可以在[這裡](https://developer.adobe.com/experience-platform-apis/references/data-access/)找到OpenAPI參考檔案。

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

`"data"`陣列包含指定批次中所有檔案的清單。 每個傳回的檔案在`"dataSetFileId"`欄位中都有自己的唯一識別碼(`{FILE_ID}`)。 您可以使用此唯一ID來存取或下載檔案。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每個檔案的檔案識別碼。 |
| `data._links.self.href` | 存取檔案的URL。 |

## 存取和下載批次中的檔案

若要存取檔案的特定詳細資料，請將檔案識別碼(`{FILE_ID}`)搭配資料存取API使用，包括其名稱、位元組大小以及下載連結。

回應包含資料陣列。 根據ID指向的檔案是個別檔案還是目錄，傳回的資料陣列可能會包含單一專案或屬於該目錄的檔案清單。 每個檔案元素都包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 等於`"dataSetFileId"`，要存取的檔案識別碼。 |

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
| `data.name` | 檔案的名稱（例如，`profiles.csv`）。 |
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
| `data.name` | 檔案的名稱（例如，`profiles.csv`）。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 存取檔案的內容 {#access-file-contents}

您也可以使用[!DNL Data Access] API來存取檔案的內容。 然後，您可以將內容下載到外部來源。

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
| `{FILE_NAME}` | 檔案的完整名稱（例如，`profiles.csv`）。 |

**回應**

`Contents of the file`

## 其他程式碼範例

如需其他範例，請參閱[資料存取教學課程](tutorials/dataset-data.md)。

## 訂閱資料擷取事件 {#subscribe-to-data-ingestion-events}

您可以透過[Adobe Developer Console](https://developer.adobe.com/console/)訂閱特定的高值事件。 例如，您可以訂閱資料擷取事件，以接收潛在延遲和失敗的通知。 如需詳細資訊，請參閱[訂閱Adobe事件通知](../observability/alerts/subscribe.md)的教學課程。
