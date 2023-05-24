---
keywords: Experience Platform；首頁；熱門主題；hubspot;hubspot
solution: Experience Platform
title: 使用流服務API建立HubSpot基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 建立 [!DNL HubSpot] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL HubSpot] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL HubSpot] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL HubSpot]，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `clientSecret` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `accessToken` | 初始驗證OAuth整合時獲取的訪問令牌。 |
| `refreshToken` | 初始驗證OAuth整合時獲取的刷新令牌。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL HubSpot] 為： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

有關入門的詳細資訊，請參閱此 [HubSpot文檔](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL HubSpot] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL HubSpot]:

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
| `auth.params.clientId` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `auth.params.clientSecret` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `auth.params.accessToken` | 初始驗證OAuth整合時獲取的訪問令牌。 |
| `auth.params.refreshToken` | 初始驗證OAuth整合時獲取的刷新令牌。 |
| `connectionSpec.id` | 的 [!DNL HubSpot] 連接規範ID: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL HubSpot] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
