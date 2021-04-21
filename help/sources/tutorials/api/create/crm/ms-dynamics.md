---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: 使用Flow Service API建立Microsoft Dynamics Source連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Platform連線至Microsoft Dynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]來源連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成使用Flow Service API將平台連接至[!DNL Microsoft Dynamics]（以下稱為「Dynamics」）帳戶的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API將平台成功連線至Dynamics帳戶。

### 收集必要的認證

要使[!DNL Flow Service]連接到[!DNL Dynamics]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]實例的服務URL。 |
| `username` | [!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Dynamics]帳戶的密碼。 |
| `servicePrincipalId` | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `servicePrincipalKey` | 服務主機密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

有關入門的詳細資訊，請造訪[this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Dynamics]帳戶只需要一個連接，因為它可用於建立多個資料流以導入不同的資料。

### 使用基本驗證建立[!DNL Dynamics]連接

要使用基本驗證建立[!DNL Dynamics]連接，請向[!DNL Flow Service] API發出POST請求，同時為連接的`serviceUri`、`username`和`password`提供值。

**API格式**

```http
POST /connections
```

**要求**

要建立[!DNL Dynamics]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Dynamics]的連接規範ID為`38ad80fe-8b06-4938-94f4-d4ee80266b07`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
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
| `auth.params.serviceUri` | 與[!DNL Dynamics]實例關聯的服務URI。 |
| `auth.params.username` | 與[!DNL Dynamics]帳戶關聯的使用者名稱。 |
| `auth.params.password` | 與[!DNL Dynamics]帳戶關聯的密碼。 |
| `connectionSpec.id` | 在上一步中檢索的[!DNL Dynamics]帳戶的連接規範`id`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 使用基於服務主體密鑰的身份驗證建立[!DNL Dynamics]連接

要使用基於服務主體密鑰的身份驗證建立[!DNL Dynamics]連接，請向[!DNL Flow Service] API發出POST請求，同時為連接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
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
| `auth.params.serviceUri` | 與[!DNL Dynamics]實例關聯的服務URI。 |
| `auth.params.servicePrincipalId` | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主機密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Dynamics]連接，並獲取了該連接的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如何使用Flow Service API](../../explore/crm.md)來探索CRM系統。[
