---
keywords: Experience Platform；首頁；熱門主題；hubspot；Hubspot
solution: Experience Platform
title: 使用Flow Service API建立HubSpot基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL HubSpot]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL HubSpot]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL HubSpot]。

### 收集必要的認證

若要讓[!DNL Flow Service]與[!DNL HubSpot]連線，您必須提供下列連線屬性：

| 認證 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的[!DNL HubSpot]應用程式關聯的使用者端識別碼。 |
| `clientSecret` | 與您的[!DNL HubSpot]應用程式關聯的使用者端密碼。 |
| `accessToken` | 最初驗證您的OAuth整合時獲得的存取權杖。 |
| `refreshToken` | 重新整理權杖是在最初驗證您的OAuth整合時取得。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL HubSpot]的連線規格識別碼為： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

如需開始使用的詳細資訊，請參閱此[HubSpot檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL HubSpot]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL HubSpot]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的[!DNL HubSpot]應用程式關聯的使用者端識別碼。 |
| `auth.params.clientSecret` | 與您的[!DNL HubSpot]應用程式關聯的使用者端密碼。 |
| `auth.params.accessToken` | 最初驗證您的OAuth整合時獲得的存取權杖。 |
| `auth.params.refreshToken` | 重新整理權杖是在最初驗證您的OAuth整合時取得。 |
| `connectionSpec.id` | [!DNL HubSpot]連線規格識別碼： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL HubSpot]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將行銷自動化資料帶入Experience Platform](../../collect/marketing-automation.md)
