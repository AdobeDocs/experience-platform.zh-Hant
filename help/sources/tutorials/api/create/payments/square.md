---
keywords: Experience Platform；首頁；熱門主題；方形；方形
title: 使用流量服務API建立方形基底連線
description: 瞭解如何使用流量服務API將Square連線至Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL Square]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Square]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一Experience Platform執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Square]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Square]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| `host` | [!DNL Square]執行個體的網址。 |
| `clientId` | 與您的[!DNL Square]帳戶相關聯的使用者端ID。 |
| `clientSecret` | 與您的[!DNL Square]帳戶相關聯的使用者端密碼。 |
| `accessToken` | 存取權杖是用來驗證您的[!DNL Square]帳戶（具有OAuth 2.0驗證）。 存取權杖可從[!DNL Square]取得。 |
| `refreshToken` | 重新整理權杖會在您目前的存取權杖過期後，用來產生新的存取權杖。 可從[!DNL Square]取得重新整理權杖。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Square]的連線規格識別碼為： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

如需這些認證以及如何取得認證的詳細資訊，請參閱OAuth[&#128279;](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)上的[!DNL Square] 檔案。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Square]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Square]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Square]執行個體的網址。 |
| `auth.params.clientId` | 與您的[!DNL Square]帳戶相關聯的使用者端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL Square]帳戶相關聯的使用者端密碼。 |
| `auth.params.accessToken` | 存取權杖是用來驗證您的[!DNL Square]帳戶（具有OAuth 2.0驗證）。 存取權杖可從[!DNL Square]取得。 |
| `auth.params.refreshToken` | 重新整理權杖會在您目前的存取權杖過期後，用來產生新的存取權杖。 可從[!DNL Square]取得重新整理權杖。 |
| `connectionSpec.id` | [!DNL Square]連線規格識別碼： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 後續步驟

依照本教學課程中的指示，您已使用[!DNL Flow Service] API建立[!DNL Square]連線，並已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何使用Flow Service API[&#128279;](../../explore/payments.md)來探索付款應用程式。
