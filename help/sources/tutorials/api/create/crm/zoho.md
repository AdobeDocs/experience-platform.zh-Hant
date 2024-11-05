---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM；zoho crm；Zoho；zoho
solution: Experience Platform
title: 使用流量服務API建立Zoho CRM基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Zoho CRM。
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立[!DNL Zoho CRM]基本連線

>[!IMPORTANT]
>
>[!DNL Zoho CRM]來源將於2025年5月底淘汰。 作為替代方法，您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)來源。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Zoho CRM]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Zoho CRM]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Zoho CRM]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| `endpoint` | 您向其提出請求的[!DNL Zoho CRM]伺服器端點。 |
| `accountsUrl` | 帳戶URL會用於產生存取和重新整理Token。 URL必須是網域專屬的。 |
| `clientId` | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端識別碼。 |
| `clientSecret` | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端密碼。 |
| `accessToken` | 存取Token授權您對您的[!DNL Zoho CRM]帳戶的安全與暫時存取。 |
| `refreshToken` | 重新整理權杖是在您的存取權杖過期後，用來產生新存取權杖的權杖。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Zoho CRM]的連線規格識別碼為： `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

如需這些認證的詳細資訊，請參閱有關[[!DNL Zoho CRM] 驗證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)的檔案。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Zoho CRM]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

>[!TIP]
>
>您的帳戶URL網域必須符合您適當的網域位置。 以下是各種網域及其對應的帳戶URL：<ul><li>美國： https://accounts.zoho.com</li><li>澳洲： https://accounts.zoho.com.au</li><li>歐洲： https://accounts.zoho.eu</li><li>印度： https://accounts.zoho.in</li><li>中國： https://accounts.zoho.com.cn</li></ul>

下列要求會建立[!DNL Zoho CRM]的基礎連線：

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
| `name` | [!DNL Zoho CRM]基本連線的名稱。 您可以使用此名稱來查閱您的[!DNL Zoho CRM]基礎連線。 |
| `description` | 您的[!DNL Zoho CRM]基礎連線的選擇性描述。 |
| `auth.specName` | 用於連線的驗證型別。 |
| `auth.params.endpoint` | 您向其提出請求的[!DNL Zoho CRM]伺服器端點。 |
| `auth.params.accountsUrl` | 帳戶URL會用於產生您的存取和重新整理Token。 URL必須是網域專屬的。 |
| `auth.params.clientId` | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端識別碼。 |
| `auth.params.clientSecret` | 與您的[!DNL Zoho CRM]使用者帳戶對應的使用者端密碼。 |
| `auth.params.accessToken` | 存取Token授權您對您的[!DNL Zoho CRM]帳戶的安全與暫時存取。 |
| `auth.params.refreshToken` | 重新整理權杖是在您的存取權杖過期後，用來產生新存取權杖的權杖。 |
| `connectionSpec.id` | [!DNL Zoho CRM]的連線規格識別碼： `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Zoho]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將CRM資料帶入Platform](../../collect/crm.md)
