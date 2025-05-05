---
title: 使用流量服務API建立Salesforce Service Cloud Source連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]來源連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Salesforce Service Cloud]建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Salesforce Service Cloud]。

### 收集必要的認證

[!DNL Salesforce Service Cloud]來源支援基本驗證和OAuth2使用者端認證。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用基本驗證將您的[!DNL Salesforce Service Cloud]帳戶連線到[!DNL Flow Service]，請提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce Service Cloud]來源執行個體的網址。 |
| `username` | [!DNL Salesforce Service Cloud]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Salesforce Service Cloud]使用者帳戶的密碼。 |
| `securityToken` | [!DNL Salesforce Service Cloud]使用者帳戶的安全性權杖。 |
| `apiVersion` | （選用）您正在使用的[!DNL Salesforce Service Cloud]執行個體的REST API版本。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本`52`，則必須以`52.0`的形式輸入值。 如果此欄位留空，Experience Platform會自動使用最新可用版本。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Salesforce Service Cloud]的連線規格識別碼為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

如需開始使用的詳細資訊，請瀏覽[此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

>[!TAB OAuth 2使用者端認證]

若要使用OAuth 2使用者端認證將您的[!DNL Salesforce Service Cloud]帳戶連線至[!DNL Flow Service]，請提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce Service Cloud]來源執行個體的網址。 |
| `clientId` | 使用者端ID會與使用者端密碼搭配使用，作為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce Service Cloud]識別您的應用程式，以代表您的帳戶運作。 |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，做為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce Service Cloud]識別您的應用程式，以代表您的帳戶運作。 |
| `apiVersion` | 您正在使用的[!DNL Salesforce Service Cloud]執行個體的REST API版本。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本`52`，則必須以`52.0`的形式輸入值。 如果此欄位留空，Experience Platform會自動使用最新可用版本。 此值是OAuth2使用者端認證驗證的必要專案。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Salesforce Service Cloud]的連線規格識別碼為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

如需針對[!DNL Salesforce Service Cloud]使用OAuth的詳細資訊，請參閱OAuth授權流程[&#128279;](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5)的[!DNL Salesforce Service Cloud] 指南。

>[!ENDTABS]

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Salesforce Service Cloud]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 基本驗證]

下列要求使用基本驗證建立[!DNL Salesforce Service Cloud]的基本連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| ---| --- |
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud]執行個體的URL。 |
| `auth.params.username` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL Salesforce Service Cloud]帳戶關聯的密碼。 |
| `auth.params.securityToken` | 與您的[!DNL Salesforce Service Cloud]帳戶關聯的安全性權杖。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]連線規格識別碼： `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2使用者端認證]

以下要求使用OAuth 2使用者端認證為[!DNL Salesforce Service Cloud]建立基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
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
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud]執行個體的URL。 |
| `auth.params.clientId` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者端密碼。 |
| `auth.params.apiVersion` | 您正在使用的[!DNL Salesforce Service Cloud]執行個體的REST API版本。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]連線規格識別碼： `cb66ab34-8619-49cb-96d1-39b37ede86ea`。 |

>[!ENDTABS]

**回應**

成功的回應會傳回您新建立的基本連線及其唯一ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流，將客戶成功資料匯入Experience Platform](../../collect/customer-success.md)
