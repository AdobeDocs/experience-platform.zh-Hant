---
keywords: Experience Platform；首頁；熱門主題；Apache Spark；Apache Spark；Azure HDInsights
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights基本連線上建立Apache Spark
type: Tutorial
description: 瞭解如何使用流量服務API將Azure HDInsights上的Apache Spark連線至Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API在[!DNL Azure] HDInsights基本連線上建立[!DNL Apache Spark]

>[!NOTE]
>
>[!DNL Azure HDInsights]聯結器上的[!DNL Apache Spark]為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，在[!DNL Azure HDInsights] （以下稱為「[!DNL Spark]」）上建立[!DNL Apache Spark]的基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Spark]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Spark]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Spark]伺服器的IP位址或主機名稱。 |
| `username` | 您用來存取[!DNL Spark]伺服器的使用者名稱。 |
| `password` | 與使用者對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Spark]的連線規格識別碼為： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

如需開始使用的詳細資訊，請參閱[此Spark檔案](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Spark]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Spark]的基礎連線：


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
| `auth.params.host` | [!DNL Spark]伺服器的主機。 |
| `auth.params.username` | 與您的[!DNL Spark]連線相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL Spark]連線相關聯的密碼。 |
| `connectionSpec.id` | [!DNL Spark]連線規格識別碼： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Spark]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶到Platform](../../collect/database-nosql.md)
