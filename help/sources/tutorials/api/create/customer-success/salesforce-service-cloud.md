---
title: 使用流量服務API建立Salesforce Service Cloud Source連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]來源連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Salesforce Service Cloud]建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Salesforce Service Cloud]。

### 收集必要的認證

閱讀[驗證指南](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials)，以取得擷取認證的詳細資訊。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Salesforce Service Cloud]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

以下要求使用OAuth 2使用者端認證為[!DNL Salesforce Service Cloud]建立基礎連線：

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
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud]執行個體的URL。 |
| `auth.params.clientId` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL Salesforce Service Cloud]帳戶相關聯的使用者端密碼。 |
| `auth.params.apiVersion` | 您正在使用的[!DNL Salesforce Service Cloud]執行個體的REST API版本。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]連線規格識別碼： `cb66ab34-8619-49cb-96d1-39b37ede86ea`。 |

**回應**

成功的回應會傳回您新建立的基本連線及其唯一ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Salesforce Service Cloud]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流，將客戶成功資料匯入Experience Platform](../../collect/customer-success.md)
