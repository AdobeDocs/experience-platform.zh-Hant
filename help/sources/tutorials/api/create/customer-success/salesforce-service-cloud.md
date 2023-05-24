---
keywords: Experience Platform；首頁；熱門主題；Salesforce服務雲；salesforce服務雲
solution: Experience Platform
title: 使用流服務API建立Salesforce服務雲源連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Salesforce服務雲。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Service Cloud] 源連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Salesforce Service Cloud]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `username` | 您的用戶名 [!DNL Salesforce Service Cloud] 用戶帳戶。 |
| `password` | 您的密碼 [!DNL Salesforce Service Cloud] 帳戶。 |
| `securityToken` | 您的安全令牌 [!DNL Salesforce Service Cloud] 帳戶。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Salesforce Service Cloud] 為： `b66ab34-8619-49cb-96d1-39b37ede86ea`。 |

有關入門的詳細資訊，請參閱 [此Salesforce服務雲文檔](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Salesforce Service Cloud] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.username` | 與您的 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.securityToken` | 與您的 [!DNL Salesforce Service Cloud] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Salesforce Service Cloud] 連接規範ID: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Salesforce Service Cloud] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/customer-success.md)
