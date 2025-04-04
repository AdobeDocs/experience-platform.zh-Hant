---
keywords: Experience Platform；首頁；熱門主題；Apache Cassandra；Apache cassandra；Cassandra；cassandra
solution: Experience Platform
title: 使用流量服務API建立Apache Cassandra Source連線
type: Tutorial
description: 瞭解如何使用流量服務API將Apache Cassandra連線至Adobe Experience Platform。
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---


# 使用[!DNL Flow Service] API建立[!DNL Apache Cassandra]來源連線

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

本教學課程使用[!DNL Flow Service] API逐步引導您完成將[!DNL Apache Cassandra] （以下稱為「Cassandra」）連線到[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到Cassandra。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Cassandra]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Cassandra]伺服器的IP位址或主機名稱。 |
| `port` | [!DNL Cassandra]伺服器用來監聽使用者端連線的TCP連線埠。 預設連線埠為`9042`。 |
| `username` | 用來連線至[!DNL Cassandra]伺服器以進行驗證的使用者名稱。 |
| `password` | 連線到[!DNL Cassandra]伺服器以進行驗證的密碼。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Cassandra]的連線規格識別碼為`a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

如需開始使用的詳細資訊，請參閱[此Cassandra檔案](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 建立連線

連線會指定來源，並包含該來源的認證。 每個[!DNL Cassandra]帳戶只需要一個聯結器，因為它可用來建立多個來源聯結器以匯入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

為了建立[!DNL Cassandra]連線，必須在POST要求中提供其唯一的連線規格ID。 [!DNL Cassandra]的連線規格識別碼為`a8f4d393-1a6b-43f3-931f-91a16ed857f4`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Cassandra]伺服器的IP位址或主機名稱。 |
| `auth.params.port` | [!DNL Cassandra]伺服器用來監聽使用者端連線的TCP連線埠。 預設連線埠為`9042`。 |
| `auth.params.username` | 用來連線至[!DNL Cassandra]伺服器以進行驗證的使用者名稱。 |
| `auth.params.password` | 連線到[!DNL Cassandra]伺服器以進行驗證的密碼。 |
| `connectionSpec.id` | [!DNL Cassandra]連線規格識別碼： `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 後續步驟

依照本教學課程中的指示，您已使用[!DNL Flow Service] API建立[!DNL Cassandra]連線，並已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何使用Flow Service API](../../explore/database-nosql.md)來探索資料庫[。
