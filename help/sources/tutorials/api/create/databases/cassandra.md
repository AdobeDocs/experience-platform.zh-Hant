---
keywords: Experience Platform；首頁；熱門主題；Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: 使用流服務API建立Apache Cassandra源連接
type: Tutorial
description: 瞭解如何使用流服務API將Apache Cassandra連接到Adobe Experience Platform。
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 建立 [!DNL Apache Cassandra] 源連接使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [!DNL Flow Service] API，引導您完成連接的步驟 [!DNL Apache Cassandra] （下稱「Cassandra」） [!DNL Experience Platform]。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Cassandra]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP地址或主機名 [!DNL Cassandra] 伺服器。 |
| `port` | TCP埠 [!DNL Cassandra] 伺服器用於偵聽客戶端連接。 預設埠為 `9042`。 |
| `username` | 用於連接到 [!DNL Cassandra] 伺服器進行身份驗證。 |
| `password` | 連接到的密碼 [!DNL Cassandra] 伺服器進行身份驗證。 |
| `connectionSpec.id` | 建立連接所需的唯一標識符。 連接規範ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

有關入門的詳細資訊，請參閱 [這份卡桑德拉檔案](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

## 建立連線

連接指定源並包含該源的憑據。 每個只需要一個連接器 [!DNL Cassandra] 帳戶，因為它可用於建立多個源連接器以引入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

為了建立 [!DNL Cassandra] 連接，其唯一連接規範ID必須作為POST請求的一部分提供。 連接規範ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。

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
| `auth.params.host` | 的IP地址或主機名 [!DNL Cassandra] 伺服器。 |
| `auth.params.port` | TCP埠 [!DNL Cassandra] 伺服器用於偵聽客戶端連接。 預設埠為 `9042`。 |
| `auth.params.username` | 用於連接到 [!DNL Cassandra] 伺服器進行身份驗證。 |
| `auth.params.password` | 連接到的密碼 [!DNL Cassandra] 伺服器進行身份驗證。 |
| `connectionSpec.id` | 的 [!DNL Cassandra] 連接規範ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Cassandra] 使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 在學習如何 [使用流服務API瀏覽資料庫](../../explore/database-nosql.md)。
