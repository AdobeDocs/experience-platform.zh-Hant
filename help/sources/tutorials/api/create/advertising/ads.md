---
title: 使用流量服務API建立Google Ads基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連結至Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立Google Ads基本連線

>[!WARNING]
>
>[!DNL Google Ads]來源暫時無法使用。 Adobe正在努力解決此來源的問題。

>[!NOTE]
>
>Google Ads來源為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步帶您瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立Google Ads的基本連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到Google Ads。

### 收集必要的認證

為了讓[!DNL Flow Service]與Google Ads連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | 使用者端客戶ID為對應至您要使用Google Ads API管理的Google Ads使用者端帳戶的帳號。 此ID遵循`123-456-7890`的範本。 |
| `loginCustomerId` | 登入客戶ID是與您的Google Ads管理員帳戶對應的帳號，用於擷取特定營運客戶的報表資料。 如需登入客戶ID的詳細資訊，請參閱[Google Ads API檔案](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| `developerToken` | 開發人員Token可讓您存取Google Ads API。 您可以使用相同的開發人員Token，對所有Google Ads帳戶提出要求。 透過[登入您的管理員帳戶](https://ads.google.com/home/tools/manager-accounts/)，然後導覽至[!DNL API Center]頁面來擷取您的開發人員權杖。 |
| `refreshToken` | 重新整理權杖是[!DNL OAuth2]驗證的一部分。 此權杖可讓您在存取權杖過期後重新產生存取權杖。 |
| `clientId` | 使用者端ID與使用者端密碼搭配使用，是[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，作為[!DNL OAuth2]驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 Google Ads的連線規格ID是： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

閱讀API概觀檔案，以瞭解[開始使用Google Ads的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基礎連線ID，請在提供您的Google Ads驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

以下請求會建立Google Ads的基本連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | 您的Google Ads帳戶的使用者端客戶ID。 |
| `auth.params.loginCustomerID` | 與您的Google Ads管理員帳戶對應的登入客戶ID。 |
| `auth.params.developerToken` | 您的Google Ads帳戶的開發人員權杖。 |
| `auth.params.refreshToken` | Google Ads帳戶的重新整理Token。 |
| `auth.params.clientID` | 您的Google Ads帳戶的使用者端ID。 |
| `auth.params.clientSecret` | 您的Google Ads帳戶的使用者端密碼。 |
| `connectionSpec.id` | Google Ads連線規格識別碼： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立Google Ads基本連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將廣告資料帶入Platform](../../collect/advertising.md)
