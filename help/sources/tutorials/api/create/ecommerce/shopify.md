---
keywords: Experience Platform；首頁；熱門主題；Shopify；Shopify；電子商務
solution: Experience Platform
title: 使用流量服務API建立Shopify聯結器基礎連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Shopify連線至Adobe Experience Platform。
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API建立[!DNL Shopify]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Shopify] （以下稱為「[!DNL Shopify]」）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Sources]](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Shopify]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Shopify]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Shopify]伺服器的端點。 |
| `accessToken` | 您的[!DNL Shopify]使用者帳戶的存取權杖。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Shopify]的連線規格識別碼為： `4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

如需開始使用的詳細資訊，請參閱此[Shopify驗證檔案](https://shopify.dev/concepts/about-apis/authentication)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Shopify]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Shopify]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Shopify]伺服器的端點。 |
| `auth.params.accessToken` | 您的[!DNL Shopify]使用者帳戶的存取權杖。 |
| `connectionSpec.id` | [!DNL Shopify]連線規格識別碼： `4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Shopify]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流，將E-Commerce資料帶入Experience Platform](../../collect/ecommerce.md)
