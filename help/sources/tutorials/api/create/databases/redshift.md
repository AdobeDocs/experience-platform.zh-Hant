---
keywords: Experience Platform；首頁；熱門主題；Redshift;Redshift;Amazon Redshift;Amazon Redshift
solution: Experience Platform
title: 使用流服務API建立Amazon Redshift基本連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連接到Amazon Redshift。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 600b216932a7d19440534c4b190fb2f3766c8785
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Amazon Redshift]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Amazon Redshift]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Amazon Redshift]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Amazon Redshift]連接，必須提供以下連接屬性：

| **憑據** | **說明** |
| -------------- | --------------- |
| `server` | 與[!DNL Amazon Redshift]帳戶相關聯的伺服器。 |
| `username` | 與您的[!DNL Amazon Redshift]帳戶相關聯的使用者名稱。 |
| `password` | 與[!DNL Amazon Redshift]帳戶相關聯的密碼。 |
| `database` | 您正在訪問的[!DNL Amazon Redshift]資料庫。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Amazon Redshift]的連接規範ID為`3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

有關入門的詳細資訊，請參閱此[[!DNL Amazon Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Amazon Redshift]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Amazon Redshift]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.server` | 您的[!DNL Amazon Redshift]伺服器。 |
| `auth.params.database` | 與[!DNL Amazon Redshift]帳戶相關聯的資料庫。 |
| `auth.params.password` | 與[!DNL Amazon Redshift]帳戶相關聯的密碼。 |
| `auth.params.username` | 與您的[!DNL Amazon Redshift]帳戶相關聯的使用者名稱。 |
| `connectionSpec.id` | [!DNL Amazon Redshift]連接規範ID:`3416976c-a9ca-4bba-901a-1f08f66978ff` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Amazon Redshift]連線，並取得連線的唯一ID值。 在學習如何使用流服務API](../../explore/database-nosql.md)來瀏覽資料庫或NoSQL系統時，您可以在下一個教程中使用此連接ID。[
