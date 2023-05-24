---
keywords: Experience Platform；首頁；熱門主題；紅移；紅移；Amazon紅移；亞馬遜紅移
solution: Experience Platform
title: 使用流服務API建立Amazon紅移基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform與Amazon紅移連接。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 建立 [!DNL Amazon Redshift] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Amazon Redshift] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Amazon Redshift] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Amazon Redshift]，必須提供以下連接屬性：

| **憑據** | **說明** |
| -------------- | --------------- |
| `server` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `username` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `password` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `database` | 的 [!DNL Amazon Redshift] 正在訪問的資料庫。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Amazon Redshift] 是 `3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

有關入門的詳細資訊，請參閱此 [[!DNL Amazon Redshift] 文檔](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

>[!NOTE]
>
>的預設編碼標準 [!DNL Redshift] 是Unicode。 不能更改。

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Amazon Redshift] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Amazon Redshift]:

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
| `auth.params.server` | 您 [!DNL Amazon Redshift] 伺服器。 |
| `auth.params.database` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.username` | 與您的 [!DNL Amazon Redshift] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Amazon Redshift] 連接規範ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Amazon Redshift] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
