---
keywords: Experience Platform；首頁；熱門主題；Apache Hive；Hive；Hive
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights基本連線上建立Apache Hive
type: Tutorial
description: 瞭解如何使用流量服務API將Azure HDInsights上的Apache Hive連線到Adobe Experience Platform。
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API在[!DNL Azure HDInsights]基礎連線上建立[!DNL Apache Hive]

>[!NOTE]
>
>[!DNL Azure HDInsights]聯結器上的[!DNL Apache Hive]為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，在[!DNL Azure HDInsights] （以下稱為「[!DNL Hive]」）上建立[!DNL Apache Hive]的基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Hive]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Hive]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Hive]伺服器的IP位址或主機名稱。 |
| `username` | 您用來存取[!DNL Hive]伺服器的使用者名稱。 |
| `password` | 與使用者對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Hive]的連線規格識別碼為： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

如需開始使用的詳細資訊，請參閱[此Hive檔案](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Hive]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Hive]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.connectionString` | 與您的[!DNL Hive]帳戶關聯的連線字串。 |
| `connectionSpec.id` | [!DNL Hive]連線規格識別碼： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API在[!DNL Azure HDInsights]基礎連線上建立[!DNL Apache Hive]。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
