---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: 使用Flow Service API建立Microsoft Dynamics連接器
topic: overview
description: 本教學課程使用Flow Service API來引導您完成將平台連接至Microsoft Dynamics（以下稱為「Dynamics」）帳戶以收集CRM資料的步驟。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# 使用 [!DNL Microsoft Dynamics] API建立連 [!DNL Flow Service] 接器

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至 [!DNL Platform][!DNL Microsoft Dynamics] （以下稱為「Dynamics」）帳戶以收集CRM資料的步驟。

如果您想要在中使用使用者介面 [!DNL Experience Platform], [](../../../ui/create/crm/dynamics.md) Dynamics來源連接器UI教學課程會提供執行類似動作的逐步指示。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md):E[!DNL xperience Platform] 提供虛擬沙盒，可將單一執行個體分割 [!DNL Platform] 成不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL Platform] API成功連線至Dynamics帳 [!DNL Flow Service] 戶。

### 收集必要的認證

要連接 [!DNL Flow Service] 到，必須 [!DNL Dynamics]為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUri` | 您實例的服務 [!DNL Dynamics] URL。 |
| `username` | 您使用者帳戶的 [!DNL Dynamics] 使用者名稱。 |
| `password` | 您帳戶的密 [!DNL Dynamics] 碼。 |

如需快速入門的詳細資訊，請造訪 [此Dynamics檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 查找連接規格

在連接 [!DNL Platform] 到帳 [!DNL Dynamics] 戶之前，必須驗證是否存在連接規範 [!DNL Dynamics]。 如果連接規範不存在，則無法建立連接。

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 您可以執行GET請求並使 [!DNL Dynamics] 用查詢參數，查找連接規範。

**API格式**

傳送不含查詢參數的GET請求時，會傳回所有可用來源的連線規格。 您可以包含查詢， `property=name=="dynamics-online"` 以取得特定的資訊 [!DNL Dynamics]。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**請求**

以下請求將檢索的連接規範 [!DNL Dynamics]。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回的連接規範 [!DNL Dynamics]，包括其唯一標識符(`id`)。 在下個步驟中需要此ID才能建立基本連線。

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 建立基本連接

基本連接指定源，並包含該源的憑據。 每個帳戶只需要一個基本連 [!DNL Dynamics] 接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的實例關聯的服務 [!DNL Dynamics] URI。 |
| `auth.params.username` | 與您帳戶關聯的使用 [!DNL Dynamics] 者名稱。 |
| `auth.params.password` | 與您帳戶關聯的 [!DNL Dynamics] 密碼。 |
| `connectionSpec.id` | 在上一步 `id` 中檢索 [!DNL Dynamics] 的帳戶的連接規範。 |

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 後續步驟

在本教學課程中，您已使用API為您的帳戶建立基 [!DNL Dynamics] 本連線，而且已取得唯一ID作為回應內文的一部分。 在下一個教學課程中，您可以使用此基本連線ID，同時學習如 [何使用Flow Service API來探索CRM系統](../../explore/crm.md)。