---
keywords: Experience Platform；主題；熱門主題；一般REST；一般靜止
solution: Experience Platform
title: 使用流服務API建立通用REST API基連接
type: Tutorial
description: 瞭解如何使用流服務API將通用REST API連接到Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Generic REST API] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Generic REST API] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Generic REST API]，必須為所選的身份驗證類型提供有效的憑據。 [!DNL Generic REST API] 支援OAuth 2刷新代碼和基本身份驗證。 有關兩種支援的身份驗證類型的憑據的資訊，請參見下表。

#### OAuth 2刷新代碼

| 憑據 | 說明 |
| --- | --- |
| `host` | 向其請求的源的主機URL。 此值是必需的，無法使用 `requestParameterOverride`。 |
| `authorizationTestUrl` | （可選）授權testURL用於在建立基連接時驗證憑據。 如果未提供，則在建立源連接步驟期間會自動檢查憑據。 |
| `clientId` | （可選）與您的用戶帳戶關聯的客戶端ID。 |
| `clientSecret` | （可選）與您的用戶帳戶關聯的客戶端密碼。 |
| `accessToken` | 用於訪問應用程式的主身份驗證憑據。 訪問令牌表示應用程式訪問用戶資料的特定方面的授權。 此值是必需的，無法使用 `requestParameterOverride`。 |
| `refreshToken` | （可選）當訪問令牌過期時用於生成新訪問令牌的令牌。 |
| `expirationDate` | （可選）定義訪問令牌的到期日期的隱藏值。 |
| `accessTokenUrl` | （可選）用於獲取訪問令牌的URL終結點。 |
| `requestParameterOverride` | （可選）允許指定要覆蓋的憑據參數的屬性。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |

#### 基本身份驗證

| 憑據 | 說明 |
| --- | --- |
| `host` | 向其請求的源的主機URL。 |
| `username` | 與您的用戶帳戶對應的用戶名。 |
| `password` | 與您的用戶帳戶對應的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

[!DNL Generic REST API] 支援基本身份驗證和OAuth 2刷新代碼。 有關如何使用兩種身份驗證類型進行身份驗證的指導，請參見以下示例。

### 建立 [!DNL Generic REST API] 使用OAuth 2刷新代碼的基連接

要使用OAuth 2刷新代碼建立基本連接ID，請向 `/connections` 提供OAuth 2憑據時的終結點。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Generic REST API]:

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
| `name` | 基本連接的名稱。 確保基本連接的名稱是描述性的，因為您可以使用此名稱查找有關基本連接的資訊。 |
| `description` | （可選）可包含的屬性，用於提供有關基本連接的詳細資訊。 |
| `connectionSpec.id` | 與關聯的連接規範ID [!DNL Generic REST API]。 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |
| `auth.specName` | 用於將源驗證到平台的驗證類型。 |
| `auth.params.host` | 用於連接到您的 [!DNL Generic REST API] 源。 |
| `auth.params.accessToken` | 用於驗證源的相應訪問令牌。 這是基於OAuth的身份驗證所必需的。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 建立 [!DNL Generic REST API] 基本連接使用基本認證

建立 [!DNL Generic REST API] 基本連接使用基本身份驗證，向POST請求 `/connections` 端點 [!DNL Flow Service] API，同時提供基本身份驗證憑據。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Generic REST API]:

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
| `name` | 基本連接的名稱。 確保基本連接的名稱是描述性的，因為您可以使用此名稱查找有關基本連接的資訊。 |
| `description` | （可選）可包含的屬性，用於提供有關基本連接的詳細資訊。 |
| `connectionSpec.id` | 與關聯的連接規範ID [!DNL Generic REST API]。 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`。 |
| `auth.specName` | 用於將源連接到平台的身份驗證類型。 |
| `auth.params.host` | 用於連接到您的 [!DNL Generic REST API] 源。 |
| `auth.params.username` | 與您的 [!DNL Generic REST API] 源。 這是基本身份驗證所必需的。 |
| `auth.params.password` | 與您的 [!DNL Generic REST API] 源。 這是基本身份驗證所必需的。 |

**回應**

成功的響應返回新建立的基本連接，包括其唯一連接標識符(`id`)。 在下一步中瀏覽源的檔案結構和內容需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Generic REST API] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/protocols.md)
