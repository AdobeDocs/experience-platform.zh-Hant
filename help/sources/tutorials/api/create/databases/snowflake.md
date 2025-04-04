---
title: 使用流量服務API連線Snowflake至Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Snowflake。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API連線[!DNL Snowflake]至Experience Platform

>[!IMPORTANT]
>
>[!DNL Snowflake]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Snowflake]來源帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

以下章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Snowflake]。

## 在Azure上連線[!DNL Snowflake]至Experience Platform {#azure}

請閱讀下列步驟，以瞭解如何在Azure上將您的[!DNL Snowflake]來源連線至Experience Platform。

### 收集必要的認證

您必須提供下列認證屬性的值，才能驗證您的[!DNL Snowflake]來源。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

| 認證 | 說明 |
| ---------- | ----------- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]資料庫包含您要帶入Experience Platform的資料。 |
| `username` | [!DNL Snowflake]帳戶的使用者名稱。 |
| `password` | [!DNL Snowflake]使用者帳戶的密碼。 |
| `role` | 在[!DNL Snowflake]工作階段中使用的預設存取控制角色。 該角色應為已指派給指定使用者的現有角色。 預設角色為`PUBLIC`。 |
| `connectionString` | 用來連線至您[!DNL Snowflake]執行個體的連線字串。 [!DNL Snowflake]的連線字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，您必須產生2048位元RSA金鑰組，然後在建立[!DNL Snowflake]來源的帳戶時提供下列值。

| 認證 | 說明 |
| --- | --- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 閱讀[擷取 [!DNL Snowflake] 帳戶識別碼](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以取得其他指引。 如需詳細資訊，請參閱[[!DNL Snowflake] 文件](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)，以瞭解詳情。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您[!DNL Snowflake]帳戶的[!DNL Base64-]編碼私密金鑰。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 如需詳細資訊，請參閱[擷取 [!DNL Snowflake] 私密金鑰](../../../../connectors/databases/snowflake.md)的指南。 |
| `privateKeyPassphrase` | 私密金鑰複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| `database` | 包含您要擷取至Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料帶到Experience Platform時必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

>[!NOTE]
>
>您必須將`PREVENT_UNLOAD_TO_INLINE_URL`標幟設定為`FALSE`，以允許從[!DNL Snowflake]資料庫將資料解除安裝至Experience Platform。

### 在Azure上的Experience Platform上為[!DNL Snowflake]建立基礎連線 {#azure-base}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Snowflake]驗證認證作為要求內文的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 連線字串]

+++要求

下列要求會建立[!DNL Snowflake]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 用來連線至您[!DNL Snowflake]執行個體的連線字串。 [!DNL Snowflake]的連線字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |
| `connectionSpec.id` | [!DNL Snowflake]連線規格識別碼： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++

+++回應

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB 使用加密私密金鑰的金鑰組驗證]

+++要求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.account` | 您的[!DNL Snowflake]帳戶名稱。 |
| `auth.params.username` | 與您的[!DNL Snowflake]帳戶相關聯的使用者名稱。 |
| `auth.params.database` | 將從其中提取資料的[!DNL Snowflake]資料庫。 |
| `auth.params.privateKey` | 您的[!DNL Snowflake]帳戶的[!DNL Base64-]編碼加密私密金鑰。 |
| `auth.params.privateKeyPassphrase` | 與您的私密金鑰對應的複雜密碼。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]倉儲。 |
| `connectionSpec.id` | [!DNL Snowflake]連線規格識別碼： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++

+++回應

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB 使用未加密私密金鑰的金鑰組驗證]

+++要求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.account` | 您的[!DNL Snowflake]帳戶名稱。 |
| `auth.params.username` | 與您的[!DNL Snowflake]帳戶相關聯的使用者名稱。 |
| `auth.params.database` | 將從其中提取資料的[!DNL Snowflake]資料庫。 |
| `auth.params.privateKey` | [!DNL Snowflake]帳戶的[!DNL Base64-]編碼未加密私密金鑰。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]倉儲。 |
| `connectionSpec.id` | [!DNL Snowflake]連線規格識別碼： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++

+++回應

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## 將[!DNL Snowflake]連線到Amazon Web Services (AWS)上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何將[!DNL Snowflake]來源連線至AWS上的Experience Platform。

### 在AWS的Experience Platform上為[!DNL Snowflake]建立基礎連線 {#aws-base}

**API格式**

```http
POST /connections
```

**要求**

下列請求會建立[!DNL Snowflake]的基礎連線，以將日期擷取至AWS上的Experience Platform：

+++選取以檢視範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.host` | 您的[!DNL Snowflake]帳戶連線到的主機URL。 |
| `auth.params.port` | [!DNL Snowflake]透過網際網路連線到伺服器時使用的連線埠號碼。 |
| `auth.params.username` | 與您的[!DNL Snowflake]帳戶相關聯的使用者名稱。 |
| `auth.params.database` | 將從其中提取資料的[!DNL Snowflake]資料庫。 |
| `auth.params.password` | 與您的[!DNL Snowflake]帳戶關聯的密碼。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]倉儲。 |
| `auth.params.schema` | 與您的[!DNL Snowflake]資料庫關聯的結構描述名稱。 您必須確保您要授與資料庫存取權的使用者也擁有此綱要的存取權。 |

+++

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的儲存空間時，需要此ID。

+++選取以檢視範例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Snowflake]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
