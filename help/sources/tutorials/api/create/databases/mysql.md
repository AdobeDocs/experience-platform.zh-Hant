---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流服務API建立MySQL連接器
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---


# 使用流服務API建立MySQL連接器

>[!NOTE]
>MySQL連接器處於測試階段。 功能和檔案可能會有所變更。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至MySQL的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用流式服務API成功連線至MySQL。

### 收集必要的認證

要使流服務與您的MySQL儲存連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的帳戶關聯的MySQL連接字串。 |

您可以閱讀 [MySQL檔案，進一步瞭解連接字串以及如何獲取連接字串](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)。

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

為了建立MySQL連接，Flow Service中必須存在一組MySQL連接規範。 將Platform連接到MySQL的第一步是檢索這些規範。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 向端點發送GET請求 `/connectionSpecs` 將返回所有可用源的連接規範。 您也可以包含查詢， `property=name=="mysql"` 以獲取MySQL的具體資訊。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="mysql"
```

**請求**

以下請求檢索MySQL的連接規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回MySQL的連接規範，包括其唯一標識符(`id`)。 在下個步驟中，建立基本連線時需要此ID。

```json
{
    "items": [
        {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "name": "mysql",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionStringAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to MySql",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any MySql instance.",
                                "format": "password",
                                "pattern": "^([sS]erver=)(.*)( ?;[pP]ort=)(.*)(; ?[dD]atabase=)(.*)(; ?[uU]id=)(.*)(; ?[pP]wd=)(.*)(;)",
                                "examples": [
                                    "Server=myserver.mysql.database.azure.com; Port=3306; Database=my_sql_db; Uid=username; Pwd=password; SslMode=Preferred;"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個MySQL帳戶只需要一個基本連接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "name": "MySQL Test Connection",
        "description": "MySQL Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 與MySQL帳戶關聯的連接字串。 |
| `connectionSpec.id` | 與MySQL帳戶關聯的連接規範的ID。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## 後續步驟

在本教程中，您使用流服務API建立了MySQL基連接，並獲取了該連接的唯一ID值。 在下一個教程中，您可以使用此基本連接ID來學習如何使 [用流服務API來探索資料庫或NoSQL系統](../../explore/database-nosql.md)。