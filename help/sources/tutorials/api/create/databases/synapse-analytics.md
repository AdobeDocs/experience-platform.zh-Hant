---
title: 使用流量服務API連線Azure Synapse Analytics至Experience Platform
description: 瞭解如何使用API將您的Azure Synapse Analytics帳戶連結至Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API連線[!DNL Azure Synapse Analytics]至Experience Platform

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Azure Synapse Analytics]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Azure Synapse Analytics]。

### 收集必要的認證

閱讀[[!DNL Azure Synapse Analytics] 總覽](../../../../connectors/databases/synapse-analytics.md#prerequisites)以取得驗證的相關資訊。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 將[!DNL Azure Synapse Analytics]連線至Experience Platform

請閱讀下列內容，瞭解如何建立基本連線，並將您的[!DNL Azure Synapse Analytics]帳戶連線至Experience Platform。

### 建立基礎連線

**基礎連線**&#x200B;儲存將來源系統連結至Adobe Experience Platform的金鑰資訊。 其中包括：

* 您來源的驗證認證
* 連線的目前狀態
* 唯一的&#x200B;**基底連線識別碼**

**基本連線ID**&#x200B;可讓您瀏覽和瀏覽來源中的檔案，協助您識別要擷取的專案，以及專案的資料型別和格式。

若要建立基底連線識別碼，請傳送POST要求至`/connections`端點，包括要求引數中的[!DNL Azure Synapse Analytics]驗證認證。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 以連線字串為基礎的驗證]

**要求**

下列要求會使用以連線字串為基礎的驗證，為[!DNL Azure Synapse Analytics]建立基礎連線。

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
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 用來連線到[!DNL Azure Synapse Analytics]的連線字串。 [!DNL Azure Synapse Analytics]連線字串模式為`Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |
| `connectionSpec.id` | [!DNL Azure Synapse Analytics]連線規格識別碼為： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視範例回應

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB 以服務主要金鑰為基礎的驗證]

下列要求會使用以服務主要金鑰為基礎的驗證，為[!DNL Azure Synapse Analytics]建立基礎連線。

**要求**

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
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| 認證 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL Azure Synapse Analytics] SQL端點的完整網域名稱。 |
| `auth.params.database` | [!DNL Azure Synapse Analytics]工作區中特定資料庫的名稱。 |
| `auth.params.tenant` | 與您的[!DNL Azure]訂閱相關聯的[!DNL Azure Active Directory]租使用者識別碼。 |
| `auth.params.servicePrincipalId` | [!DNL Azure Active Directory]應用程式的使用者端識別碼。 |
| `auth.params.servicePrincipalKey` | 與服務主體關聯的使用者端密碼或密碼。 |
| `connectSpec.id` | [!DNL Azure Synapse Analytics]的連線規格ID。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視範例回應

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Azure Synapse Analytics]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
