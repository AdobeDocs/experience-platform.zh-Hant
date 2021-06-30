---
keywords: Experience Platform；首頁；熱門主題；MariaDB;mariadb
solution: Experience Platform
title: 使用流服務API建立MariaDB基連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至MariaDB。
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL MariaDB]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL MariaDB]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL MariaDB]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL MariaDB]連接，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與[!DNL MariaDB]驗證相關聯的連線字串。 [!DNL MariaDB]連接字串模式為：`Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL MariaDB]的連接規範ID為`3000eb99-cd47-43f3-827c-43caf170f015`。 |

有關獲取連接字串的詳細資訊，請參閱此[[!DNL MariaDB] document](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL MariaDB]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL MariaDB]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for maria-db",
        "description": "Test connection for maria-db",
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
| `auth.params.connectionString` | 與[!DNL MariaDB]驗證相關聯的連線字串。 [!DNL MariaDB]連接字串模式為：`Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL MariaDB]連接規範ID為：`3000eb99-cd47-43f3-827c-43caf170f015`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步中瀏覽資料庫時需要此ID。

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL MariaDB]連線，並取得連線的唯一ID值。 在學習如何使用流服務API](../../explore/database-nosql.md)來瀏覽資料庫或NoSQL系統時，您可以在下一個教程中使用此連接ID。[
