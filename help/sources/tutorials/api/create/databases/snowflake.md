---
title: 使用流量服務API建立Snowflake基礎連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Snowflake。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Snowflake]基本連線

>[!IMPORTANT]
>
>[!DNL Snowflake]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

使用下列教學課程瞭解如何使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)為[!DNL Snowflake]建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

以下章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Snowflake]。

### 收集必要的認證

您必須提供下列認證屬性的值，才能驗證您的[!DNL Snowflake]來源。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

| 認證 | 說明 |
| ---------- | ----------- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 如需帳戶名稱的詳細資訊，請閱讀[帳戶識別碼](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)的[!DNL Snowflake]檔案。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料傳送至Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]資料庫包含您要帶入Platform的資料。 |
| `username` | [!DNL Snowflake]帳戶的使用者名稱。 |
| `password` | [!DNL Snowflake]使用者帳戶的密碼。 |
| `role` | 在[!DNL Snowflake]工作階段中使用的預設存取控制角色。 該角色應為已指派給指定使用者的現有角色。 預設角色為`PUBLIC`。 |
| `connectionString` | 用來連線至您[!DNL Snowflake]執行個體的連線字串。 [!DNL Snowflake]的連線字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 金鑰組驗證]

若要使用金鑰組驗證，您必須產生2048位元RSA金鑰組，然後在建立[!DNL Snowflake]來源的帳戶時提供下列值。

| 認證 | 說明 |
| --- | --- |
| `account` | 帳戶名稱可唯一識別組織內的帳戶。 在此情況下，您必須跨不同的[!DNL Snowflake]組織唯一識別帳戶。 若要這麼做，您必須在帳戶名稱前加上組織名稱。 例如： `orgname-account_name`。 如需帳戶名稱的詳細資訊，請閱讀[帳戶識別碼](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)的[!DNL Snowflake]檔案。 |
| `username` | 您[!DNL Snowflake]帳戶的使用者名稱。 |
| `privateKey` | 您[!DNL Snowflake]帳戶的[!DNL Base64-]編碼私密金鑰。 您可以產生加密或未加密的私密金鑰。 如果您使用加密的私密金鑰，則在針對Experience Platform進行驗證時，也必須提供私密金鑰複雜密碼。 |
| `privateKeyPassphrase` | 私密金鑰複雜密碼是附加的安全性層級，在使用加密的私密金鑰進行驗證時必須使用此層級。 如果您使用未加密的私密金鑰，則不需要提供複雜密碼。 |
| `database` | 包含您要擷取以Experience Platform之資料的[!DNL Snowflake]資料庫。 |
| `warehouse` | [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個[!DNL Snowflake]倉儲彼此獨立，在將資料移至Experience Platform時，必須個別存取。 |

如需這些值的詳細資訊，請參閱[[!DNL Snowflake] 金鑰組驗證指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

>[!NOTE]
>
>您必須將`PREVENT_UNLOAD_TO_INLINE_URL`標幟設定為`FALSE`，以允許從[!DNL Snowflake]資料庫解除安裝資料以Experience Platform。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Snowflake]驗證認證作為要求內文的一部分時，向`/connections`端點提出POST要求。

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

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Snowflake]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶到Platform](../../collect/database-nosql.md)
