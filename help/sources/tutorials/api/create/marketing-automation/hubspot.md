---
keywords: Experience Platform；首頁；熱門主題；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服務API建立HubSpot源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL HubSpot]源連接

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連線至[!DNL HubSpot]的步驟。

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
| `connectionSpec` | 建立連線所需的唯一識別碼。 [!DNL HubSpot]的連接規範ID為：`cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

有關入門的詳細資訊，請參閱此[HubSpot文檔](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的區段。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都會隔離至特定虛擬沙箱。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL HubSpot]帳戶只需一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```https
POST /connections
```

**要求**

若要建立[!DNL HubSpot]連線，必須在POST請求中提供其唯一連線規格ID。 [!DNL HubSpot]的連接規範ID為`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
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

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL HubSpot]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/marketing-automation.md)探索行銷自動化系統時，您可以在下一個教學課程中使用此連線ID。[
