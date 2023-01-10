---
keywords: Experience Platform；首頁；熱門主題；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服務API建立HubSpot基礎連接
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 建立 [!DNL HubSpot] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL HubSpot] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL HubSpot] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL HubSpot]，您必須提供下列連線屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的 [!DNL HubSpot] 應用程式。 |
| `clientSecret` | 與您的 [!DNL HubSpot] 應用程式。 |
| `accessToken` | 初次驗證OAuth整合時取得的存取權杖。 |
| `refreshToken` | 初次驗證OAuth整合時取得的重新整理代號。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL HubSpot] 為： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

如需快速入門的詳細資訊，請參閱 [HubSpot文檔](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL HubSpot] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL HubSpot]:

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
| `auth.params.clientId` | 與您的 [!DNL HubSpot] 應用程式。 |
| `auth.params.clientSecret` | 與您的 [!DNL HubSpot] 應用程式。 |
| `auth.params.accessToken` | 初次驗證OAuth整合時取得的存取權杖。 |
| `auth.params.refreshToken` | 初次驗證OAuth整合時取得的重新整理代號。 |
| `connectionSpec.id` | 此 [!DNL HubSpot] 連接規範ID: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**回應**

成功的回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL HubSpot] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
