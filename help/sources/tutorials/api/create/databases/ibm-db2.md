---
keywords: Experience Platform；首頁；熱門主題；IBM [!DNL IBM DB2]；IBM；ibm [!DNL IBM DB2]；[!DNL IBM DB2]；[!DNL IBM DB2]
solution: Experience Platform
title: 使用Flow Service API建立IBM [!DNL IBM DB2] 基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將IBM [!DNL IBM DB2] 連線至Adobe Experience Platform。
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立IBM [!DNL IBM DB2]基本連線

>[!NOTE]
>
>IBM [!DNL IBM DB2]聯結器為Beta版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL IBM DB2]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL IBM DB2]。

| 認證 | 說明 |
| ---------- | ----------- |
| `server` | [!DNL IBM DB2]伺服器的名稱。 您可以在以冒號分隔的伺服器名稱后面指定連線埠號碼。 例如：server：port。 |
| `database` | [!DNL IBM DB2]資料庫的名稱。 |
| `username` | 用來連線至[!DNL IBM DB2]資料庫的使用者名稱。 |
| `password` | 您為使用者名稱指定的使用者帳戶密碼。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL IBM DB2]的連線規格識別碼為`09182899-b429-40c9-a15a-bf3ddbc8ced7`。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL IBM DB2] 檔案](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL IBM DB2]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL IBM DB2]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 與您的[!DNL IBM DB2]帳戶關聯的連線字串。 |
| `connectionSpec.id` | [!DNL IBM DB2]連線規格識別碼： `09182899-b429-40c9-a15a-bf3ddbc8ced7`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL IBM DB2]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶到Platform](../../collect/database-nosql.md)

