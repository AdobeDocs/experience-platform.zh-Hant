---
title: 使用流服務API建立SalesforceMarketing Cloud基連接
description: 瞭解如何使用流服務API對Experience Platform驗證SalesforceMarketing Cloud帳戶。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Marketing Cloud] 基本連接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>當前不支援自定義對象攝取 [!DNL Salesforce Marketing Cloud] 源整合。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Salesforce Marketing Cloud] 使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

以下部分提供了成功連接到所需的其他資訊 [!DNL Salesforce Marketing Cloud] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Salesforce Marketing Cloud]，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子域。 **注：** 輸入 `host` 值，只需指定子域，而不是整個URL。 例如，如果主機URL為 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則只需輸入 `acme-ab12c3d4e5fg6hijk7lmnop8qrst` 作為主機值。 |
| `clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| `clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Salesforce Marketing Cloud] 為： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

有關入門的詳細資訊，請參閱此 [[!DNL Salesforce Marketing Cloud] 文檔](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Salesforce Marketing Cloud] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| `auth.params.clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| `connectionSpec.id` | 的 [!DNL Salesforce Marketing Cloud] 連接規範ID: `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Salesforce Marketing Cloud] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
