---
title: 使用流量服務API將Azure資料庫連線至Experience Platform
description: 瞭解如何使用API將Azure Databricks連線至Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 9df2f9cc70876834aa635d50d548a882f45e3190
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API連線[!DNL Azure Databricks]至Experience Platform

>[!AVAILABILITY]
>
>* [!DNL Azure Databricks]來源可在來源目錄中提供給已購買Real-Time CDP Ultimate的使用者。
>
>* [!DNL Azure Databricks]來源是測試版。 閱讀來源概觀中的[條款與條件](../../../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Azure Databricks]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

閱讀[如何開始使用Experience Platform API](../../../../../landing/api-guide.md)的指南，瞭解如何成功呼叫Experience Platform API。

### 設定先決條件設定

請閱讀[[!DNL Databricks] 總覽](../../../../connectors/databases/databricks.md)，瞭解在您將帳戶連線至Experience Platform之前必須完成的先決條件設定。

### 收集必要的認證

提供下列認證的值，以便將[!DNL Databricks]連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| `domain` | [!DNL Databricks]工作區的URL。 例如 `https://adb-1234567890123456.7.azuredatabricks.net`。 |
| `clusterId` | [!DNL Databricks]中叢集的識別碼。 此叢集必須是現有的叢集，而且應該是互動式叢集。 |
| `accessToken` | 驗證您[!DNL Databricks]帳戶的存取Token。 您可以使用[!DNL Databricks]工作區產生存取權杖。 |
| `database` | 三角湖中的資料庫名稱。 |
| `connectionSpec.Id` | 連線規格ID會傳回來源的連線器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Databricks]的連線規格識別碼為`e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`。 |

如需詳細資訊，請閱讀 [[!DNL Azure Databricks]  概觀](../../../../connectors/databases/databricks.md)。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線識別碼，請對`/connections`端點提出POST要求，並為您的[!DNL Databricks]帳戶提供適當的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會使用存取權杖驗證，為[!DNL Databricks]來源建立基底連線。

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
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.domain` | [!DNL Databricks]工作區的URL。 |
| `auth.params.clusterId` | [!DNL Databricks]中叢集的識別碼。 此叢集必須是現有的叢集，而且應該是互動式叢集 |
| `auth.params.accessToken` | 驗證您[!DNL Databricks]帳戶的存取Token。 |
| `auth.params.database` | 三角湖中的資料庫名稱。 |
| `connectionSpec.id` | [!DNL Databricks]連線規格識別碼。 |

+++

**回應**

成功的回應會傳回您新建立的連線，包括基本連線ID。

+++檢視回應範例

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## 後續步驟

依照此教學課程，您已成功建立[!DNL Databricks]帳戶與Experience Platform之間的連線。 您可在下列教學課程中使用新產生的基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
