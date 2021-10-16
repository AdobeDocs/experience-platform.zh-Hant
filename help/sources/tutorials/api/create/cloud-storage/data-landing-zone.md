---
keywords: Experience Platform；首頁；熱門主題；
solution: Experience Platform
title: 使用流量服務API將資料登陸區域連線至Adobe Experience Platform
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至資料登陸區。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 3%

---

# 使用流量服務API將[!DNL Data Landing Zone]連線至Adobe Experience Platform

[!DNL Data Landing Zone] 是雲端資料儲存設施，適用於布建有Adobe Experience Platform的暫存檔案儲存。7天後，資料會從[!DNL Data Landing Zone]中自動刪除。

本教學課程會逐步引導您了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Data Landing Zone]來源連線。 本教學課程也提供如何擷取[!DNL Data Landing Zone]，以及檢視和重新整理憑證的指示。

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功建立[!DNL Data Landing Zone]源連接。

此外，本教學課程需要您閱讀[Platform API快速入門手冊](../../../../../landing/api-guide.md)，了解如何驗證Platform API並解譯檔案中提供的範例呼叫。

## 擷取可用的登陸區

使用API存取[!DNL Data Landing Zone]的第一步，是向[!DNL Connectors] API的`/landingzone`端點提出GET要求，同時提供`type=user_drop_zone`作為要求標題的一部分。

**API格式**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`類型可讓API將著陸區容器與您可用的其他類型容器區分。 |

**要求**

下列要求會擷取現有的登陸區域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**回應**

下列回應會傳回登錄區域的資訊，包括其對應的`containerName`和`containerTTL`。

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 您擷取的登陸區域名稱。 |
| `containerTTL` | 套用至登陸區域內資料的存留時間設定。 指定登錄區域內的任何值會在七天後刪除。 |

## 檢索[!DNL Data Landing Zone]憑據

要檢索[!DNL Data Landing Zone]的憑據，請向[!DNL Connectors] API的`/credentials`端點發出GET請求。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下回應會傳回登錄區的憑證資訊，包括您目前的`SASToken`和`SASUri`，以及與登錄區容器對應的`storageAccountName`。

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


## 更新[!DNL Data Landing Zone]憑據

您可以向[!DNL Connectors] API的`/credentials`端點提出POST請求，以更新`SASToken`。

**API格式**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 標頭 | 說明 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`類型可讓API將著陸區容器與您可用的其他類型容器區分。 |
| `refresh` | `refresh`動作可讓您重設登錄區域憑證並自動產生新的`SASToken`。 |

**要求**

下列請求會更新您的登錄區域憑證。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下響應返回`SASToken`和`SASUri`的更新值。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 探索登錄區域檔案結構和內容

您可以向[!DNL Flow Service] API的`connectionSpecs`端點提出GET要求，以探索登錄區域的檔案結構和內容。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 與[!DNL Data Landing Zone]對應的連接規範ID。 此固定ID為：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回在查詢的目錄中找到的檔案和資料夾陣列。 記下您要上傳之檔案的`path`屬性，因為您必須在下一個步驟中提供該屬性以檢查其結構。

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
| `{CONNECTION_SPEC_ID}` | 與[!DNL Data Landing Zone]對應的連接規範ID。 此固定ID為：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢的檔案的結構，包括表名和資料類型。

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

## 建立源連接

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 來源連線例項是租用戶和IMS組織專屬的。

要建立源連接，請向[!DNL Flow Service] API的`/sourceConnections`端點發出POST請求。


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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | [!DNL Data Landing Zone]源連接的名稱。 |
| `data.format` | 您要帶入Platform的資料格式。 |
| `params.path` | 要帶入Platform之檔案的路徑。 |
| `connectionSpec.id` | 與[!DNL Data Landing Zone]對應的連接規範ID。 此固定ID為：`26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 後續步驟

依照本教學課程，您已擷取您的[!DNL Data Landing Zone]憑證、探索其檔案結構以尋找您要帶入Platform的檔案，並建立來源連線以開始將資料帶入Platform。 您現在可以繼續進行下一個教學課程，其中您將學習如何[建立資料流，以使用 [!DNL Flow Service] API](../../collect/cloud-storage.md)將雲儲存資料帶入Platform。
