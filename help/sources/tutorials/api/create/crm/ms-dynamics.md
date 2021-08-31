---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 使用流服務API建立Microsoft Dynamics基連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Platform連線至Microsoft Dynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Microsoft Dynamics]基本連線（以下稱為「[!DNL Dynamics]」）的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功將Platform連接到Dynamics帳戶。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL Dynamics]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]實例的服務URL。 |
| `username` | [!DNL Dynamics]用戶帳戶的用戶名。 |
| `password` | [!DNL Dynamics]帳戶的密碼。 |
| `servicePrincipalId` | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Dynamics]的連接規範ID為：`38ad80fe-8b06-4938-94f4-d4ee80266b07`。 |

有關入門的詳細資訊，請訪問[this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Dynamics]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

### 使用基本身份驗證建立[!DNL Dynamics]基本連接

若要使用基本驗證建立[!DNL Dynamics]基本連線，請向[!DNL Flow Service] API發出POST請求，同時提供連線的`serviceUri`、`username`和`password`值。

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
| `auth.params.username` | 與您的[!DNL Dynamics]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與[!DNL Dynamics]帳戶相關聯的密碼。 |
| `connectionSpec.id` | [!DNL Dynamics]連接規範ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 使用基於服務主體密鑰的身份驗證建立[!DNL Dynamics]基本連接

要使用基於服務主體密鑰的身份驗證建立[!DNL Dynamics]基本連接，請向[!DNL Flow Service] API發出POST請求，同時為連接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

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
| `auth.params.servicePrincipalId` | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的驗證時，需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |
| `connectionSpec.id` | [!DNL Dynamics]連接規範ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Dynamics]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/crm.md)探索CRM系統時，您可以在下一個教學課程中使用此ID。[
