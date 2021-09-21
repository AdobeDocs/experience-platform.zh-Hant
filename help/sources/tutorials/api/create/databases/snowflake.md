---
keywords: Experience Platform；首頁；熱門主題；Snowflake;snowflake
solution: Experience Platform
title: 使用流量服務API建立Snowflake基礎連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Snowflake。
source-git-commit: 5e2301a409f04bd4e23888648f244918b871f0ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Snowflake]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Snowflake]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

以下章節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Snowflake]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Snowflake]連接，必須提供以下連接屬性：

| 憑據 | 說明 |
| --- | --- |
| `account` | 要連接到Platform的[!DNL Snowflake]帳戶。 |
| `warehouse` | [!DNL Snowflake]倉庫管理應用程式的查詢執行過程。 每個[!DNL Snowflake]倉庫彼此獨立，在將資料傳至Platform時必須個別存取。 |
| `database` | [!DNL Snowflake]包含您要帶入平台的資料。 |
| `username` | [!DNL Snowflake]帳戶的用戶名。 |
| `password` | [!DNL Snowflake]用戶帳戶的密碼。 |
| `connectionString` | 用於連接到[!DNL Snowflake]實例的連接字串。 [!DNL Snowflake]的連接字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Snowflake]的連接規範ID為`b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

有關入門的詳細資訊，請參閱此[[!DNL Snowflake] document](https://docs.snowflake.com/en/user-guide/oauth-custom.html)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Snowflake]驗證憑證作為要求內文的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Snowflake]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
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
| `auth.params.connectionString` | 用於連接到[!DNL Snowflake]實例的連接字串。 [!DNL Snowflake]的連接字串模式為`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |
| `connectionSpec.id` | [!DNL Snowflake]連接規範ID:`b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Snowflake]連線，並取得連線的唯一ID值。 在您了解如何使用流服務API](../../explore/database-nosql.md)來探索資料庫時，您可以在下一個教學課程中使用此連接ID。[