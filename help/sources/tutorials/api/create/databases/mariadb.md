---
keywords: Experience Platform；首頁；熱門主題；MariaDB;mariadb
solution: Experience Platform
title: 使用流服務API建立MariaDB基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到MariaDB。
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# 建立 [!DNL MariaDB] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL MariaDB] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL MariaDB] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL MariaDB]，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的 [!DNL MariaDB] 驗證。 的 [!DNL MariaDB] 連接字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL MariaDB] 是 `3000eb99-cd47-43f3-827c-43caf170f015`。 |

有關獲取連接字串的詳細資訊，請參閱 [[!DNL MariaDB] 文檔](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL MariaDB] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL MariaDB]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.connectionString` | 與您的 [!DNL MariaDB] 驗證。 的 [!DNL MariaDB] 連接字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 的 [!DNL MariaDB] 連接規範ID為： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步中瀏覽資料庫時需要此ID。

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL MariaDB] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
