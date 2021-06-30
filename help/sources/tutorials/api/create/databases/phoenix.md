---
keywords: Experience Platform；首頁；熱門主題；鳳凰；鳳凰
solution: Experience Platform
title: 使用Flow Service API建立Phoenix基本連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Phoenix資料庫連線至Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Phoenix]基本連線

>[!NOTE]
>
>[!DNL Phoenix]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API引導您完成將[!DNL Phoenix]資料庫連接到[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Phoenix]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Phoenix]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix]伺服器的IP地址或主機名。 |
| `username` | 用於訪問[!DNL Phoenix]伺服器的用戶名。 |
| `password` | 與用戶對應的密碼。 |
| `port` | [!DNL Phoenix]伺服器用於偵聽客戶端連接的TCP埠。 如果連接到[!DNL Azure] HDInsights，請將埠指定為443。 |
| `httpPath` | 與[!DNL Phoenix]伺服器對應的部分URL。 如果使用[!DNL Azure] HDInsights群集，請指定/hbasephoenix0。 |
| `enableSsl` | 布林值。 指定是否使用SSL加密與伺服器的連接。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Phoenix]的連接規範ID為：`102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有關入門的詳細資訊，請參閱[此Phoenix文檔](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Phoenix]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Phoenix]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Phoenix]伺服器的主機。 |
| `auth.params.username` | 與您的[!DNL Phoenix]連接相關聯的用戶名。 |
| `auth.params.password` | 與[!DNL Phoenix]連接相關聯的密碼。 |
| `auth.params.port` | [!DNL Phoenix]連接的TCP埠。 |
| `auth.params.httpPath` | [!DNL Phoenix]連接的部分http路徑。 |
| `auth.params.enableSsl` | 指定是否使用SSL加密與伺服器的連接的布爾值。 |
| `connectionSpec.id` | [!DNL Phoenix]連接規範ID:`102706fb-a5cd-42ee-afe0-bc42f017ff43`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Phoenix]連線，並取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何使用流量服務API](../../explore/database-nosql.md)探索資料庫。[
