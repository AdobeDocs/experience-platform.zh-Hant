---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk;spark sdk；資料存取api；導出；導出
solution: Experience Platform
title: 資料存取API指南
topic-legacy: developer guide
description: Data Access API為Adobe Experience Platform公司提供REST風格的介面，主要針對在Experience Platform內蒐集到的資料集的可探索性和可存取性，為開發人員提供支援。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# 資料存取API指南

Data Access API為Adobe Experience Platform提供REST風格的介面，主要針對[!DNL Experience Platform]內收錄資料集的可探索性和可存取性，為使用者提供支援。

![Experience Platform時的資料存取](images/Data_Access_Experience_Platform.png)

## API規格參考

Swagger API參考檔案可在[這裡](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)找到。

## 術語

本檔案中常用術語的說明。

| 詞語 | 說明 |
| ----- | ------------ |
| 資料集 | 包含架構和欄位的資料集合。 |
| 批次 | 一組在一段時間內收集並以單個單位一起處理的資料。 |

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

`"data"`陣列包含指定批中所有檔案的清單。 傳回的每個檔案在`"dataSetFileId"`欄位中都包含其專屬的唯一ID(`{FILE_ID}`)。 然後，此唯一ID可用來存取或下載檔案。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每個檔案的檔案ID。 |
| `data._links.self.href` | 存取檔案的URL。 |

## 在批次中存取和下載檔案

透過使用檔案識別碼(`{FILE_ID}`)，資料存取API可用來存取檔案的特定詳細資料，包括檔案名稱、位元組大小和下載連結。

回應將包含資料陣列。 根據ID所指向的檔案是單個檔案還是目錄，返回的資料陣列可能包含屬於該目錄的單個條目或檔案清單。 每個檔案元素都會包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 等於`"dataSetFileId"`，即要訪問的檔案的ID。 |

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
| `data.name` | 檔案的名稱（例如profiles.csv）。 |
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

返回目錄時，該目錄包含目錄內所有檔案的陣列。

| 屬性 | 說明 |
| -------- | ----------- |
| `data.name` | 檔案的名稱（例如profiles.csv）。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 存取檔案內容

[!DNL Data Access] API也可用來存取檔案的內容。 然後，這可用來將內容下載至外部來源。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 資料集內檔案的ID。 |
| `{FILE_NAME}` | 檔案的完整名稱（例如profiles.csv）。 |

**回應**

`Contents of the file`

## 其他程式碼範例

有關其他示例，請參閱[資料存取教程](tutorials/dataset-data.md)。

## 訂閱資料擷取事件

[!DNL Platform] 透過Adobe開發人員主控台提供特定的高價值 [事件供訂閱](https://www.adobe.com/go/devs_console_ui)。例如，您可以訂閱資料擷取事件，以通知您可能發生的延遲和失敗。 如需詳細資訊，請參閱[訂閱資料擷取通知的教學課程。](../ingestion/quality/subscribe-events.md)
