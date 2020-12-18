---
keywords: Experience Platform;home;popular topics;Apache hive;hive;Hive
solution: Experience Platform
title: 在Azure HDInsights連接器上使用Flow Service API建立Apache Hive
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Azure HDInsights上的Apache Hive連線至Experience Platform的步驟。
translation-type: tm+mt
source-git-commit: 36620a229fc8e6e3fa4545bfc775a49bc89935bb
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API在[!DNL Azure HDInsights]連接器上建立[!DNL Apache Hive]

>[!NOTE]
>
>[!DNL Azure HDInsights]連接器上的[!DNL Apache Hive]為beta。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Azure HDInsights]上的[!DNL Apache Hive]連接至[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Hive]。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Hive]連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Hive]伺服器的IP地址或主機名。 |
| `username` | 用於訪問[!DNL Hive]伺服器的用戶名。 |
| `password` | 與用戶對應的密碼。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Hive]的連接規範ID為：`aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

有關入門的詳細資訊，請參閱[此Hive文檔](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

#### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個Hive帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立[!DNL Hive]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Hive]的連接規範ID為`aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 與[!DNL Hive]帳戶關聯的連接字串。 |
| `connectionSpec.id` | [!DNL Hive]連接規範ID:`aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Hive]連接，並獲取了該連接的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使用流服務API[來探索資料庫。](../../explore/database-nosql.md)
