---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: 使用流服務API建立Zoho CRM基本連線
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Zoho CRM。
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# 建立 [!DNL Zoho CRM] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Zoho CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Zoho CRM] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Zoho CRM]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| --- | --- |
| `endpoint` | 的端點 [!DNL Zoho CRM] 伺服器。 |
| `accountsUrl` | 帳戶URL可用來產生您的存取權和重新整理Token。 URL必須是網域專屬的。 |
| `clientId` | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| `clientSecret` | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| `accessToken` | 存取權杖可授權您對 [!DNL Zoho CRM] 帳戶。 |
| `refreshToken` | 重新整理Token是用來在您的存取Token過期後產生新存取Token的Token。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Zoho CRM] 為： `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

如需這些認證的詳細資訊，請參閱 [[!DNL Zoho CRM] 驗證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Zoho CRM] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

>[!TIP]
>
>您的帳戶URL網域必須與適當的網域位置對應。 以下是各種網域及其對應的帳戶URL:<ul><li>美國：https://accounts.zoho.com</li><li>澳大利亞：https://accounts.zoho.com.au</li><li>歐洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中國：https://accounts.zoho.com.cn</li></ul>

下列請求會為 [!DNL Zoho CRM]:

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
| `name` | 您的 [!DNL Zoho CRM] 基本連接。 您可以使用此名稱來查詢 [!DNL Zoho CRM] 基本連接。 |
| `description` | 您的 [!DNL Zoho CRM] 基本連接。 |
| `auth.specName` | 用於連接的驗證類型。 |
| `auth.params.endpoint` | 的端點 [!DNL Zoho CRM] 伺服器。 |
| `auth.params.accountsUrl` | 帳戶URL可用來產生您的存取權並重新整理Token。 URL必須是網域專屬的。 |
| `auth.params.clientId` | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| `auth.params.clientSecret` | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| `auth.params.accessToken` | 存取權杖可授權您對 [!DNL Zoho CRM] 帳戶。 |
| `auth.params.refreshToken` | 重新整理Token是用來在您的存取Token過期後產生新存取Token的Token。 |
| `connectionSpec.id` | 的連接規範ID [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Zoho] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/crm.md)
