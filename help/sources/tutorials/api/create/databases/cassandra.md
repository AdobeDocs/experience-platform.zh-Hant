---
keywords: Experience Platform;home;popular topics;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: 使用Flow Service API建立Apache Cassandra連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Apache Cassandra（以下稱為「Cassandra」）連接至Experience Platform的步驟。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---


# 使用 [!DNL Apache Cassandra] API建立連 [!DNL Flow Service] 接器

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連接 [!DNL Apache Cassandra] （以下稱為「Cassandra」）至的步驟 [!DNL Experience Platform]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API成功連線至Cassandra。

### 收集必要的認證

要連接 [!DNL Flow Service] ，必須為以 [!DNL Cassandra]下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 伺服器的IP地址或主 [!DNL Cassandra] 機名。 |
| `port` | 伺服器用於監聽 [!DNL Cassandra] 客戶機連接的TCP埠。 The default port is `9042`. |
| `username` | 用於連接到伺服器以進行驗 [!DNL Cassandra] 證的用戶名。 |
| `password` | 連線至伺服器以進行驗 [!DNL Cassandra] 證的密碼。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 的連接規範ID [!DNL Cassandra] 為 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

有關快速入門的詳細資訊，請參 [閱此Cassandra檔案](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個帳戶只需要一個連 [!DNL Cassandra] 接器，因為它可用於建立多個來源連接器以匯入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立連接，必 [!DNL Cassandra] 須在POST請求中提供其唯一連接規範ID。 的連接規範ID [!DNL Cassandra] 為 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | 伺服器的IP地址或主 [!DNL Cassandra] 機名。 |
| `auth.params.port` | 伺服器用於監聽 [!DNL Cassandra] 客戶機連接的TCP埠。 The default port is `9042`. |
| `auth.params.username` | 用於連接到伺服器以進行驗 [!DNL Cassandra] 證的用戶名。 |
| `auth.params.password` | 連線至伺服器以進行驗 [!DNL Cassandra] 證的密碼。 |
| `connectionSpec.id` | 連 [!DNL Cassandra] 接規範ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 後續步驟

在本教學課程中，您已使 [!DNL Cassandra] 用 [!DNL Flow Service] API建立連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使 [用Flow Service API來探索資料庫](../../explore/database-nosql.md)。
