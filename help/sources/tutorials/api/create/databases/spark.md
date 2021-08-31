---
keywords: Experience Platform；首頁；熱門主題；Apache Spark;Apache Spark;Azure HDInsights
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights Base Connection上建立Apache Spark
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Azure HDInsights上的Apache Spark連線至Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API在[!DNL Azure] HDInsights基本連線上建立[!DNL Apache Spark]

>[!NOTE]
>
>[!DNL Azure HDInsights]連接器上的[!DNL Apache Spark]為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，在[!DNL Azure HDInsights]（以下稱為「[!DNL Spark]」）上建立[!DNL Apache Spark]基本連線。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Spark]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Spark]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Spark]伺服器的IP地址或主機名。 |
| `username` | 用於訪問[!DNL Spark]伺服器的用戶名。 |
| `password` | 與用戶對應的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Spark]的連接規範ID為：`6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

有關入門的詳細資訊，請參閱[此Spark文檔](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Spark]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Spark]建立基本連接：


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
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
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
| `auth.params.username` | 與您的[!DNL Spark]連接相關聯的用戶名。 |
| `auth.params.password` | 與[!DNL Spark]連接相關聯的密碼。 |
| `connectionSpec.id` | [!DNL Spark]連接規範ID:`6a8d82bc-1caf-45d1-908d-cadabc9d63a6`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Spark]連線，並取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何使用流量服務API](../../explore/database-nosql.md)探索資料庫。[
