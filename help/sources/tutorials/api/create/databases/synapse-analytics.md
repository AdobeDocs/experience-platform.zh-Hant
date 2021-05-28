---
keywords: Experience Platform；首頁；熱門主題；Synapse;Synapse;Azure synapse分析
solution: Experience Platform
title: 使用流程服務API建立Azure synapseAnalytics來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Azure synapseAnalytics連線至Adobe Experience Platform。
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Synapse Analytics]源連接

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

了解如何將[!DNL Azure Synapse Analytics]（以下稱為「[!DNL Synapse]」）連接至[!DNL Experience Platform]。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Synapse]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Synapse]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到[!DNL Synapse]的連接字串。 [!DNL Synapse]連接字串模式為`Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Synapse]的連接規範ID為：`a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |

有關獲取連接字串的詳細資訊，請參閱[此Synapse文檔](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure?toc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Ftoc.json&amp;bc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Fbreadcrumb%2Ftoc.json&amp;tabs=azure-powershell)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都會隔離至特定虛擬沙箱。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Synapse]帳戶只需一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

若要建立[!DNL Synapse]連線，必須在POST請求中提供其唯一連線規格ID。 [!DNL Synapse]的連接規範ID為`a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for Azure Synapse Analytics",
        "description": "Connection for Azure Synapse Analytics",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectionSpec": {
            "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 用於連接到[!DNL Synapse]的連接字串。 [!DNL Synapse]連接字串模式為`Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |
| `connectionSpec.id` | [!DNL Synapse]連接規範ID為：`a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料庫時需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Synapse]連線，並取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何使用流量服務API](../../explore/database-nosql.md)探索資料庫。[
