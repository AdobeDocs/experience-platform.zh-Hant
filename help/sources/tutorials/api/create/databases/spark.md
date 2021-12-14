---
keywords: Experience Platform；首頁；熱門主題；Apache Spark;Apache Spark;Azure HDInsights
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights Base Connection上建立Apache Spark
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Azure HDInsights上的Apache Spark連線至Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 建立 [!DNL Apache Spark] on [!DNL Azure] HDInsights基本連接，使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Apache Spark] on [!DNL Azure HDInsights] 連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Apache Spark] on [!DNL Azure HDInsights] (下稱「[!DNL Spark]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Spark] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Spark]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Spark] 伺服器。 |
| `username` | 您用來存取的使用者名稱 [!DNL Spark] 伺服器。 |
| `password` | 與用戶對應的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Spark] 為： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

如需快速入門的詳細資訊，請參閱 [這個Spark檔案](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Spark] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Spark]:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 主機 [!DNL Spark] 伺服器。 |
| `auth.params.username` | 與您的 [!DNL Spark] 連線。 |
| `auth.params.password` | 與您的 [!DNL Spark] 連線。 |
| `connectionSpec.id` | 此 [!DNL Spark] 連接規範ID: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Spark] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何 [使用流服務API瀏覽資料庫](../../explore/database-nosql.md).
