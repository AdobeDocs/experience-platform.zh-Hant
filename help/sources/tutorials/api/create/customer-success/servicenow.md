---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立ServiceNow連接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---


# 使用 [!DNL ServiceNow] API建立連 [!DNL Flow Service] 接器

>[!NOTE]
>
>連接 [!DNL ServiceNow] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至伺服器 [!DNL Experience Platform] 的步 [!DNL ServiceNow] 驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用API成功連 [!DNL ServiceNow] 線至伺 [!DNL Flow Service] 服器。

### 收集必要的認證

要連接 [!DNL Flow Service] 到，必須 [!DNL ServiceNow]為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | 用於連接到伺服器以進行驗 [!DNL ServiceNow] 證的用戶名。 |
| `password` | 連線至伺服器以進行驗 [!DNL ServiceNow] 證的密碼。 |

有關快速入門的詳細資訊，請參 [閱本ServiceNow檔案](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

要建立連接， [!DNL ServiceNow] 必須在中存 [!DNL ServiceNow] 在一組連接規範 [!DNL Flow Service]。 連接到的第一步 [!DNL Platform] 是 [!DNL ServiceNow] 檢索這些規範。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 向端點發送GET請求 `/connectionSpecs` 將返回所有可用源的連接規範。 您也可以包含查詢， `property=name=="service-now"` 以取得特定的資訊 [!DNL ServiceNow]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**請求**

以下請求將檢索的連接規範 [!DNL ServiceNow]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回的連接規範 [!DNL ServiceNow]，包括其唯一標識符(`id`)。 在下個步驟中需要此ID才能建立基本連線。

```json
{
    "items": [
        {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "name": "service-now",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to ServiceNow server",
                        "properties": {
                            "endpoint": {
                                "type": "string",
                                "description": "The endpoint of the ServiceNow server (http://<instance>.service-now.com)."
                            },
                            "username": {
                                "type": "string",
                                "description": "The user name used to connect to the ServiceNow server for authentication."
                            },
                            "password": {
                                "type": "string",
                                "description": "password to connect to the ServiceNow server for authentication.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "endpoint",
                            "username",
                            "password"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個帳戶只需要一個基本連 [!DNL ServiceNow] 接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "name": "Base connection for service-now",
        "description": "Base connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | 伺服器的端 [!DNL ServiceNow] 點。 |
| `auth.params.username` | 用於連接到伺服器以進行驗 [!DNL ServiceNow] 證的用戶名。 |
| `auth.params.password` | 連線至伺服器以進行驗 [!DNL ServiceNow] 證的密碼。 |
| `connectionSpec.id` | 與關聯的連接規範ID [!DNL ServiceNow]。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步中探索您的CRM時，需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

在本教學課程中，您已使用 [!DNL ServiceNow][!DNL Flow Service] API建立基本連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此基本連線ID，學習如 [何使用Flow Service API來探索客戶成功系統](../../explore/customer-success.md)。