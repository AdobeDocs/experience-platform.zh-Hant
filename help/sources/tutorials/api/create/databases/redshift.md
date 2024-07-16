---
title: 使用流量服務API建立Amazon Redshift基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Amazon Redshift。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL Amazon Redshift]基本連線

>[!IMPORTANT]
>
>[!DNL Amazon Redshift]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Amazon Redshift]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Amazon Redshift]。

### 收集必要的認證

若要讓[!DNL Flow Service]與[!DNL Amazon Redshift]連線，您必須提供下列連線屬性：

| **認證** | **說明** |
| -------------- | --------------- |
| `server` | 與您的[!DNL Amazon Redshift]帳戶關聯的伺服器。 |
| `port` | [!DNL Amazon Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| `username` | 與您的[!DNL Amazon Redshift]帳戶相關聯的使用者名稱。 |
| `password` | 與您的[!DNL Amazon Redshift]帳戶關聯的密碼。 |
| `database` | 您正在存取的[!DNL Amazon Redshift]資料庫。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Amazon Redshift]的連線規格識別碼為`3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

如需開始使用的詳細資訊，請參閱此[[!DNL Amazon Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

>[!NOTE]
>
>[!DNL Redshift]的預設編碼標準為Unicode。 無法變更此設定。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Amazon Redshift]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Amazon Redshift]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | 您的[!DNL Amazon Redshift]伺服器。 |
| `auth.params.port` | [!DNL Amazon Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| `auth.params.database` | 與您的[!DNL Amazon Redshift]帳戶關聯的資料庫。 |
| `auth.params.password` | 與您的[!DNL Amazon Redshift]帳戶關聯的密碼。 |
| `auth.params.username` | 與您的[!DNL Amazon Redshift]帳戶相關聯的使用者名稱。 |
| `connectionSpec.id` | [!DNL Amazon Redshift]連線規格識別碼： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Amazon Redshift]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶到Platform](../../collect/database-nosql.md)
