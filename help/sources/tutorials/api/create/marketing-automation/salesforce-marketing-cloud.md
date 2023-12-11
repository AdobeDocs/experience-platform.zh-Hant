---
title: 使用流量服務API建立SalesforceMarketing Cloud基礎連線
description: 瞭解如何使用流量服務API，針對Experience Platform驗證您的SalesforceMarketing Cloud帳戶。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 635ab266fac9d3dc232307d7cb49f83904197782
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 4%

---

# 建立 [!DNL Salesforce Marketing Cloud] 基礎連線使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>自訂物件擷取目前不受 [!DNL Salesforce Marketing Cloud] 來源整合。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Salesforce Marketing Cloud] 使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

下節提供成功連線所需的其他資訊 [!DNL Salesforce Marketing Cloud] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Salesforce Marketing Cloud]，您必須提供下列連線屬性：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：** 輸入您的 `host` 值，您必須指定 `{subdomain}.rest.marketingcloudapis.com`. 例如，如果您的主機URL為 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則您只需輸入 `acme-ab12c3d4e5fg6hijk7lmnop8qrstauth.marketingcloudapis.com/` 作為您的主機值。 |
| `clientId` | 與您的關聯的使用者端ID [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `clientSecret` | 與您的關聯的使用者端密碼 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Salesforce Marketing Cloud] 為： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

如需入門的詳細資訊，請參閱此 [[!DNL Salesforce Marketing Cloud] 檔案](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Salesforce Marketing Cloud] 要求內文中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL Salesforce Marketing Cloud]：

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
| `auth.params.clientId` | 與您的關聯的使用者端ID [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `auth.params.clientSecret` | 與您的關聯的使用者端密碼 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Marketing Cloud] 連線規格ID： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Salesforce Marketing Cloud] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用將行銷自動化資料帶入Platform [!DNL Flow Service] API](../../collect/marketing-automation.md)
