---
keywords: Experience Platform；主題；熱門主題；ApacheHadoop分佈式檔案系統；Apachehadoop;hdfs;HDFS
solution: Experience Platform
title: 使用流服務API建立Apache HDFS基連接
type: Tutorial
description: 瞭解如何使用流服務API將ApacheHadoop分佈式檔案系統連接到Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 建立 [!DNL Apache] HDFS基連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>Apache HDFS連接器為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Apache Hadoop Distributed File System] (以下簡稱：[!DNL HDFS]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL HDFS] 使用 [!DNL Flow Service] API。

### 收集所需憑據

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | URL定義連接到所需的身份驗證參數 [!DNL HDFS] 匿名。 有關如何獲取此值的詳細資訊，請參閱 [這個 [!DNL HDFS] 文檔](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL AdWords] 為： `54e221aa-d342-4707-bcff-7a4bceef0001`。 |

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL HDFS] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL HDFS]:

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
| `auth.params.url` | 定義連接所需的身份驗證參數的URL [!DNL HDFS] 匿名 |
| `connectionSpec.id` | 的 [!DNL HDFS] 連接規範ID: `54e221aa-d342-4707-bcff-7a4bceef0001`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL HDFS] 使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 在學習如何 [使用流服務API瀏覽第三方雲儲存](../../explore/cloud-storage.md)。
