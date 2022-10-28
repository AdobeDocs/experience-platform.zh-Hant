---
keywords: Experience Platform；首頁；熱門主題；
solution: Experience Platform
title: 使用流量服務API將資料登陸區域連線至Adobe Experience Platform
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至資料登陸區。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 4%

---

# Connect [!DNL Data Landing Zone] 使用流量服務API傳送至Adobe Experience Platform

[!DNL Data Landing Zone] 是安全的雲端檔案儲存功能，可將檔案匯入Adobe Experience Platform。 資料會自動從 [!DNL Data Landing Zone] 七天後。

本教學課程會逐步帶您了解如何建立 [!DNL Data Landing Zone] 源連接使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 本教學課程也提供如何擷取 [!DNL Data Landing Zone]，以及檢視和重新整理您的憑證。

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功建立 [!DNL Data Landing Zone] 源連接使用 [!DNL Flow Service] API。

本教學課程也要求您閱讀 [Platform API快速入門](../../../../../landing/api-guide.md) 了解如何驗證至Platform API並解譯檔案中提供的範例呼叫。

## 擷取可用的登陸區

使用API存取的第一步 [!DNL Data Landing Zone] 是向 `/landingzone` 端點 [!DNL Connectors] API，同時提供 `type=user_drop_zone` 作為請求標題的一部分。

**API格式**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | 此 `user_drop_zone` 類型可讓API將著陸區容器與您可用的其他類型容器區分開來。 |

**要求**

下列要求會擷取現有的登陸區域。

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

下列回應會傳回登錄區域的資訊，包括其對應的 `containerName` 和 `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 您擷取的登陸區域名稱。 |
| `containerTTL` | 登錄區域內套用至資料的到期時間（以天為單位）。 指定登錄區域內的任何值會在七天後刪除。 |

## 擷取 [!DNL Data Landing Zone] 憑據

檢索憑據 [!DNL Data Landing Zone]，請向提出GET要求 `/credentials` 端點 [!DNL Connectors] API。

**API格式**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**要求**

下列要求範例會擷取現有登陸區域的憑證。

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

以下回應會傳回登錄區的憑證資訊，包括您目前的 `SASToken` 和 `SASUri`，以及 `storageAccountName` 對應至著陸區容器。

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
| `containerName` | 登錄區域的名稱。 |
| `SASToken` | 登錄區域的共用存取簽名令牌。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登錄區域的共用訪問簽名URI。 此字串是登錄區域的URI及其對應的SAS令牌的組合， |


## 更新 [!DNL Data Landing Zone] 憑據

您可以更新 `SASToken` 透過向 `/credentials` 端點 [!DNL Connectors] API。

**API格式**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | 此 `user_drop_zone` 類型可讓API將著陸區容器與您可用的其他類型容器區分開來。 |
| `refresh` | 此 `refresh` 動作可讓您重設登錄區域憑證，並自動產生新的 `SASToken`. |

**要求**

下列請求會更新您的登錄區域憑證。

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

下列回應會傳回 `SASToken` 和 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 探索登錄區域檔案結構和內容

您可以向發出GET要求，以探索登錄區域的檔案結構和內容 `connectionSpecs` 端點 [!DNL Flow Service] API。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 與 [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

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

成功的響應返回在查詢的目錄中找到的檔案和資料夾陣列。 請注意 `path` 屬性，因為您需要在下一個步驟中提供它以檢查其結構。

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

若要檢查登錄區域中的檔案結構，請執行GET要求，同時提供檔案的路徑和類型作為查詢參數。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 與 [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | 要訪問的對象的類型。 | `file` |
| `{OBJECT}` | 要訪問的對象的路徑和名稱。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 檔案的類型。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 一個布林值，定義是否支援檔案預覽。 | </ul><li>`true`</li><li>`false`</li></ul> |

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

成功的回應會傳回查詢的檔案結構，包括檔案名稱和資料類型。

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

您可以使用 `determineProperties` 參數來自動偵測您的 [!DNL Data Landing Zone] 進行GET呼叫以探索來源的內容和結構時。

#### `determineProperties` 使用案例

下表概述了使用 `determineProperties` 查詢參數，或手動提供檔案的相關資訊。

| `determineProperties` | `queryParams` | 回應 |
| --- | --- | --- |
| True | 不適用 | 若 `determineProperties` 會以查詢參數的形式提供，則會發生檔案屬性偵測，且回應會傳回新的 `properties` 索引鍵，包含檔案類型、壓縮類型和欄分隔字元的相關資訊。 |
| 不適用 | True | 如果檔案類型、壓縮類型和列分隔符的值是手動提供的，則作為 `queryParams`，則會用來產生結構，並會在回應中傳回相同的屬性。 |
| True | True | 如果同時完成兩個選項，則會傳回錯誤。 |
| 不適用 | 不適用 | 如果兩個選項均未提供，則會傳回錯誤，因為無法取得回應的屬性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `determineProperties` | 此查詢參數可讓 [!DNL Flow Service] 偵測檔案屬性相關資訊的API，包括檔案類型、壓縮類型和欄分隔字元的資訊。 | `true` |

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

成功的回應會傳回查詢的檔案結構，包括檔案名稱和資料類型，以及 `properties` 索引鍵，包含 `fileType`, `compressionType`，和 `columnDelimiter`.

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
| `properties.fileType` | 查詢檔案的相應檔案類型。 支援的檔案類型為： `delimited`, `json`，和 `parquet`. |
| `properties.compressionType` | 用於查詢的檔案的相應壓縮類型。 支援的壓縮類型為： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用於查詢的檔案的相應列分隔符。 任何單一字元值都是允許的欄分隔字元。 預設值為逗號 `(,)`. |


## 建立源連接

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 來源連線例項是租用戶和IMS組織專屬的。

若要建立來源連線，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。


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
| `name` | 您的 [!DNL Data Landing Zone] 源連接。 |
| `data.format` | 您要帶入Platform的資料格式。 |
| `params.path` | 要帶入Platform之檔案的路徑。 |
| `connectionSpec.id` | 與 [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 後續步驟

依照本教學課程，您已擷取 [!DNL Data Landing Zone] 憑證、探索其檔案結構以尋找您要帶入Platform的檔案，並建立來源連線以開始將資料帶入Platform。 您現在可以繼續下一個教學課程，學習如何 [建立資料流，使用 [!DNL Flow Service] API](../../collect/cloud-storage.md).
