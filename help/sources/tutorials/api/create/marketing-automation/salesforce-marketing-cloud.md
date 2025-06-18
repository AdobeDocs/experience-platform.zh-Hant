---
title: 使用流量服務API連線Salesforce Marketing Cloud至Experience Platform
description: 瞭解如何使用API將您的Salesforce Marketing Cloud帳戶連結至Experience Platform。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API連線[!DNL Salesforce Marketing Cloud]至Experience Platform

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]來源將於2026年1月汰除。 新的來源將作為替代方案於今年晚些時候發行。 釋放新來源後，您必須在2026年1月底之前建立新的帳戶連線和資料流，以計畫移轉至新來源。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Salesforce Marketing Cloud]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Azure Synapse Analytics]。


### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

以下章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Salesforce Marketing Cloud]。

### 收集必要的認證

閱讀[[!DNL Salesforce Marketing Cloud] 驗證概觀](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md)以取得有關驗證的資訊。

### 使用Experience Platform API

閱讀[Experience Platform API快速入門](../../../../../landing/api-guide.md)的指南，瞭解如何成功呼叫Experience Platform API。

## 將[!DNL Salesforce Marketing Cloud]連線至[!DNL Azure]上的Experience Platform

請閱讀下列內容，瞭解如何建立基本連線，並將您的[!DNL Salesforce Marketing Cloud]帳戶連線至[!DNL Azure]上的Experience Platform。

### 建立基礎連線 {#azure-base}

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源整合目前不支援自訂物件擷取。

**基礎連線**&#x200B;儲存將來源系統連結至Adobe Experience Platform的金鑰資訊。 其中包括：

* 您來源的驗證認證
* 連線的目前狀態
* 唯一的&#x200B;**基底連線識別碼**

**基本連線ID**&#x200B;可讓您瀏覽和瀏覽來源中的檔案，協助您識別要擷取的專案，以及專案的資料型別和格式。

若要建立基底連線識別碼，請傳送POST要求至`/connections`端點，包括要求引數中的[!DNL Salesforce Marketing Cloud]驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Salesforce Marketing Cloud]的基礎連線。

+++檢視範例請求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
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
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端識別碼。 |
| `auth.params.clientSecret` | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端密碼。 |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud]連線規格識別碼： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

+++

+++檢視範例回應

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## 將[!DNL Salesforce Marketing Cloud]連線至Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何在AWS上將您的[!DNL Salesforce Marketing Cloud]帳戶連結至Experience Platform。

### 建立基礎連線 {#aws-base}

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Salesforce Service Cloud]的基礎連線，以連線至AWS上的Experience Platform。

+++檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## 建立[!DNL Salesforce Marketing Cloud]資料的資料流

現在您已成功連線您的[!DNL Salesforce Marketing Cloud]帳戶，您現在可以[建立資料流，並將行銷自動化提供者的資料擷取到Experience Platform](../../collect/marketing-automation.md)。