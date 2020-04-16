---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Google AdWords連接器
topic: overview
translation-type: tm+mt
source-git-commit: a456dce58c32348c9e680cd672b71dd7bbdc1a04

---


# 使用Flow Service API建立Google AdWords連接器

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Google AdWords（以下稱為「AdWords」）的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用Flow Service API成功連線至AdWords。

### 收集必要的認證

為了讓流式服務與AdWords連線，您必須提供下列連線屬性的值：

| **憑證** | **說明** |
| -------------- | --------------- |
| `clientCustomerID` | 與目標Google AdWords關聯的客戶ID | account. |
| `developerToken` | 用來識別AdWords API開發人員的字串。 |
| `refreshToken` | 從Google取得的重新整理Token，用來授權存取AdWords。 |
| `clientID` | 用來產生重新整理Token之應用程式的ID。 |
| `clientSecret` | 用來產生重新整理Token之應用程式的用戶端密碼。 |

如需這些值的詳細資訊，請參閱此 [Google AdWords檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於流服務的資源）都會隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

若要建立AdWords連線，Flow Service中必須有一組AdWords連線規格。 將Platform連接至AdWords的第一步是擷取這些規格。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 您可以執行GET請求並使用查詢參數，以尋找AdWords的連線規格。

傳送不含查詢參數的GET請求時，會傳回所有可用來源的連線規格。 您可以包含查詢， `property=name=="google-adwords"` 以取得AdWords的特定資訊。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-adwords"
```

**請求**

下列請求會擷取AdWords的連線規格。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?{QUERY_PARAMS}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回AdWords的連線規格，包括其唯一識別碼(`id`)。 在下個步驟中需要此ID才能建立基本連線。

```json
{
    "items": [
        {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "name": "google-adwords",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-adwords",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "clientCustomerID": {
                                "type": "string",
                                "description": "The Client customer ID of the AdWords account"
                            },
                            "developerToken": {
                                "type": "string",
                                "description": "The developer token associated with the manager account",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google for authorizing access to AdWords",
                                "format": "password"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "The client ID of the Google application used to acquire the refresh token"
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret of the google application used to acquire the refresh token",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientCustomerID",
                            "developerToken",
                            "refreshToken",
                            "clientId",
                            "clientSecret"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個AdWords帳戶只需要一個基本連線，因為它可用於建立多個來源連接器以匯入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-adwords base connection",
        "description": "Base connection for google-adwords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientCustomerID` | 您AdWords帳戶的客戶客戶ID。 |
| `auth.params.developerToken` | 您AdWords帳戶的開發人員代號。 |
| `auth.params.refreshToken` | 您AdWords帳戶的重新整理Token。 |
| `auth.params.clientID` | 您AdWords帳戶的用戶端ID。 |
| `auth.params.clientSecret` | 您AdWords帳戶的客戶機密碼。 |
| `connectionSpec.id` | 在上一步 `id` 中擷取的AdWords帳戶連線規格。 |

**回應**

成功的響應返回新建基本連`id`接的唯一標識符()。 在下一個教學課程中探索您的AdWords資料時，需要此ID。

```json
{
    "id": "e6ce1eab-416b-4a20-8e1e-ab416b1a206f",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

在本教學課程中，您已使用Flow Service API建立AdWords基本連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此基本連線ID，同時學習如 [何使用Flow Service API來探索CRM系統](../../explore/crm.md)。
