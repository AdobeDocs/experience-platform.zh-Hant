---
title: 使用流程服務API建立Google Ads基本連線
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 7c77b0dc658ad45a25f4ead4e14f5826701cf645
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 使用建立Google Ads基本連線 [!DNL Flow Service] API

>[!NOTE]
>
>Google廣告來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Experience Platform例項分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 若要與Google Ads連線，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | 用戶端客戶ID是與您要透過Google Ads API管理之Google Ads用戶端帳戶對應的帳號。 此ID會遵循 `123-456-7890`. |
| `loginCustomerId` | 登入客戶ID是與您的Google Ads管理員帳戶對應的帳號，用於從特定作業客戶擷取報表資料。 如需登入客戶ID的詳細資訊，請參閱 [Google Ads API檔案](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| `developerToken` | 開發人員代號可讓您存取Google Ads API。 您可以使用相同的開發人員代號，對您的所有Google Ads帳戶提出要求。 擷取開發人員代號，方法為 [登入您的經理帳戶](https://ads.google.com/home/tools/manager-accounts/) 然後導覽至 [!DNL API Center] 頁面。 |
| `refreshToken` | 重新整理代號是 [!DNL OAuth2] 驗證。 此Token可讓您在存取Token過期後重新產生存取Token。 |
| `clientId` | 用戶端ID會與用戶端密碼一併用於 [!DNL OAuth2] 驗證。 用戶端ID和用戶端密碼可搭配使用，將您的應用程式識別至Google，以代表您的帳戶運作。 |
| `clientSecret` | 用戶端密碼會與用戶端ID搭配使用，作為 [!DNL OAuth2] 驗證。 用戶端ID和用戶端密碼可搭配使用，將您的應用程式識別至Google，以代表您的帳戶運作。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 Google廣告的連線規格ID為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

請參閱API概觀檔案，以取得 [開始使用Google Ads的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點，同時提供Google Ads驗證憑證作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為Google Ads建立基本連線：

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
| `auth.params.clientCustomerID` | Google Ads帳戶的用戶端客戶ID。 |
| `auth.params.loginCustomerID` | 與您的Google Ads經理帳戶對應的登入客戶ID。 |
| `auth.params.developerToken` | Google Ads帳戶的開發人員代號。 |
| `auth.params.refreshToken` | Google Ads帳戶的重新整理Token。 |
| `auth.params.clientID` | Google Ads帳戶的用戶端ID。 |
| `auth.params.clientSecret` | Google Ads帳戶的用戶端密碼。 |
| `connectionSpec.id` | Google Ads連接規範ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照本教學課程，您已使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/advertising.md)
