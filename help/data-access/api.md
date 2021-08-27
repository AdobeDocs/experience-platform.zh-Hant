---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk;spark sdk；資料存取api；匯出；匯出
solution: Experience Platform
title: 資料存取API指南
topic-legacy: developer guide
description: 資料存取API為開發人員提供RESTful介面，著重於Experience Platform內所擷取資料集的探索性和協助功能，以支援Adobe Experience Platform。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---

# 資料存取API指南

資料存取API為使用者提供RESTful介面，著重於[!DNL Experience Platform]內所擷取資料集的可探索性和可存取性，以支援Adobe Experience Platform。

![資料存取Experience Platform](images/Data_Access_Experience_Platform.png)

## API規格參考

您可在[此處](https://www.adobe.io/experience-platform-apis/references/data-access/)找到Swagger API參考檔案。

## 術語

本檔案中常用術語的說明。

| 詞語 | 說明 |
| ----- | ------------ |
| 資料集 | 包含結構和欄位的資料集合。 |
| 批次 | 在一段時間內收集並以單一單位一起處理的一組資料。 |

## 檢索批中的檔案清單

透過使用批次識別碼(batchID)，資料存取API可擷取屬於該特定批次的檔案清單。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

`"data"`陣列包含指定批中所有檔案的清單。 傳回的每個檔案在`"dataSetFileId"`欄位中都包含其專屬的唯一ID(`{FILE_ID}`)。 然後，便可使用此唯一ID來存取或下載檔案。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批中每個檔案的檔案ID。 |
| `data._links.self.href` | 存取檔案的url。 |

## 批次存取和下載檔案

通過使用檔案標識符(`{FILE_ID}`)，資料訪問API可用於訪問檔案的特定詳細資訊，包括其名稱、位元組大小和下載連結。

回應將包含資料陣列。 根據ID指向的檔案是單個檔案還是目錄，返回的資料陣列可能包含一個條目或屬於該目錄的檔案清單。 每個檔案元素都包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 等於`"dataSetFileId"`，要存取的檔案ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | 檔案名稱（例如profiles.csv）。 |
| `data.length` | 檔案大小（以位元組為單位）。 |
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
| `data.name` | 檔案名稱（例如profiles.csv）。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 存取檔案的內容

[!DNL Data Access] API也可用於存取檔案的內容。 然後，這可用來將內容下載至外部來源。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 資料集內的檔案ID。 |
| `{FILE_NAME}` | 檔案的完整名稱（例如profiles.csv）。 |

**回應**

`Contents of the file`

## 其他程式碼範例

有關其他示例，請參閱[資料訪問教程](tutorials/dataset-data.md)。

## 訂閱資料擷取事件

[!DNL Platform] 可透過Adobe開發人員控制台 [提供特定的高](https://www.adobe.com/go/devs_console_ui)價值事件供訂閱。例如，您可以訂閱資料擷取事件，以接收可能延遲和失敗的通知。 如需詳細資訊，請參閱[訂閱資料擷取通知](../ingestion/quality/subscribe-events.md)的教學課程。
