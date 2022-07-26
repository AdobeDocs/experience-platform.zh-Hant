---
keywords: Experience Platform；首頁；熱門主題；
solution: Experience Platform
title: 使用流服務API將資料登錄區連接到Adobe Experience Platform
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到資料登錄區。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: b98afad74ef45cf3fabb9fa1ced283b2c768cef8
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 4%

---

# 連接 [!DNL Data Landing Zone] 到Adobe Experience Platform使用流服務API

[!DNL Data Landing Zone] 是一種安全、基於雲的檔案儲存設施，用於將檔案帶入Adobe Experience Platform。 資料將自動從 [!DNL Data Landing Zone] 七天後。

本教程將指導您完成如何建立 [!DNL Data Landing Zone] 源連接使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。 本教程還提供有關如何檢索 [!DNL Data Landing Zone]，以及查看和刷新您的憑據。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功建立 [!DNL Data Landing Zone] 源連接使用 [!DNL Flow Service] API。

本教程還要求您閱讀 [平台API入門](../../../../../landing/api-guide.md) 瞭解如何驗證到平台API並解釋文檔中提供的示例調用。

## 檢索可用著陸區

使用API訪問的第一步 [!DNL Data Landing Zone] 就是向他提出GET `/landingzone` 端點 [!DNL Connectors] API，同時提供 `type=user_drop_zone` 作為請求標題的一部分。

**API格式**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | 的 `user_drop_zone` type允許API將著陸區容器與可供您使用的其他類型的容器區別開來。 |

**要求**

以下請求檢索現有登錄區域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**回應**

以下響應返回著陸區的資訊，包括其相應的 `containerName` 和 `containerTTL`。

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 您檢索到的著陸區的名稱。 |
| `containerTTL` | 應用於登錄區域內資料的即時設定。 給定著陸區內的任何內容在七天後被刪除。 |

## 檢索 [!DNL Data Landing Zone] 憑據

檢索憑據 [!DNL Data Landing Zone]，向GET請求 `/credentials` 端點 [!DNL Connectors] API。

**API格式**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**要求**

以下請求示例檢索現有登錄區的憑據。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下響應返回您的登錄區的憑據資訊，包括當前的憑據資訊 `SASToken` 和 `SASUri`，以及 `storageAccountName` 與降落區容器相對應。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 降落區的名稱。 |
| `SASToken` | 登錄區域的共用訪問簽名令牌。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登錄區域的共用訪問簽名URI。 此字串是要對其進行身份驗證的登錄區域的URI及其相應的SAS令牌的組合， |


## 更新 [!DNL Data Landing Zone] 憑據

您可以更新 `SASToken` 通過向POST `/credentials` 端點 [!DNL Connectors] API。

**API格式**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | 的 `user_drop_zone` type允許API將著陸區容器與可供您使用的其他類型的容器區別開來。 |
| `refresh` | 的 `refresh` 操作允許您重置登錄區域憑據並自動生成新憑據 `SASToken`。 |

**要求**

以下請求更新您的登錄區域憑據。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下響應將返回更新的值 `SASToken` 和 `SASUri`。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 瀏覽登錄區域檔案結構和內容

您可以通過向以下站點發出GET請求來瀏覽登錄區的檔案結構和內容 `connectionSpecs` 端點 [!DNL Flow Service] API。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 與 [!DNL Data Landing Zone]。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢目錄中找到的檔案和資料夾陣列。 注意 `path` 要上載的檔案的屬性，因為需要在下一步中提供該屬性以檢查其結構。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 預覽登錄區域檔案結構和內容

要檢查登錄區域中檔案的結構，請在提供檔案路徑並鍵入查詢參數的同時執行GET請求。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 與 [!DNL Data Landing Zone]。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |
| `{OBJECT_TYPE}` | 要訪問的對象的類型。 | `file` |
| `{OBJECT}` | 要訪問的對象的路徑和名稱。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 檔案的類型。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 一個布爾值，用於定義是否支援檔案預覽。 | </ul><li>`true`</li><li>`false`</li></ul> |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回查詢檔案的結構，包括檔案名和資料類型。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### 使用 `determineProperties` 自動檢測 [!DNL Data Landing Zone]

您可以使用 `determineProperties` 用於自動檢測檔案內容的屬性資訊的參數 [!DNL Data Landing Zone] 進行GET調用以瀏覽源的內容和結構時。

#### `determineProperties` 使用案例

下表概述了使用 `determineProperties` 查詢參數或手動提供檔案資訊。

| `determineProperties` | `queryParams` | 回應 |
| --- | --- | --- |
| True | 不適用 | 如果 `determineProperties` 作為查詢參數提供，然後進行檔案屬性檢測並返回新 `properties` 鍵，其中包括有關檔案類型、壓縮類型和列分隔符的資訊。 |
| 不適用 | 真 | 如果檔案類型、壓縮類型和列分隔符的值是手動提供的，則作為 `queryParams`，然後使用它們生成模式，並返回作為響應一部分的相同屬性。 |
| 真 | 真 | 如果同時執行兩個選項，則返回錯誤。 |
| 不適用 | 不適用 | 如果未提供這兩個選項，則返回錯誤，因為無法獲取響應的屬性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `determineProperties` | 此查詢參數允許 [!DNL Flow Service] API，用於檢測有關檔案屬性的資訊，包括有關檔案類型、壓縮類型和列分隔符的資訊。 | `true` |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回查詢檔案的結構，包括檔案名和資料類型，以及 `properties` 鍵，包含有關 `fileType`。 `compressionType`, `columnDelimiter`。

+++按一下我

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 屬性 | 說明 |
| --- | --- |
| `properties.fileType` | 查詢檔案的相應檔案類型。 支援的檔案類型有： `delimited`。 `json`, `parquet`。 |
| `properties.compressionType` | 用於查詢檔案的相應壓縮類型。 支援的壓縮類型有： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用於查詢檔案的相應列分隔符。 任何單個字元值都是允許的列分隔符。 預設值是逗號 `(,)`。 |


## 建立源連接

源連接建立並管理與外部源的連接，該連接來自接收資料的位置。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 源連接實例是特定於租戶和IMS組織的。

要建立源連接，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。


**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 您的名稱 [!DNL Data Landing Zone] 源連接。 |
| `data.format` | 要帶到平台的資料的格式。 |
| `params.path` | 要帶到平台的檔案的路徑。 |
| `connectionSpec.id` | 與 [!DNL Data Landing Zone]。 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在下一教程中建立資料流時需要此ID。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 後續步驟

按照本教程，您已檢索到 [!DNL Data Landing Zone] 憑據、探索其檔案結構以查找要帶到平台的檔案，並建立源連接以開始將資料帶到平台。 現在，您可以繼續下一個教程，在該教程中您將學習如何 [建立資料流，使用 [!DNL Flow Service] API](../../collect/cloud-storage.md)。
