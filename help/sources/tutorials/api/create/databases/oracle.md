---
keywords: Experience Platform；首頁；熱門主題；Oracle；oracle
solution: Experience Platform
title: 使用流量服務API建立Oracle基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Oracle連線至Experience Platform。
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Oracle]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Oracle]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Oracle]。

| 認證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用來連線到[!DNL Oracle]的連線字串。 [!DNL Oracle]連線字串模式為： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Oracle]的連線規格識別碼為`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 |

如需開始使用的詳細資訊，請參閱此[[!DNL Oracle] 檔案](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Oracle]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Oracle]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle connection",
        "description": "A connection for Oracle",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                    "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 用來連線到您[!DNL Oracle]資料庫的連線字串。 [!DNL Oracle]連線字串模式為： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL Oracle]連線規格識別碼： `d6b52d86-f0f8-475f-89d4-ce54c8527328`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Oracle]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
