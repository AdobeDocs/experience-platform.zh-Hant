---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Salesforce連接器
topic: overview
translation-type: tm+mt
source-git-commit: 5839e4695589455bd32b6e3e33a7c377343f920d
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---


# 使用 [!DNL Salesforce] API建立連 [!DNL Flow Service] 接器

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至帳戶以 [!DNL Platform] 收集 [!DNL Salesforce] CRM資料的步驟。

如果您想要使用中的使用者介面 [!DNL Experience Platform], [](../../../ui/create/crm/salesforce.md) Salesforce來源連接器UI教學課程會提供執行類似動作的逐步指示。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL Platform] API [!DNL Salesforce] 成功連 [!DNL Flow Service] 線至帳戶。

### 收集必要的認證

要連接 [!DNL Flow Service] 到，必須 [!DNL Salesforce]為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | 來源例項的 [!DNL Salesforce] URL。 |
| `username` | 使用者帳戶的 [!DNL Salesforce] 使用者名稱。 |
| `password` | 使用者帳戶 [!DNL Salesforce] 的密碼。 |
| `securityToken` | 使用者帳戶的安 [!DNL Salesforce] 全性Token。 |

如需快速入門的詳細資訊，請造 [訪此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

在連接 [!DNL Platform] 到帳 [!DNL Salesforce] 戶之前，必須驗證是否存在連接規範 [!DNL Salesforce]。 如果連接規範不存在，則無法建立連接。

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 您可以執行GET請求並使 [!DNL Salesforce] 用查詢參數，查找連接規範。

**API格式**

傳送不含查詢參數的GET請求時，會傳回所有可用來源的連線規格。 您可以包含查詢， `property=name=="salesforce"` 以取得特定的資訊 [!DNL Salesforce]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**請求**

以下請求將檢索的連接規範 [!DNL Salesforce]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回的連接規範 [!DNL Salesforce]，包括其唯一標識符(`id`)。 在下個步驟中需要此ID才能建立基本連線。

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
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
            ]
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個帳戶只需要一個基本連 [!DNL Salesforce] 接，因為它可用於建立多個源連接器以導入不同的資料。

執行以下POST請求以建立基本連接。

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.username` | 與您帳戶關聯的使用 [!DNL Salesforce] 者名稱。 |
| `auth.params.password` | 與您帳戶關聯的 [!DNL Salesforce] 密碼。 |
| `auth.params.securityToken` | 與您帳戶關聯的安全性 [!DNL Salesforce] Token。 |
| `connectionSpec.id` | 在上一步 `id` 中檢索 [!DNL Salesforce] 的帳戶的連接規範。 |

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 後續步驟

在本教學課程中，您已使用API為您的帳戶建立基 [!DNL Salesforce] 本連線，而且已取得唯一ID作為回應內文的一部分。 在下一個教學課程中，您可以使用此基本連線ID，同時學習如 [何使用Flow Service API來探索CRM系統](../../explore/crm.md)。