---
keywords: Experience Platform；首頁；熱門主題；veeva crm；Veeva CRM；Veeva；
solution: Experience Platform
title: 使用流量服務API建立Veeva CRM基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連結至Veeva CRM。
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Veeva CRM]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Veeva CRM]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Veeva CRM]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Veeva CRM]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]執行個體的URL。 |
| `username` | 您[!DNL Veeva CRM]帳戶的使用者名稱值。 |
| `password` | [!DNL Veeva CRM]帳戶的密碼值。 |
| `securityToken` | 您的[!DNL Veeva CRM]執行個體的安全性權杖。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Veeva CRM]的連線規格識別碼為： `fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

如需這些值的詳細資訊，請參閱此[[!DNL Veeva CRM] 檔案](https://developer.veevacrm.com/doc/Content/rest-api.htm)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Veeva CRM]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Veeva CRM]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | [!DNL Veeva CRM]基本連線的名稱。 您可以使用此名稱來查閱您的[!DNL Veeva CRM]基礎連線。 |
| `description` | 您的[!DNL Veeva CRM]基礎連線的選擇性描述。 |
| `auth.specName` | 用於連線的驗證型別。 |
| `auth.params.environmentUrl` | [!DNL Veeva CRM]執行個體的URL。 |
| `auth.params.username` | 您[!DNL Veeva CRM]帳戶的使用者名稱值。 |
| `auth.params.password` | [!DNL Veeva CRM]帳戶的密碼值。 |
| `auth.params.securityToken` | 您的[!DNL Veeva CRM]執行個體的安全性權杖。 |
| `connectionSpec.id` | [!DNL Veeva CRM]的連線規格識別碼： `fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Veeva CRM]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將CRM資料帶入Platform](../../collect/crm.md)
