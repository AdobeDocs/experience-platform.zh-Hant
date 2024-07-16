---
title: 使用流量服務API建立Salesforce基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Salesforce帳戶。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立[!DNL Salesforce]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Salesforce]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線[!DNL Platform]至[!DNL Salesforce]帳戶。

### 收集必要的認證

[!DNL Salesforce]來源支援基本驗證和OAuth2使用者端認證。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用基本驗證將您的[!DNL Salesforce]帳戶連線到[!DNL Flow Service]，請提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce]來源執行個體的網址。 |
| `username` | [!DNL Salesforce]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Salesforce]使用者帳戶的密碼。 |
| `securityToken` | [!DNL Salesforce]使用者帳戶的安全性權杖。 |
| `apiVersion` | 選用性)您正在使用的[!DNL Salesforce]執行個體的REST API版本。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本`52`，則必須以`52.0`的形式輸入值。 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Salesforce]的連線規格識別碼為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

如需開始使用的詳細資訊，請瀏覽[此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

>[!TAB OAuth 2使用者端認證]

若要使用OAuth 2使用者端認證將您的[!DNL Salesforce]帳戶連線至[!DNL Flow Service]，請提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce]來源執行個體的網址。 |
| `clientId` | 使用者端ID會與使用者端密碼搭配使用，作為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce]識別您的應用程式，以代表您的帳戶運作。 |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，做為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce]識別您的應用程式，以代表您的帳戶運作。 |
| `apiVersion` | 您正在使用的[!DNL Salesforce]執行個體的REST API版本。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本`52`，則必須以`52.0`的形式輸入值。 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 此值是OAuth2使用者端認證驗證的必要專案。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Salesforce]的連線規格識別碼為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

如需針對[!DNL Salesforce]使用OAuth的詳細資訊，請參閱OAuth授權流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5)的[[!DNL Salesforce] 指南。

>[!ENDTABS]

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請向`/connections`端點發出POST要求，並在要求內文中提供您的[!DNL Salesforce]驗證認證。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 基本驗證]

下列要求使用基本驗證建立[!DNL Salesforce]的基本連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce]執行個體的URL。 |
| `auth.params.username` | 與您的[!DNL Salesforce]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL Salesforce]帳戶關聯的密碼。 |
| `auth.params.securityToken` | 與您的[!DNL Salesforce]帳戶關聯的安全性權杖。 |
| `connectionSpec.id` | [!DNL Salesforce]連線規格識別碼： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

>[!TAB OAuth 2使用者端認證]

以下要求使用OAuth 2使用者端認證為[!DNL Salesforce]建立基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce]執行個體的URL。 |
| `auth.params.clientId` | 與您的[!DNL Salesforce]帳戶相關聯的使用者端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL Salesforce]帳戶相關聯的使用者端密碼。 |
| `auth.params.apiVersion` | 您正在使用的[!DNL Salesforce]執行個體的REST API版本。 |
| `connectionSpec.id` | [!DNL Salesforce]連線規格識別碼： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

>[!ENDTABS]

**回應**

成功的回應會傳回您新建立的基本連線及其唯一ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Salesforce]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將CRM資料帶入Platform](../../collect/crm.md)
