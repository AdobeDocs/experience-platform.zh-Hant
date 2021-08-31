---
keywords: Experience Platform；首頁；熱門主題；Google PubSub;Google Pubsub
solution: Experience Platform
title: 使用流程服務API建立Google PubSub Source連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Google PubSub帳戶。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# 使用流服務API建立[!DNL Google PubSub]源連接

>[!NOTE]
>
>[!DNL Google PubSub]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將[!DNL Google PubSub]（以下稱為「[!DNL PubSub]」）連線至Experience Platform的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功將[!DNL PubSub]連線至Platform。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL PubSub]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證[!DNL PubSub]所需的項目ID。 |
| `credentials` | 驗證[!DNL PubSub]所需的憑據或密鑰。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基本和源目標連接相關的驗證規範。 [!DNL PubSub]連接規範ID為：`70116022-a743-464a-bbfe-e226a7f8210c`。 |

有關這些值的詳細資訊，請參閱此[[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication)文檔。 要使用基於服務帳戶的身份驗證，請參閱本[[!DNL PubSub] 建立服務帳戶的指南](https://cloud.google.com/docs/authentication/production#create_service_account)以了解如何生成憑據的步驟。

>[!TIP]
>
>如果您使用服務帳戶型驗證，請確定您已授予您服務帳戶的足夠使用者存取權，且複製和貼上憑證時，JSON中沒有額外的空格。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證[!DNL PubSub]源並生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL PubSub]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

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
| `auth.params.credentials` | 驗證[!DNL PubSub]所需的憑據或密鑰。 |
| `connectionSpec.id` | [!DNL PubSub]連接規範ID:`70116022-a743-464a-bbfe-e226a7f8210c`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此基本連接ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 來源連線例項是租用戶和IMS組織專屬的。

要建立源連接，請向[!DNL Flow Service] API的`/sourceConnections`端點發出POST請求。

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可提供的選用值，用於包含來源連線的詳細資訊。 |
| `baseConnectionId` | 在上一步中生成的[!DNL PubSub]源的基本連接ID。 |
| `connectionSpec.id` | [!DNL PubSub]的固定連接規範ID。 此ID為：`70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 您要擷取的[!DNL PubSub]資料格式。 目前，唯一支援的資料格式是`json`。 |
| `params.topicId` | 主題ID定義發佈者所傳送訊息的特定命名資源 |
| `params.subscriptionId` | 訂閱ID定義特定命名資源，該資源代表來自單一特定主題的訊息流，要傳送至訂閱應用程式。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括：`raw`和`xdm`。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL PubSub]來源連線。 您可以在[的下一個教程中使用此源連接ID，以使用 [!DNL Flow Service] API](../../collect/streaming.md)建立流資料流。
