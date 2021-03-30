---
keywords: Experience Platform;home；熱門主題；Shopify;shopify；電子商務
solution: Experience Platform
title: 使用Flow Service API建立Shopify連接器來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用Flow Service API將Shopify連線至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API建立[!DNL Shopify]來源連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API來引導您完成將[!DNL Shopify]連接至[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Shopify]。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Shopify]連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Shopify]伺服器的端點。 |
| `accessToken` | 您[!DNL Shopify]使用者帳戶的存取Token。 |
| `connectionSpec` | 建立連線所需的唯一識別碼。 [!DNL Shopify]的連接規範ID為：`4f63aa36-bd48-4e33-bb83-49fbcd11c708` |

有關快速入門的詳細資訊，請參閱[Shopify authentication document](https://shopify.dev/concepts/about-apis/authentication)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Shopify]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立[!DNL Shopify]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Shopify]的連接規範ID為`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Shopify]伺服器的端點。 |
| `auth.params.accessToken` | 您[!DNL Shopify]使用者帳戶的存取Token。 |
| `connectionSpec.id` | [!DNL Shopify]連接規範ID:`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Shopify]連接，並獲取了該連接的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如何使用Flow Service API](../../explore/ecommerce.md)來探索電子商務連線。[