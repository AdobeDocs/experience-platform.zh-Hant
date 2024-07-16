---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般Rest
solution: Experience Platform
title: 使用流程服務API建立一般REST API基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Generic REST API連線至Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立一般REST API基底連線

>[!NOTE]
>
>[!DNL Generic REST API]來源是測試版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Generic REST API]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Generic REST API]連線，您必須為您選擇的驗證型別提供有效的認證。 [!DNL Generic REST API]同時支援OAuth 2重新整理程式碼和基本驗證。 請參閱下清單格，瞭解兩種支援的驗證型別之證明資料的資訊。

#### OAuth 2重新整理代碼

| 認證 | 說明 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 此值為必要項，無法使用`requestParameterOverride`略過。 |
| `authorizationTestUrl` | （選用）建立基本連線時，授權測試URL會用於驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| `clientId` | （選用）與您的使用者帳戶相關聯的使用者端ID。 |
| `clientSecret` | （選用）與您的使用者帳戶相關聯的使用者端密碼。 |
| `accessToken` | 用來存取應用程式的主要驗證認證。 存取權杖代表應用程式的授權，可存取使用者資料的特定方面。 此值為必要項，無法使用`requestParameterOverride`略過。 |
| `refreshToken` | （選用）當存取權杖過期時，用來產生新存取權杖的權杖。 |
| `expirationDate` | （選用）定義存取Token到期日的隱藏值。 |
| `accessTokenUrl` | （選用）用來擷取存取權杖的URL端點。 |
| `requestParameterOverride` | （選擇性）屬性，可讓您指定要覆寫哪些認證引數。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Generic REST API]的連線規格識別碼為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |

#### 基本驗證

| 認證 | 說明 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 |
| `username` | 與您的使用者帳戶對應的使用者名稱。 |
| `password` | 與您的使用者帳戶對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Generic REST API]的連線規格識別碼為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

[!DNL Generic REST API]支援基本驗證和OAuth 2重新整理程式碼。 請參閱下列範例，以取得如何使用任一驗證型別進行驗證的指引。

### 使用OAuth 2重新整理程式碼建立[!DNL Generic REST API]基本連線

若要使用OAuth 2重新整理程式碼建立基本連線ID，請在提供您的OAuth 2認證時，向`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Generic REST API]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）可包含的屬性，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 與[!DNL Generic REST API]關聯的連線規格識別碼。 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |
| `auth.specName` | 您用來向Platform驗證來源的驗證型別。 |
| `auth.params.host` | 用來連線至您[!DNL Generic REST API]來源的根URL。 |
| `auth.params.accessToken` | 用來驗證來源的對應存取權杖。 這是OAuth型驗證的必要專案。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 使用基本驗證建立[!DNL Generic REST API]基本連線

若要使用基本驗證建立[!DNL Generic REST API]基本連線，請在提供基本驗證認證時，向[!DNL Flow Service] API的`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Generic REST API]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）可包含的屬性，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 與[!DNL Generic REST API]關聯的連線規格識別碼。 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |
| `auth.specName` | 您用來將來源連線到Platform的驗證型別。 |
| `auth.params.host` | 用來連線至您[!DNL Generic REST API]來源的根URL。 |
| `auth.params.username` | 與您的[!DNL Generic REST API]來源對應的使用者名稱。 這是基本驗證的必要專案。 |
| `auth.params.password` | 與您的[!DNL Generic REST API]來源對應的密碼。 這是基本驗證的必要專案。 |

**回應**

成功的回應會傳回新建立的基礎連線，包括其唯一的連線識別碼(`id`)。 在下一步中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Generic REST API]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將通訊協定資料帶入Platform](../../collect/protocols.md)
