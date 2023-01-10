---
keywords: Experience Platform；首頁；熱門主題；Redshift;Redshift;Amazon Redshift;Amazon Redshift
solution: Experience Platform
title: 使用流服務API建立Amazon Redshift基本連接
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連接到Amazon Redshift。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 建立 [!DNL Amazon Redshift] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Amazon Redshift] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Amazon Redshift] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Amazon Redshift]，您必須提供下列連線屬性：

| **憑據** | **說明** |
| -------------- | --------------- |
| `server` | 與 [!DNL Amazon Redshift] 帳戶。 |
| `username` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `password` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `database` | 此 [!DNL Amazon Redshift] 您正在訪問的資料庫。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Amazon Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

如需快速入門的詳細資訊，請參閱 [[!DNL Amazon Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

>[!NOTE]
>
>的預設編碼標準 [!DNL Redshift] 為Unicode。 無法變更。

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Amazon Redshift] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | 您的 [!DNL Amazon Redshift] 伺服器。 |
| `auth.params.database` | 與 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.username` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Amazon Redshift] 連接規範ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Amazon Redshift] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
