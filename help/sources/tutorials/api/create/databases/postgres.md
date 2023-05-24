---
keywords: Experience Platform；首頁；熱門主題；PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: 使用流服務API建立PostgreSQL基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# 建立 [!DNL PostgreSQL] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL PostgreSQL] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。


## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL PostgreSQL] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL PostgreSQL]，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的 [!DNL PostgreSQL] 帳戶。 的 [!DNL PostgreSQL] 連接字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL PostgreSQL] 是 `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

有關獲取連接字串的詳細資訊，請參閱 [[!DNL PostgreSQL] 文檔](https://www.postgresql.org/docs/9.2/app-psql.html)。

#### 為連接字串啟用SSL加密

您可以為 [!DNL PostgreSQL] 連接字串，方法是將連接字串與以下屬性附加：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 允許您在 [!DNL PostgreSQL] 資料。 | <uL><li>`EncryptionMethod=0`(停用)</li><li>`EncryptionMethod=1`(啟用)</li><li>`EncryptionMethod=6`（請求SSL）</li></ul> |
| `ValidateServerCertificate` | 驗證您發送的證書 [!DNL PostgreSQL] 資料庫 `EncryptionMethod` 的子菜單。 | <uL><li>`ValidationServerCertificate=0`(停用)</li><li>`ValidationServerCertificate=1`(啟用)</li></ul> |

以下是 [!DNL PostgreSQL] 附加有SSL加密的連接字串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL PostgreSQL] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
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
| `auth.params.connectionString` | 與您的 [!DNL PostgreSQL] 帳戶。 的 [!DNL PostgreSQL] 連接字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 的 [!DNL PostgreSQL] 連接規範ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

**回應**

成功的響應返回唯一標識符(`id`)。 需要此ID來瀏覽 [!DNL PostgreSQL] 資料庫。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL PostgreSQL] 連接基連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
