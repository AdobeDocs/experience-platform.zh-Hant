---
title: 使用Flow Service API建立Microsoft SQL Server基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Microsoft SQL Server。
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Microsoft] SQL Server基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Microsoft SQL Server]建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Microsoft SQL Server]。

### 收集必要的認證 {#gather-required-credentials}

若要連線到[!DNL Microsoft SQL Server]，您必須提供下列連線屬性：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `connectionString` | 與您的[!DNL Microsoft SQL Server]帳戶關聯的連線字串。 您的連線字串模式取決於您是使用伺服器名稱或執行個體名稱作為資料來源：<ul><li>使用伺服器名稱的連線字串： `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>使用執行個體名稱的連線字串： `Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Microsoft SQL Server]的連線規格識別碼為`1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`。 |

如需有關取得連線字串的詳細資訊，請參閱此[[!DNL Microsoft SQL Server] 檔案](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Microsoft SQL Server]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Microsoft SQL Server]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.connectionString` | 與您的[!DNL Microsoft SQL Server]帳戶關聯的連線字串。 如需詳細資訊，請閱讀[收集所需認證](#gather-required-credentials)的相關章節。 |
| `connectionSpec.id` | [!DNL Microsoft SQL Server]連線規格識別碼為： `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料庫時，需要此ID。

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Microsoft SQL Server]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)