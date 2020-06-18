---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立HubSpot連接器
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# 使用Flow Service API建立HubSpot連接器

>[!NOTE]
>HubSpot連接器處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至HubSpot的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用Flow Service API成功連線至HubSpot。

### 收集必要的認證

為了讓流服務與HubSpot連接，您必須提供以下連接屬性：

| 憑證 | 說明 |
| ---------- | ----------- |
| 用戶端ID | 與您的HubSpot應用程式相關聯的用戶端ID。 |
| 用戶端密碼 | 與您的HubSpot應用程式相關聯的用戶端密碼。 |
| 存取Token | 首次驗證您的OAuth整合時取得的存取Token。 |
| 重新整理Token | 初次驗證您的OAuth整合時取得的重新整理Token。 |
| 連接規範ID | 建立連線所需的唯一識別碼。 HubSpot的連接規範ID為： `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

有關快速入門的詳細資訊，請參閱此 [HubSpot檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於流服務的資源）都會隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個HubSpot帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```https
POST /connections
```

**請求**

要建立HubSpot連接，必須在POST請求中提供其唯一連接規範ID。 HubSpot的連接規範ID為 `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。

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
| `auth.params.clientId` | 與您的HubSpot應用程式相關聯的用戶端ID。 |
| `auth.params.clientSecret` | 與您的HubSpot應用程式相關聯的用戶端密碼。 |
| `auth.params.accessToken` | 首次驗證您的OAuth整合時取得的存取Token。 |
| `auth.params.refreshToken` | 初次驗證您的OAuth整合時取得的重新整理Token。 |

**回應**

成功的回應會傳回新建立之API連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

在本教程中，您已使用Flow Service API建立HubSpot連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此連線ID，學習如何使 [用流程服務API來探索行銷自動化系統](../../explore/marketing-automation.md)。