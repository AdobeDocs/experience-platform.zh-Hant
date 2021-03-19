---
keywords: Experience Platform;home；熱門主題；Google PubSub;google pubsub
solution: Experience Platform
title: 使用Flow Service API建立Google PubSub來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至Google PubSub帳戶。
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---


# 使用流服務API建立[!DNL Google PubSub]源連接

>[!NOTE]
>
>[!DNL Google PubSub]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)來引導您完成將[!DNL Google PubSub]（以下稱為&quot;[!DNL PubSub]&quot;）連接至Adobe Experience Platform的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功建立[!DNL PubSub]來源連線。

### 收集必要的認證

要使[!DNL Flow Service]連接到[!DNL PubSub]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證[!DNL PubSub]所需的項目ID。 |
| `credentials` | 驗證[!DNL PubSub]所需的憑證或金鑰。 |

如需這些值的詳細資訊，請參閱下列[PubSub authentication](https://cloud.google.com/pubsub/docs/authentication)檔案。 如果您使用服務帳戶型驗證，請參閱以下[PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account)以取得如何產生認證的步驟。

>[!TIP]
>
>如果您使用以服務帳戶為基礎的驗證，請確定您已授與足夠的使用者存取權給您的服務帳戶，而且在複製和貼上認證時，JSON中沒有額外的空格。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL PubSub]帳戶只需要一個連接，因為它可用於建立多個資料流以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立[!DNL PubSub]連接，必須在POST請求中提供提供程式ID和連接規範ID。 提供程式ID為`521eee4d-8cbe-4906-bb48-fb6bd4450033`，連接規範ID為`70116022-a743-464a-bbfe-e226a7f8210c`。

**API格式**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.projectId` | 驗證[!DNL PubSub]所需的項目ID。 |
| `auth.params.credentials` | 驗證[!DNL PubSub]所需的憑證或金鑰。 |
| `connectionSpec.id` | [!DNL PubSub]連接規範ID:`70116022-a743-464a-bbfe-e226a7f8210c`。 |

**回應**

成功的響應返回新建立的[!DNL PubSub]連接的連接ID。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL PubSub]連接並獲取了其唯一連接ID。 您可以使用此連線ID來使用Flow Service API](../../collect/streaming.md)收集串流資料。[
