---
keywords: Experience Platform；首頁；熱門主題；ApacheHadoop分佈式檔案系統；Apachehadoop;hdfs; HDFS
solution: Experience Platform
title: 使用Flow Service API建立Apache HDFS基本連接
type: Tutorial
description: 了解如何使用Flow Service API將ApacheHadoop分佈式檔案系統連線至Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 建立 [!DNL Apache] HDFS基連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>Apache HDFS連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Apache Hadoop Distributed File System] (下稱「[!DNL HDFS]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL HDFS] 使用 [!DNL Flow Service] API。

### 收集所需憑據

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | URL定義連線至所需的驗證參數 [!DNL HDFS] 匿名。 如需如何取得此值的詳細資訊，請參閱 [此 [!DNL HDFS] 檔案](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL AdWords] 為： `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL HDFS] 驗證憑證作為要求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL HDFS]:

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
| `auth.params.url` | 定義連線至所需驗證參數的URL [!DNL HDFS] 匿名 |
| `connectionSpec.id` | 此 [!DNL HDFS] 連接規範ID: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL HDFS] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何 [使用流量服務API探索協力廠商雲端儲存空間](../../explore/cloud-storage.md).
