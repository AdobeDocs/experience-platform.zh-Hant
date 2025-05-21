---
title: 使用流程服務API連線MySQL至Experience Platform
description: 瞭解如何使用API將MySQL資料庫連結至Experience Platform。
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API連線[!DNL MySQL]至Experience Platform

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL MySQL]帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL MySQL]。

### 收集必要的認證

閱讀[[!DNL MySQL] 總覽](../../../../connectors/databases/mysql.md#prerequisites)以取得驗證的相關資訊。

### 使用Experience Platform API

閱讀[Experience Platform API快速入門](../../../../../landing/api-guide.md)的指南，瞭解如何成功呼叫Experience Platform API。

## 在Azure上連線[!DNL MySQL]至Experience Platform {#azure}

請閱讀下列步驟，以瞭解如何在Azure上將您的[!DNL MySQL]帳戶連線至Experience Platform。

### 在Azure上的Experience Platform上為[!DNL MySQL]建立基礎連線 {#azure-base}

基礎連線會將您的來源連結至Experience Platform，以儲存驗證詳細資料、連線狀態和唯一ID。 使用此ID來瀏覽來源檔案並識別要擷取的特定專案，包括其資料型別和格式。

**API格式**

```https
POST /connections
```

若要建立基底連線ID，請對`/connections`端點提出POST要求，並提供您的[!DNL MySQL]驗證認證作為要求引數的一部分。

>[!BEGINTABS]

>[!TAB 以連線字串為基礎的驗證]

**要求**

下列要求會使用以連線字串為基礎的驗證，為[!DNL MySQL]建立基礎連線。

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.connectionString` | 與您的帳戶相關聯的[!DNL MySQL]連線字串。 [!DNL MySQL]連線字串模式為： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL MySQL]連線規格識別碼： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB 基本驗證]

**要求**

下列要求使用基本驗證建立[!DNL MySQL]來源的基本連線。

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL]資料庫的名稱或IP。 |
| `auth.params.database` | 資料庫的名稱。 |
| `auth.params.username` | 與您的資料庫對應的使用者名稱。 |
| `auth.params.password` | 與資料庫對應的密碼。 |
| `auth.params.sslMode` | 資料傳輸期間加密資料的方法。 |
| `connectionSpec.id` | [!DNL MySQL]連線規格識別碼為： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應範例

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## 將[!DNL MySQL]連線至Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何在AWS上將您的[!DNL MySQL]帳戶連結至Experience Platform。

### 在AWS上的Experience Platform上為[!DNL MySQL]建立基礎連線 {#aws-base}

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL MySQL]的基礎連線，以連線至AWS上的Experience Platform。

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
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL]資料庫的名稱或IP。 |
| `auth.params.database` | 資料庫的名稱。 |
| `auth.params.username` | 與您的資料庫對應的使用者名稱。 |
| `auth.params.password` | 與資料庫對應的密碼。 |
| `auth.params.sslMode` | 根據您的伺服器支援，控制SSL是否強制執行的布林值。 此設定預設為`false`。 |
| `connectionSpec.id` | [!DNL MySQL]連線規格識別碼為： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

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

## 建立[!DNL MySQL]資料的資料流

現在您已經成功連線[!DNL MySQL]資料庫，您現在可以[建立資料流，並將資料庫中的資料擷取到Experience Platform](../../collect/database-nosql.md)。