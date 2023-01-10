---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般REST
solution: Experience Platform
title: 使用流程服務API建立一般REST API基本連線
type: Tutorial
description: 了解如何使用流量服務API將一般REST API連線至Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 使用建立一般REST API基本連線 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Generic REST API] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Generic REST API] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Generic REST API]，您必須為您選擇的驗證類型提供有效憑證。 [!DNL Generic REST API] 支援OAuth 2重新整理程式碼和基本驗證。 有關兩種受支援身份驗證類型的憑據的資訊，請參閱下表。

#### OAuth 2重新整理程式碼

| 憑據 | 說明 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 此值為必要值，無法使用 `requestParameterOverride`. |
| `authorizationTestUrl` | （可選）建立基本連線時，授權測試URL用於驗證憑證。 如果未提供，則在建立源連接步驟期間將自動檢查憑據。 |
| `clientId` | （選用）與您的使用者帳戶相關聯的用戶端ID。 |
| `clientSecret` | （選用）與您的使用者帳戶相關聯的用戶端密碼。 |
| `accessToken` | 用於訪問應用程式的主身份驗證憑據。 存取權杖代表您應用程式存取使用者資料之特定方面的授權。 此值為必要值，無法使用 `requestParameterOverride`. |
| `refreshToken` | （選用）存取權杖過期時用來產生新存取權杖的權杖。 |
| `expirationDate` | （選用）定義存取權杖到期日的隱藏值。 |
| `accessTokenUrl` | （選用）用來擷取存取權杖的URL端點。 |
| `requestParameterOverride` | （可選）可讓您指定要覆寫的憑證參數的屬性。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### 基本驗證

| 憑據 | 說明 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 |
| `username` | 與您的使用者帳戶對應的使用者名稱。 |
| `password` | 與您的使用者帳戶對應的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

[!DNL Generic REST API] 支援基本驗證和OAuth 2重新整理程式碼。 如需如何使用任一驗證類型進行驗證的指引，請參閱下列範例。

### 建立 [!DNL Generic REST API] 使用OAuth 2重新整理程式碼進行基本連線

若要使用OAuth 2重新整理程式碼來建立基本連線ID，請向 `/connections` 端點，同時提供您的OAuth 2憑證。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL Generic REST API]:

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
| `name` | 基本連接的名稱。 請確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供有關基本連線的詳細資訊。 |
| `connectionSpec.id` | 與關聯的連接規範ID [!DNL Generic REST API]. 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 用於向平台驗證源的驗證類型。 |
| `auth.params.host` | 用來連線至您 [!DNL Generic REST API] 來源。 |
| `auth.params.accessToken` | 用於驗證源的相應訪問令牌。 這是OAuth型驗證的必要項目。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 建立 [!DNL Generic REST API] 基本驗證

建立 [!DNL Generic REST API] 基本連接使用基本身份驗證，向POST請求 `/connections` 端點 [!DNL Flow Service] API，同時提供基本驗證憑證。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Generic REST API]:

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
| `name` | 基本連接的名稱。 請確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供有關基本連線的詳細資訊。 |
| `connectionSpec.id` | 與關聯的連接規範ID [!DNL Generic REST API]. 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 用於將源連接到平台的驗證類型。 |
| `auth.params.host` | 用來連線至您 [!DNL Generic REST API] 來源。 |
| `auth.params.username` | 與您的 [!DNL Generic REST API] 來源。 這是基本驗證的必要條件。 |
| `auth.params.password` | 與您的 [!DNL Generic REST API] 來源。 這是基本驗證的必要條件。 |

**回應**

成功的響應返回新建的基本連接，包括其唯一連接標識符(`id`)。 在下一步中，瀏覽源的檔案結構和內容時需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Generic REST API] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用將通訊協定資料帶入Platform [!DNL Flow Service] API](../../collect/protocols.md)
