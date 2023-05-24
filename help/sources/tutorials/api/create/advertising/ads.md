---
title: 使用流服務API建立Google廣告基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform與Google廣告連接。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 7c77b0dc658ad45a25f4ead4e14f5826701cf645
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

>[!NOTE]
>
>Google廣告的來源是β 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將引導您完成使用以下工具為Google廣告建立基本連接的步驟： [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用Experience Platform服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個Experience Platform實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 要連接Google廣告，必須提供以下連接屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | 客戶端客戶ID是與您要使用Google廣告API管理的Google廣告客戶端帳戶對應的帳號。 此ID位於的模板後 `123-456-7890`。 |
| `loginCustomerId` | 登錄客戶ID是與您的Google廣告經理帳戶相對應的帳號，用於從特定操作客戶獲取報告資料。 有關登錄客戶ID的詳細資訊，請閱讀 [Google廣告API文檔](https://developers.google.com/google-ads/api/docs/migration/login-customer-id)。 |
| `developerToken` | 開發人員令牌允許您訪問Google廣告API。 您可以使用同一開發人員令牌對所有Google廣告帳戶發出請求。 檢索開發人員令牌的方式 [登錄到您的Manager帳戶](https://ads.google.com/home/tools/manager-accounts/) 然後導航到 [!DNL API Center] 的子菜單。 |
| `refreshToken` | 刷新令牌是 [!DNL OAuth2] 驗證。 此令牌允許您在訪問令牌過期後重新生成它們。 |
| `clientId` | 客戶機ID與客戶機密碼一起使用，作為 [!DNL OAuth2] 驗證。 客戶端ID和客戶端密碼共同使您的應用程式能夠代表您的帳戶運行，方法是將您的應用程式標識到Google。 |
| `clientSecret` | 客戶機密碼與客戶機ID一起用作 [!DNL OAuth2] 驗證。 客戶端ID和客戶端密碼共同使您的應用程式能夠代表您的帳戶運行，方法是將您的應用程式標識到Google。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 Google廣告的連接規範ID為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

閱讀API概述文檔 [有關開始使用Google廣告的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 端點，同時將您的Google廣告身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為Google廣告建立基本連接：

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
| `auth.params.clientCustomerID` | 您的Google廣告帳戶的客戶端客戶ID。 |
| `auth.params.loginCustomerID` | 與您的Google廣告經理帳戶對應的登錄客戶ID。 |
| `auth.params.developerToken` | 您的Google廣告帳戶的開發者令牌。 |
| `auth.params.refreshToken` | 您的Google廣告帳戶的刷新令牌。 |
| `auth.params.clientID` | 你的Google廣告帳戶的客戶端ID。 |
| `auth.params.clientSecret` | 你Google廣告賬戶的客戶機密。 |
| `connectionSpec.id` | Google廣告連接規範ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

通過本教程，您已使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/advertising.md)
