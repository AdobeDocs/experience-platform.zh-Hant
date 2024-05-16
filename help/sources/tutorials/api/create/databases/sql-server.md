---
title: 使用Flow Service API建立Microsoft SQL Server基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Microsoft SQL Server。
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 5%

---

# 建立 [!DNL Microsoft] SQL Server基本連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本教學課程以瞭解如何建立基本連線，用於 [!DNL Microsoft SQL Server] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需的其他資訊 [!DNL Microsoft SQL Server] 使用 [!DNL Flow Service] API。

### 收集必要的認證 {#gather-required-credentials}

為了連線到 [!DNL Microsoft SQL Server]，您必須提供下列連線屬性：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `connectionString` | 與您的關聯的連線字串 [!DNL Microsoft SQL Server] 帳戶。 您的連線字串模式取決於您是使用伺服器名稱或執行個體名稱作為資料來源：<ul><li>使用伺服器名稱的連線字串： `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>使用執行個體名稱的連線字串：`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Microsoft SQL Server] 是 `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

如需有關取得連線字串的詳細資訊，請參閱此 [[!DNL Microsoft SQL Server] 檔案](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Microsoft SQL Server] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL Microsoft SQL Server]：

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
| `auth.params.connectionString` | 與您的關聯的連線字串 [!DNL Microsoft SQL Server] 帳戶。 閱讀本節： [正在蒐集必要的認證](#gather-required-credentials) 以取得詳細資訊。 |
| `connectionSpec.id` | 此 [!DNL Microsoft SQL Server] 連線規格ID為： `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料庫時，需要此ID。

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Microsoft SQL Server] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)