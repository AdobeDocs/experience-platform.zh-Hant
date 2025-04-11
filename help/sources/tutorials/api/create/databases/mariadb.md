---
title: 使用流程服務API連線MariaDB至Experience Platform
description: 瞭解如何使用API將您的MariaDB帳戶連結至Experience Platform。
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API連線[!DNL MariaDB]至Experience Platform

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL MariaDB]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL MariaDB]。

### 收集必要的認證

[[!DNL MariaDB] 有關身份驗證的資訊，請閱讀概述](../../../../connectors/databases/mariadb.md#prerequisites)。

### 使用 Experience Platform API

有關如何成功調用 Experience Platform API 的資訊，請閱讀有關開始使用 Experience Platform API](../../../../../landing/api-guide.md) 指南[。

## 連接到 [!DNL MariaDB] Azure 上的 Experience Platform {#azure}

有關如何將帳戶連接到 [!DNL MariaDB] Azure 上的Experience Platform的信息，請閱讀以下步驟。

### 在Azure上的Experience Platform上為[!DNL MariaDB]建立基礎連線 {#azure-base}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

**API格式**

```https
POST /connections
```

若要建立基底連線識別碼，請對`/connections`端點提出POST要求，並為您的[!DNL MariaDB]帳戶提供適當的驗證認證。

>[!BEGINTABS]

>[!TAB 以連線字串為基礎的驗證]

**要求**

下列要求使用以連線字串為基礎的驗證，為[!DNL MariaDB]來源建立基礎連線。

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 與您的[!DNL MariaDB]驗證關聯的連線字串。 [!DNL MariaDB]連線字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL MariaDB]連線規格識別碼為： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB 基本驗證]

**要求**

以下請求使用基本身份驗證為源創建 [!DNL MariaDB] 基本連接。

+++檢視 請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL MariaDB]資料庫的名稱或IP。 |
| `auth.params.database` | 資料庫的名稱。 |
| `auth.params.username` | 與您的資料庫對應的使用者名稱。 |
| `auth.params.password` | 與資料庫對應的密碼。 |
| `auth.params.sslMode` | 資料傳輸期間加密資料的方法。 |
| `connectionSpec.id` | [!DNL MariaDB]連線規格識別碼為： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

>[!ENDTABS]

## 將[!DNL MariaDB]連線至Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何在AWS上將您的[!DNL MariaDB]帳戶連結至Experience Platform。

### 建立 AWS 上 On Experience Platform 的基本 [!DNL MariaDB] 連接 {#aws-base}

**API 格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL MariaDB]的基礎連線，以連線至AWS上的Experience Platform。

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
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL MariaDB]資料庫的名稱或IP。 |
| `auth.params.database` | 資料庫的名稱。 |
| `auth.params.username` | 與您的資料庫對應的使用者名稱。 |
| `auth.params.password` | 與資料庫對應的密碼。 |
| `auth.params.sslMode` | 資料傳輸期間加密資料的方法。 |
| `connectionSpec.id` | [!DNL MariaDB]連線規格識別碼為： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL MariaDB]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
