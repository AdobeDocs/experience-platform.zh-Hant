---
keywords: Experience Platform；首頁；熱門主題；Salesforce;salesforce
solution: Experience Platform
title: 使用流服務API建立Salesforce基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Salesforce帳戶。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# 建立 [!DNL Salesforce] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Salesforce] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL Platform] 到 [!DNL Salesforce] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL Salesforce]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Salesforce] 源實例。 |
| `username` | 用戶名 [!DNL Salesforce] 用戶帳戶。 |
| `password` | 的密碼 [!DNL Salesforce] 用戶帳戶。 |
| `securityToken` | 的安全令牌 [!DNL Salesforce] 用戶帳戶。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL AdWords] 為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

有關入門的詳細資訊，請訪問 [此Salesforce文檔](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Salesforce] 身份驗證憑據作為請求參數的一部分。


**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Salesforce]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.username` | 與您的 [!DNL Salesforce] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Salesforce] 帳戶。 |
| `auth.params.securityToken` | 與您的 [!DNL Salesforce] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Salesforce] 連接規範ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Salesforce] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/crm.md)
