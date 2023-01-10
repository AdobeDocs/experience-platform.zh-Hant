---
keywords: Experience Platform；首頁；熱門主題；鳳凰；鳳凰
solution: Experience Platform
title: 使用Flow Service API建立Phoenix基本連線
type: Tutorial
description: 了解如何使用Flow Service API將Phoenix資料庫連線至Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 建立 [!DNL Phoenix] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Phoenix] 連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用 [!DNL Flow Service] API可引導您完成連線步驟 [!DNL Phoenix] 資料庫 [!DNL Experience Platform].

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Phoenix]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Phoenix] 伺服器。 |
| `username` | 您用來存取的使用者名稱 [!DNL Phoenix] 伺服器。 |
| `password` | 與用戶對應的密碼。 |
| `port` | TCP埠 [!DNL Phoenix] 伺服器用於偵聽客戶端連接。 如果您連線至 [!DNL Azure] HDInsights，將埠指定為443。 |
| `httpPath` | 與 [!DNL Phoenix] 伺服器。 如果使用 [!DNL Azure] HDInsights群集。 |
| `enableSsl` | 布林值。 指定是否使用SSL加密與伺服器的連接。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Phoenix] 為： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

如需快速入門的詳細資訊，請參閱 [這份鳳凰號檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Phoenix] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Phoenix]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
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
| `auth.params.host` | 主機 [!DNL Phoenix] 伺服器。 |
| `auth.params.username` | 與您的 [!DNL Phoenix] 連線。 |
| `auth.params.password` | 與您的 [!DNL Phoenix] 連線。 |
| `auth.params.port` | 您的TCP埠 [!DNL Phoenix] 連線。 |
| `auth.params.httpPath` | 您的 [!DNL Phoenix] 連線。 |
| `auth.params.enableSsl` | 指定是否使用SSL加密與伺服器的連接的布爾值。 |
| `connectionSpec.id` | 此 [!DNL Phoenix] 連接規範ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Phoenix] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
