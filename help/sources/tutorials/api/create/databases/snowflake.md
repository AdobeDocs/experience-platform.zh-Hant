---
keywords: Experience Platform；首頁；熱門主題；Snowflake;snowflake
solution: Experience Platform
title: 使用流服務API建立Snowflake基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Snowflake。
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: b1c0c3ea0d7170f76728de06e05787b7c9aaffe9
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 1%

---

# 建立 [!DNL Snowflake] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Snowflake] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

以下部分提供了成功連接到所需的其他資訊 [!DNL Snowflake] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Snowflake]，必須提供以下連接屬性：

| 憑據 | 說明 |
| --- | --- |
| `account` | 與您的 [!DNL Snowflake] 帳戶。 完全合格 [!DNL Snowflake] 帳戶名包括您的帳戶名、區域和雲平台。 例如 `cj12345.east-us-2.azure`。有關帳戶名的詳細資訊，請參閱 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html)。 |
| `warehouse` | 的 [!DNL Snowflake] 倉庫管理應用程式的查詢執行過程。 每個 [!DNL Snowflake] 倉庫彼此獨立，在將資料傳送到平台時必須單獨訪問。 |
| `database` | 的 [!DNL Snowflake] 資料庫包含要帶入平台的資料。 |
| `username` | 用戶名 [!DNL Snowflake] 帳戶。 |
| `password` | 的密碼 [!DNL Snowflake] 用戶帳戶。 |
| `connectionString` | 用於連接到您的 [!DNL Snowflake] 實例。 的連接字串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Snowflake] 是 `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

有關入門的詳細資訊，請參閱此 [[!DNL Snowflake] 文檔](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Snowflake] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Snowflake]:

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
          "specName": "ConnectionString,
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
| `auth.params.connectionString` | 用於連接到您的 [!DNL Snowflake] 實例。 的連接字串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |
| `connectionSpec.id` | 的 [!DNL Snowflake] 連接規範ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

按照本教程，您建立了 [!DNL Snowflake] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
