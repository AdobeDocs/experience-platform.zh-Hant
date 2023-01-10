---
keywords: Experience Platform；首頁；熱門主題；Apache Cassandra;Apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: 使用Flow Service API建立Apache Cassandra Source Connection
type: Tutorial
description: 了解如何使用Flow Service API將Apache Cassandra連線至Adobe Experience Platform。
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 建立 [!DNL Apache Cassandra] 源連接使用 [!DNL Flow Service] API

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用 [!DNL Flow Service] API可引導您完成連線步驟 [!DNL Apache Cassandra] （以下簡稱「卡珊卓」） [!DNL Experience Platform].

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Cassandra]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Cassandra] 伺服器。 |
| `port` | TCP埠 [!DNL Cassandra] 伺服器用於偵聽客戶端連接。 預設埠為 `9042`. |
| `username` | 用來連線至 [!DNL Cassandra] 伺服器進行驗證。 |
| `password` | 連線至的密碼 [!DNL Cassandra] 伺服器進行驗證。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 的連接規範ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

如需快速入門的詳細資訊，請參閱 [這個卡珊德拉檔案](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個只需一個連接器 [!DNL Cassandra] 帳戶，因為它可用來建立多個來源連接器，以匯入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

若要建立 [!DNL Cassandra] 連接，其唯一連接規範ID必須作為POST請求的一部分提供。 的連接規範ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | 的IP位址或主機名稱 [!DNL Cassandra] 伺服器。 |
| `auth.params.port` | TCP埠 [!DNL Cassandra] 伺服器用於偵聽客戶端連接。 預設埠為 `9042`. |
| `auth.params.username` | 用來連線至 [!DNL Cassandra] 伺服器進行驗證。 |
| `auth.params.password` | 連線至的密碼 [!DNL Cassandra] 伺服器進行驗證。 |
| `connectionSpec.id` | 此 [!DNL Cassandra] 連接規格ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Cassandra] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何 [使用流服務API瀏覽資料庫](../../explore/database-nosql.md).
