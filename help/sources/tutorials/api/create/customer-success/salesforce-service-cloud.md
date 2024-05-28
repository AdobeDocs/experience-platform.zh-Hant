---
title: 使用流量服務API建立Salesforce Service雲端來源連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# 建立 [!DNL Salesforce Service Cloud] 來源連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程以瞭解如何建立基本連線，用於 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供對單一區域進行分割的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需的其他資訊 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集必要的認證

此 [!DNL Salesforce Service Cloud] 來源支援基本驗證和OAuth2使用者端認證。

>[!BEGINTABS]

>[!TAB 基本驗證]

連線您的 [!DNL Salesforce Service Cloud] 帳戶至 [!DNL Flow Service] 使用基本驗證，提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 來源執行個體。 |
| `username` | 的使用者名稱 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `password` | 的密碼 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `securityToken` | 的安全性權杖 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `apiVersion` | （選用）的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的例項。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本 `52`，則您必須輸入值為 `52.0`. 如果此欄位留空，Experience Platform將自動使用最新可用版本。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Salesforce Service Cloud] 為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

如需開始使用的詳細資訊，請造訪 [此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2使用者端認證]

連線您的 [!DNL Salesforce Service Cloud] 帳戶至 [!DNL Flow Service] 使用OAuth 2使用者端認證，提供下列認證的值：

| 認證 | 說明 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 來源執行個體。 |
| `clientId` | 使用者端ID會與使用者端密碼搭配使用，作為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過識別您的應用程式來代表您的帳戶運作。 [!DNL Salesforce Service Cloud]. |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，做為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過識別您的應用程式來代表您的帳戶運作。 [!DNL Salesforce Service Cloud]. |
| `apiVersion` | 的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的例項。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本 `52`，則您必須輸入值為 `52.0`. 如果此欄位留空，Experience Platform將自動使用最新可用版本。 此值是OAuth2使用者端認證驗證的必要專案。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Salesforce Service Cloud] 為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

如需為使用OAuth的詳細資訊 [!DNL Salesforce Service Cloud]，閱讀 [[!DNL Salesforce Service Cloud] OAuth授權流程指南](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Salesforce Service Cloud] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 基本驗證]

下列要求會建立 [!DNL Salesforce Service Cloud] 使用基本驗證：

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
| `auth.params.environmentUrl` | 您的URL [!DNL Salesforce Service Cloud] 執行個體。 |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.securityToken` | 與您的關聯的安全性權杖 [!DNL Salesforce Service Cloud] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 連線規格ID： `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2使用者端認證]

下列要求會建立 [!DNL Salesforce Service Cloud] 使用OAuth 2使用者端認證：

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
| `auth.params.environmentUrl` | 您的URL [!DNL Salesforce Service Cloud] 執行個體。 |
| `auth.params.clientId` | 與您的關聯的使用者端ID [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.clientSecret` | 與您的關聯的使用者端密碼 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.apiVersion` | 的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的例項。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 連線規格ID： `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

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

依照本教學課程，您已建立 [!DNL Salesforce Service Cloud] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用將客戶成功資料匯入Platform [!DNL Flow Service] API](../../collect/customer-success.md)
