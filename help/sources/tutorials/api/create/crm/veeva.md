---
keywords: Experience Platform；首頁；熱門主題；veeva crm; Veeva CRM; Veeva;
solution: Experience Platform
title: 使用流程服務API建立Veva CRM基本連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Veeva CRM。
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# （測試版）使用[!DNL Flow Service] API建立[!DNL Veeva CRM]基本連線

>[!NOTE]
>
>[!DNL Veeva CRM]源位於測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Veeva CRM]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Veeva CRM]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Veeva CRM]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]實例的URL。 |
| `username` | [!DNL Veeva CRM]帳戶的用戶名值。 |
| `password` | [!DNL Veeva CRM]帳戶的密碼值。 |
| `securityToken` | [!DNL Veeva CRM]實例的安全令牌。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Veeva CRM]的連接規範ID為：`fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

有關這些值的詳細資訊，請參閱此[[!DNL Veeva CRM] document](https://developer.veevacrm.com/api/#order-management-rest-api)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Veeva CRM]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Veeva CRM]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | [!DNL Veeva CRM]基本連接的名稱。 您可以使用此名稱來查找[!DNL Veeva CRM]基本連接。 |
| `description` | [!DNL Veeva CRM]基本連接的可選說明。 |
| `auth.specName` | 用於連接的驗證類型。 |
| `auth.params.environmentUrl` | [!DNL Veeva CRM]實例的URL。 |
| `auth.params.username` | [!DNL Veeva CRM]帳戶的用戶名值。 |
| `auth.params.password` | [!DNL Veeva CRM]帳戶的密碼值。 |
| `auth.params.securityToken` | [!DNL Veeva CRM]實例的安全令牌。 |
| `connectionSpec.id` | [!DNL Veeva CRM]的連接規範ID:`fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Veeva CRM]基本連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/crm.md)探索CRM系統時，您可以在下一個教學課程中使用此ID。[
