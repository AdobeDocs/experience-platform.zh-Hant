---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立HubSpot連接器
topic: overview
translation-type: tm+mt
source-git-commit: 5839e4695589455bd32b6e3e33a7c377343f920d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 1%

---


# 使用 [!DNL HubSpot] API建立連 [!DNL Flow Service] 接器

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至的 [!DNL Experience Platform] 步驟 [!DNL HubSpot]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL HubSpot][!DNL Flow Service] API成功連線至。

### 收集必要的認證

要連接， [!DNL Flow Service] 必須提供 [!DNL HubSpot]以下連接屬性：

| 憑證 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的應用程式相關聯的用戶 [!DNL HubSpot] 端ID。 |
| `clientSecret` | 與您的應用程式相關聯的用戶端 [!DNL HubSpot] 密碼。 |
| `accessToken` | 首次驗證您的OAuth整合時取得的存取Token。 |
| `refreshToken` | 初次驗證您的OAuth整合時取得的重新整理Token。 |

有關快速入門的詳細資訊，請參閱此 [HubSpot檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

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

要建立連接， [!DNL HubSpot] 必須在中存 [!DNL HubSpot] 在一組連接規範 [!DNL Flow Service]。 連接到的第一步 [!DNL Platform] 是 [!DNL HubSpot] 檢索這些規範。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 向端點發送GET請求 `/connectionSpecs` 將返回所有可用源的連接規範。 您也可以包含查詢， `property=name=="hubspot"` 以取得特定的資訊 [!DNL HubSpot]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**請求**

以下請求將檢索的連接規範 [!DNL HubSpot]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回的連接規範 [!DNL HubSpot]，包括其唯一標識符(`id`)。 在下個步驟中，此ID是建立API連線的必要項。

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 建立API的連線

API的連線會指定來源，並包含該來源的認證。 每個帳戶只需要一個API連線， [!DNL HubSpot] 因為它可用於建立多個來源連接器，以匯入不同的資料。

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
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的應用程式相關聯的用戶 [!DNL HubSpot] 端ID。 |
| `auth.params.clientSecret` | 與您的應用程式相關聯的用戶端 [!DNL HubSpot] 密碼。 |
| `auth.params.accessToken` | 首次驗證您的OAuth整合時取得的存取Token。 |
| `auth.params.refreshToken` | 初次驗證您的OAuth整合時取得的重新整理Token。 |

**回應**

成功的回應會傳回新建立之API連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

在本教學課程中，您已使 [!DNL HubSpot] 用 [!DNL Flow Service] API建立連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此連線ID，學習如 [何使用Flow Service API來探索CRM系統](../../explore/crm.md)。