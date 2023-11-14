---
keywords: Experience Platform；首頁；熱門主題；Apache Spark；Apache Spark；Azure HDInsights
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights基本連線上建立Apache Spark
type: Tutorial
description: 瞭解如何使用流量服務API將Azure HDInsights上的Apache Spark連線至Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 建立 [!DNL Apache Spark] 於 [!DNL Azure] HDInsights基本連線使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Apache Spark] 於 [!DNL Azure HDInsights] 聯結器為Beta版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Apache Spark] 於 [!DNL Azure HDInsights] (以下稱「[!DNL Spark]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用以下專案來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需的其他資訊 [!DNL Spark] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Spark]，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Spark] 伺服器。 |
| `username` | 您用來存取的使用者名稱 [!DNL Spark] 伺服器。 |
| `password` | 與使用者對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Spark] 為： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

如需開始使用的詳細資訊，請參閱 [此Spark檔案](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL Spark] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL Spark]：


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | 的主機 [!DNL Spark] 伺服器。 |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Spark] 連線。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Spark] 連線。 |
| `connectionSpec.id` | 此 [!DNL Spark] 連線規格ID： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Spark] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
