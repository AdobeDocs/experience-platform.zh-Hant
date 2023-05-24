---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM;Zoho crm;Zoho;zoho
solution: Experience Platform
title: 使用流服務API建立Zoho CRM基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Zoho CRM。
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 建立 [!DNL Zoho CRM] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Zoho CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接到所需的其他資訊 [!DNL Zoho CRM] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Zoho CRM]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| --- | --- |
| `endpoint` | 的端點 [!DNL Zoho CRM] 伺服器。 |
| `accountsUrl` | 帳戶URL用於生成訪問和刷新令牌。 該URL必須是特定於域的。 |
| `clientId` | 與您的 [!DNL Zoho CRM] 用戶帳戶。 |
| `clientSecret` | 與您的 [!DNL Zoho CRM] 用戶帳戶。 |
| `accessToken` | 訪問令牌授權您對您的 [!DNL Zoho CRM] 帳戶。 |
| `refreshToken` | 刷新令牌是用於在訪問令牌過期後生成新訪問令牌的令牌。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Zoho CRM] 為： `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

有關這些憑據的詳細資訊，請參閱 [[!DNL Zoho CRM] 認證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Zoho CRM] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

>[!TIP]
>
>您的帳戶URL域必須與相應的域位置對應。 以下是各種域及其相應帳戶URL:<ul><li>美國：https://accounts.zoho.com</li><li>澳大利亞：https://accounts.zoho.com.au</li><li>歐洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中國：https://accounts.zoho.com.cn</li></ul>

以下請求為 [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | 您的名稱 [!DNL Zoho CRM] 基本連接。 您可以使用此名稱查找 [!DNL Zoho CRM] 基本連接。 |
| `description` | 您的可選說明 [!DNL Zoho CRM] 基本連接。 |
| `auth.specName` | 用於連接的驗證類型。 |
| `auth.params.endpoint` | 的端點 [!DNL Zoho CRM] 伺服器。 |
| `auth.params.accountsUrl` | 帳戶URL用於生成訪問和刷新令牌。 該URL必須是特定於域的。 |
| `auth.params.clientId` | 與您的 [!DNL Zoho CRM] 用戶帳戶。 |
| `auth.params.clientSecret` | 與您的 [!DNL Zoho CRM] 用戶帳戶。 |
| `auth.params.accessToken` | 訪問令牌授權您對您的 [!DNL Zoho CRM] 帳戶。 |
| `auth.params.refreshToken` | 刷新令牌是用於在訪問令牌過期後生成新訪問令牌的令牌。 |
| `connectionSpec.id` | 連接規範ID [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Zoho] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/crm.md)
