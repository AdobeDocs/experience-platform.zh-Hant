---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Amazon Redshift連接器
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# 使用Flow Service API建立Amazon Redshift連接器

>[!NOTE]
>Amazon Redshift連接器處於測試階段。 功能和檔案可能會有所變更。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接到Amazon Redshift（以下稱為「Redshift」）的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用Flow Service API成功連線至Redshift。

### 收集必要的認證

為了使流服務與Redshift連接，您必須提供以下連接屬性：

| **憑證** | **說明** |
| -------------- | --------------- |
| `server` | 與您的Redshift帳戶關聯的伺服器。 |
| `username` | 與您的Redshift帳戶關聯的用戶名。 |
| `password` | 與Redshift帳戶關聯的密碼。 |
| `database` | 您正在訪問的Redshift資料庫。 |

有關開始使用的詳細資訊，請參 [閱本Redshift文檔](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於流服務的資源）都會隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

要建立紅移連接，流服務中必須有一組紅移連接規範。 將平台與紅移連接起來的第一步是檢索這些規格。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 通過執行GET請求並使用查詢參數，可以查找Redshift的連接規範。

傳送不含查詢參數的GET請求時，會傳回所有可用來源的連線規格。 您可以包含查詢，以 `property=name=="amazon-redshift"` 獲取Redshift的具體資訊。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**請求**

以下請求將檢索Redshift的連接規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回Redshift的連接規範，包括其唯一標識符(`id`)。 在下個步驟中需要此ID才能建立基本連線。

```json
{
    "items": [
        {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "name": "amazon-redshift",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "server": {
                                "type": "string",
                                "description": "IP address or host name of the Amazon Redshift server"
                            },
                            "username": {
                                "type": "string",
                                "description": "Name of user who has access to the database"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "database": {
                                "type": "string",
                                "description": "Name of the Amazon Redshift database"
                            }
                        },
                        "required": [
                            "server",
                            "username",
                            "password",
                            "database"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個Redshift帳戶只需一個基本連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | 您的Redshift伺服器。 |
| `auth.params.database` | 與Redshift帳戶關聯的資料庫。 |
| `auth.params.password` | 與Redshift帳戶關聯的密碼。 |
| `auth.params.username` | 與您的Redshift帳戶關聯的用戶名。 |
| `connectionSpec.id` | 在上一步 `id` 中檢索的Redshift帳戶的連接規範。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

在本教程中，您使用Flow Service API建立了Redshift基本連接，並獲得了該連接的唯一ID值。 在下一個教程中，您可以使用此基本連接ID來學習如何使 [用流服務API來探索資料庫或NoSQL系統](../../explore/database-nosql.md)。
