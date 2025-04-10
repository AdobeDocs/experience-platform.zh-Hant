---
title: 使用流程服務API連線PostgreSQL至Experience Platform
description: 瞭解如何使用API將您的 [!DNL PostgreSQL] 資料庫連線到Experience Platform。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 5348158f6de9fea1a9fe186a14409afb7e7a376e
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL PostgreSQL]基本連線

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL PostgreSQL]資料庫連線至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL PostgreSQL]。

### 使用Experience Platform API

閱讀[Experience Platform API快速入門](../../../../../landing/api-guide.md)的指南，瞭解如何成功呼叫Experience Platform API。

### 收集必要的認證

如需驗證的詳細資訊，請閱讀[[!DNL PostgreSQL] 概觀](../../../../connectors/databases/postgres.md)。

### 為您的連線字串啟用SSL加密

您可以使用下列屬性附加您的連線字串，以啟用[!DNL PostgreSQL]連線字串的SSL加密：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 可讓您對[!DNL PostgreSQL]資料啟用SSL加密。 | <uL><li>`EncryptionMethod=0`（已停用）</li><li>`EncryptionMethod=1`（已啟用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 套用`EncryptionMethod`時，驗證您的[!DNL PostgreSQL]資料庫傳送的憑證。 | <uL><li>`ValidationServerCertificate=0`（已停用）</li><li>`ValidationServerCertificate=1`（已啟用）</li></ul> |

下列是附加SSL加密的[!DNL PostgreSQL]連線字串範例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 在Azure上連線[!DNL PostgreSQL]至Experience Platform {#azure}

請閱讀下列步驟，瞭解如何將您的[!DNL PostgreSQL]帳戶連線至Azure上的Experience Platform。

### 建立基礎連線 {#azure-base}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL PostgreSQL]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 以帳戶金鑰為基礎的驗證]

**要求**

下列要求使用以帳戶金鑰為基礎的驗證來建立[!DNL PostgreSQL]的基礎連線：

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.connectionString` | 與您的[!DNL PostgreSQL]帳戶關聯的連線字串。 [!DNL PostgreSQL]連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]連線規格識別碼： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**回應**

成功的回應會傳回新建立之基礎連線的唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB 基本驗證]

**要求**

下列要求使用基本驗證建立[!DNL PostgreSQL]的基本連線：

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL]資料庫的名稱或IP位址。 |
| `auth.params.port` | 資料庫伺服器的連線埠號碼。 |
| `auth.params.database` | [!DNL PostgreSQL]資料庫的名稱。 |
| `auth.params.username` | 與您的[!DNL PostgreSQL]資料庫驗證相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL PostgreSQL]資料庫驗證關聯的密碼。 |
| `auth.params.sslMode` | 資料傳輸期間加密資料的方法。 可用的值包括： `Disable`、`Allow`、`Prefer`、`Verify Ca`和`Verify Full`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]連線規格識別碼： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**回應**

成功的回應會傳回新建立之基礎連線的唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## 將[!DNL PostgreSQL]連線至Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何將[!DNL PostgreSQL]資料庫連線至AWS上的Experience Platform。

### 建立基礎連線 {#aws-base}

若要建立基底連線ID，請在提供您的[!DNL PostgreSQL]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL PostgreSQL]的基礎連線，以連線至AWS上的Experience Platform。

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL]資料庫的名稱或IP位址。 |
| `auth.params.port` | 資料庫伺服器的連線埠號碼。 |
| `auth.params.database` | [!DNL PostgreSQL]資料庫的名稱。 |
| `auth.params.username` | 與您的[!DNL PostgreSQL]資料庫驗證相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL PostgreSQL]資料庫驗證關聯的密碼。 |
| `auth.params.sslMode` | 資料傳輸期間加密資料的方法。 可用的值包括： `Disable`、`Allow`、`Prefer`、`Verify Ca`和`Verify Full`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]連線規格識別碼： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**回應**

成功的回應會傳回新建立之基礎連線的唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## 後續步驟

現在您已建立[!DNL PostgreSQL]資料庫與Experience Platform之間的連線，您可以繼續後續步驟，並將[!DNL PostgreSQL]資料帶入Experience Platform。 如需詳細資訊，請參閱下列檔案：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
