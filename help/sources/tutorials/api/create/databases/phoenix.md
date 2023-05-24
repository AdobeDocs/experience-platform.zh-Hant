---
keywords: Experience Platform；主題；熱門主題；鳳凰；phoenix
solution: Experience Platform
title: 使用流服務API建立Phoenix基連接
type: Tutorial
description: 瞭解如何使用流服務API將Phoenix資料庫連接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 建立 [!DNL Phoenix] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Phoenix] 連接器位於beta中。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [!DNL Flow Service] API，引導您完成連接 [!DNL Phoenix] 資料庫 [!DNL Experience Platform]。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Phoenix]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP地址或主機名 [!DNL Phoenix] 伺服器。 |
| `username` | 用於訪問的用戶名 [!DNL Phoenix] 伺服器。 |
| `password` | 與用戶對應的密碼。 |
| `port` | TCP埠 [!DNL Phoenix] 伺服器用於偵聽客戶端連接。 如果連接到 [!DNL Azure] HDInsights，將埠指定為443。 |
| `httpPath` | 與 [!DNL Phoenix] 伺服器。 如果使用 [!DNL Azure] HDInsights群集。 |
| `enableSsl` | 布爾值。 指定是否使用SSL加密與伺服器的連接。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Phoenix] 為： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有關入門的詳細資訊，請參閱 [這份菲尼克斯檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Phoenix] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Phoenix]:

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
| `auth.params.username` | 與您的 [!DNL Phoenix] 連接。 |
| `auth.params.password` | 與您的 [!DNL Phoenix] 連接。 |
| `auth.params.port` | 您的TCP埠 [!DNL Phoenix] 連接。 |
| `auth.params.httpPath` | 您的部分http路徑 [!DNL Phoenix] 連接。 |
| `auth.params.enableSsl` | 用於指定是否使用SSL加密與伺服器的連接的布爾值。 |
| `connectionSpec.id` | 的 [!DNL Phoenix] 連接規範ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Phoenix] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
