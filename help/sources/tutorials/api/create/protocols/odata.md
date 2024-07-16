---
keywords: Experience Platform；首頁；熱門主題；通用OData；通用OData
solution: Experience Platform
title: 使用Flow Service API建立一般OData基底連線
type: Tutorial
description: 瞭解如何使用流量服務API將Generic OData連線到Adobe Experience Platform。
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Generic OData]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Generic OData]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Generic OData]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Generic OData]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `url` | [!DNL Generic OData]服務的根URL。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Generic Generic OData]的連線規格識別碼為： `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL Generic OData] 檔案](https://www.odata.org/getting-started/basic-tutorial/)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Generic OData]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Generic OData]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url":  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.url` | [!DNL Generic OData]伺服器的主機。 |
| `connectionSpec.id` | [!DNL Generic OData]連線規格識別碼： `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Generic REST OData]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將通訊協定資料帶入Platform](../../collect/protocols.md)
