---
keywords: Experience Platform；首頁；熱門主題；salesforce marketing cloud;SalesforceMarketing Cloud
solution: Experience Platform
title: 使用流服務API建立SalesforceMarketing Cloud基礎連接
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至SalesforceMarketing Cloud。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Marketing Cloud] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Salesforce Marketing Cloud] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Salesforce Marketing Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可分割單一 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

以下章節提供您成功連線至所需了解的其他資訊 [!DNL Salesforce Marketing Cloud] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Salesforce Marketing Cloud]，您必須提供下列連線屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：** 輸入 `host` 值時，您只需指定子網域，而非整個URL。 例如，若您的主機URL為 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則您只需輸入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作為您的主機值。 |
| `clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Salesforce Marketing Cloud] 為： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

如需快速入門的詳細資訊，請參閱 [[!DNL Salesforce Marketing Cloud] 檔案](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Salesforce Marketing Cloud] 請求內文的驗證憑證。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `auth.params.clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Marketing Cloud] 連接規範ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**回應**

成功的回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Salesforce Marketing Cloud] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
