---
keywords: Experience Platform；首頁；熱門主題；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服務API建立HubSpot基礎連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL HubSpot]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL HubSpot]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL HubSpot]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL HubSpot]連接，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端密碼。 |
| `accessToken` | 初次驗證OAuth整合時取得的存取權杖。 |
| `refreshToken` | 初次驗證OAuth整合時取得的重新整理代號。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL HubSpot]的連接規範ID為：`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

有關入門的詳細資訊，請參閱此[HubSpot文檔](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL HubSpot]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL HubSpot]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.clientId` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端密碼。 |
| `auth.params.accessToken` | 初次驗證OAuth整合時取得的存取權杖。 |
| `auth.params.refreshToken` | 初次驗證OAuth整合時取得的重新整理代號。 |
| `connectionSpec.id` | [!DNL HubSpot]連接規範ID:`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL HubSpot]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/marketing-automation.md)探索行銷自動化系統時，您可以在下一個教學課程中使用此連線ID。[
