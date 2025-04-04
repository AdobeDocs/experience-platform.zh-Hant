---
keywords: Experience Platform；首頁；熱門主題；Apache Hadoop分散式檔案系統；Apache Hadoop；hdfs；HDFS
solution: Experience Platform
title: 使用流量服務API建立Apache HDFS基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Apache Hadoop分散式檔案系統連結至Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Apache] HDFS基底連線

>[!NOTE]
>
>Apache HDFS聯結器為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Apache Hadoop Distributed File System] （以下稱為「[!DNL HDFS]」）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL HDFS]。

### 收集必要的認證

| 認證 | 說明 |
| ---------- | ----------- |
| `url` | URL定義匿名連線至[!DNL HDFS]所需的驗證引數。 如需有關如何取得此值的詳細資訊，請參閱[此 [!DNL HDFS] 檔案](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL AdWords]的連線規格識別碼為： `54e221aa-d342-4707-bcff-7a4bceef0001`。 |

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL HDFS]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL HDFS]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.url` | 定義匿名連線至[!DNL HDFS]所需的驗證引數的URL |
| `connectionSpec.id` | [!DNL HDFS]連線規格識別碼： `54e221aa-d342-4707-bcff-7a4bceef0001`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 後續步驟

依照本教學課程中的指示，您已使用[!DNL Flow Service] API建立[!DNL HDFS]連線，並已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何使用Flow Service API[探索協力廠商雲端儲存空間](../../explore/cloud-storage.md)。
