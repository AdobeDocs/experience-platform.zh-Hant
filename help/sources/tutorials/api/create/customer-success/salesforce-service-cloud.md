---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Salesforce Service Cloud連接器
topic: overview
translation-type: tm+mt
source-git-commit: cada7c7eff7597015caa7333559bef16a59eab65
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---


# 使用Flow Service API建立Salesforce Service Cloud連接器

>[!NOTE]
>Salesforce Service Cloud連接器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Salesforce Service Cloud（以下稱為「SSC」）的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用流服務API成功連接到SSC。

### 收集必要的認證

要使流服務與SSC連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `username` | 使用者帳戶的使用者名稱。 |
| `password` | 使用者帳戶的密碼。 |
| `securityToken` | 使用者帳戶的安全性Token。 |

如需快速入門的詳細資訊，請參 [閱此Salesforce Service Cloud檔案](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於Flow Service的資源）都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

要建立SSC連接，流服務中必須存在一組SSC連接規範。 將平台連接到SSC的第一步是檢索這些規範。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 向端點發送GET請求 `/connectionSpecs` 將返回所有可用源的連接規範。 您還可以包括查詢以 `property=name=="salesforce-service-cloud"` 獲取SSC的具體資訊。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**請求**

以下請求檢索SSC的連接規範。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回SSC的連接規範，包括其唯一標識符(`id`)。 在下個步驟中，建立基本連線時需要此ID。

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個SSC帳戶只需要一個基本連接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.username` | 與SSC帳戶關聯的用戶名。 |
| `auth.params.password` | 與SSC帳戶關聯的密碼。 |
| `auth.params.securityToken` | 與SSC帳戶關聯的安全令牌。 |
| `connectionSpec.id` | 在上一步 `id` 中檢索的SSC帳戶的連接規範。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

通過本教程，您已使用流服務API建立了SSC基本連接，並獲取了連接的唯一ID值。 在下一個教學課程中，您可以使用此基本連線ID，學習如 [何使用Flow Service API來探索客戶成功系統](../../explore/customer-success.md)。
