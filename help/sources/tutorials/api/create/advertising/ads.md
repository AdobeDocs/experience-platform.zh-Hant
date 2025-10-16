---
title: 使用API將Google Ads連線至Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連結至Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: a0977e98219797eda14dd8d7ddb6cf3f1410cef0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 使用[!DNL Google Ads] API連線[!DNL Flow Service]至Experience Platform

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程，瞭解如何使用[!DNL Google Ads]API[[!DNL Flow Service] 將您的](https://developer.adobe.com/experience-platform-apis/references/flow-service/)帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Google Ads] API成功連線到[!DNL Flow Service]。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

### 收集必要的認證

如需驗證的詳細資訊，請閱讀[[!DNL Google Ads] 來源概觀](../../../../connectors/advertising/ads.md)。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基礎連線ID，請在提供您的Google Ads驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v19"

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
| `auth.params.clientCustomerID` | 您[!DNL Google Ads]帳戶的使用者端客戶識別碼。 |
| `auth.params.loginCustomerID` | 與您的[!DNL Google Ads]管理員帳戶對應的登入客戶識別碼。 |
| `auth.params.developerToken` | 您[!DNL Google Ads]帳戶的開發人員權杖。 |
| `auth.params.refreshToken` | 您[!DNL Google Ads]帳戶的重新整理權杖。 |
| `auth.params.clientID` | 您[!DNL Google Ads]帳戶的使用者端識別碼。 |
| `auth.params.clientSecret` | 您[!DNL Google Ads]帳戶的使用者端密碼。 |
| `auth.params.googleAdsApiVersion` | 您正在使用的[!DNL Google Ads] API版本。 Experience Platform目前支援版本`v19`和更新版本。 請確定您使用其中一個支援的版本，以確保相容性。 |
| `connectionSpec.id` | [!DNL Google Ads]連線規格識別碼： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 建立資料流以擷取廣告資料

依照此教學課程，您已使用[!DNL Google Ads] API建立[!DNL Flow Service]基本連線，並將您的[!DNL Google Ads]帳戶連線至Experience Platform。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將廣告資料帶入Experience Platform](../../collect/advertising.md)
