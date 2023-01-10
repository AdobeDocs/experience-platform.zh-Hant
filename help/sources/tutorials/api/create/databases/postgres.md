---
keywords: Experience Platform；首頁；熱門主題；PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: 使用流服務API建立PostgreSQL基連接
type: Tutorial
description: 了解如何使用流程服務API將Adobe Experience Platform連線至PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# 建立 [!DNL PostgreSQL] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL PostgreSQL] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL PostgreSQL] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL PostgreSQL]，您必須提供下列連線屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與 [!DNL PostgreSQL] 帳戶。 此 [!DNL PostgreSQL] 連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL PostgreSQL] is `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

有關獲取連接字串的詳細資訊，請參閱 [[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/9.2/app-psql.html).

#### 為連線字串啟用SSL加密

您可以為 [!DNL PostgreSQL] 連線字串，方法是使用下列屬性附加連線字串：

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `EncryptionMethod` | 可讓您在 [!DNL PostgreSQL] 資料。 | <uL><li>`EncryptionMethod=0`(停用)</li><li>`EncryptionMethod=1`(啟用)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 驗證您所傳送的憑證 [!DNL PostgreSQL] 資料庫 `EncryptionMethod` 中所有規則的URL區段。 | <uL><li>`ValidationServerCertificate=0`(停用)</li><li>`ValidationServerCertificate=1`(啟用)</li></ul> |

以下是 [!DNL PostgreSQL] 附加了SSL加密的連接字串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL PostgreSQL] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL PostgreSQL]:

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
| `auth.params.connectionString` | 與 [!DNL PostgreSQL] 帳戶。 此 [!DNL PostgreSQL] 連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 此 [!DNL PostgreSQL] 連接規範ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 瀏覽您的 [!DNL PostgreSQL] 資料庫。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL PostgreSQL] 連接基連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
