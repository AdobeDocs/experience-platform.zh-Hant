---
keywords: Experience Platform；首頁；熱門主題；Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: 使用流服務API建立Salesforce Service Cloud源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]源連接

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Salesforce Service Cloud]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Salesforce Service Cloud]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Salesforce Service Cloud]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `username` | [!DNL Salesforce Service Cloud]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Salesforce Service Cloud]帳戶的密碼。 |
| `securityToken` | [!DNL Salesforce Service Cloud]帳戶的安全令牌。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Salesforce Service Cloud]的連接規範ID為：`b66ab34-8619-49cb-96d1-39b37ede86ea`。 |

有關入門的詳細資訊，請參閱[此Salesforce Service Cloud文檔](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Salesforce Service Cloud]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL Salesforce Service Cloud]建立基本連接：

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
| `auth.params.username` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與[!DNL Salesforce Service Cloud]帳戶相關聯的密碼。 |
| `auth.params.securityToken` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的安全令牌。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]連接規範ID:`b66ab34-8619-49cb-96d1-39b37ede86ea` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/customer-success.md)探索客戶成功系統時，您可以在下一個教學課程中使用此連線ID。[
