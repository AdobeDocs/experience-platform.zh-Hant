---
title: 使用流服務API建立GooglePubSub源連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到GooglePubSub帳戶。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 371947cff518c16816692210054680367fd6504c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# 建立 [!DNL Google PubSub] 使用流服務API的源連接

本教程將指導您完成連接的步驟 [!DNL Google PubSub] (以下簡稱：[!DNL PubSub]&quot;)到Experience Platform，使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL PubSub] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL PubSub]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證所需的項目ID [!DNL PubSub]。 |
| `credentials` | 驗證所需的憑據或密鑰 [!DNL PubSub]。 |
| `topicName` | 表示消息源的資源名稱。 如果要提供對中特定資料流的訪問權限，則必須指定主題名 [!DNL PubSub] 源。 主題名稱格式為： `projects/{PROJECT_ID}/topics/{TOPIC_ID}`。 |
| `subscriptionName` | 您的名稱 [!DNL PubSub] 訂閱。 在 [!DNL PubSub]，訂閱允許您通過訂閱已發佈消息的主題來接收消息。 **注釋**:單 [!DNL PubSub] 訂閱只能用於一個資料流。 要建立多個資料流，必須有多個預訂。 訂閱名稱格式為： `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基本和源目標連接相關的驗證規範。 的 [!DNL PubSub] 連接規範ID為： `70116022-a743-464a-bbfe-e226a7f8210c`。 |

有關這些值的詳細資訊，請參閱 [[!DNL PubSub] 認證](https://cloud.google.com/pubsub/docs/authentication) 的子菜單。 要使用基於服務帳戶的身份驗證，請參閱 [[!DNL PubSub] 建立服務帳戶指南](https://cloud.google.com/docs/authentication/production#create_service_account) 有關如何生成憑據的步驟。

>[!TIP]
>
>如果您使用基於服務帳戶的身份驗證，請確保在複製和貼上憑據時，已授予用戶對服務帳戶的足夠訪問權限，並且JSON中沒有額外的空白。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證 [!DNL PubSub] 源並生成基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL PubSub] 身份驗證憑據作為請求參數的一部分。

的 [!DNL PubSub] 源允許您指定在驗證期間允許的訪問類型。 您可以將帳戶設定為具有根訪問權限或限制對特定帳戶的訪問權限 [!DNL PubSub] 主題和訂閱。

>[!NOTE]
>
>分配給的承擔者（角色） [!DNL PubSub] 項目在建立於 [!DNL PubSub] 項目。 如果希望承擔者（角色）有權訪問特定主題，則還必須將該承擔者（角色）添加到主題的相應訂閱中。 有關詳細資訊，請閱讀 [[!DNL PubSub] 訪問控制文檔](<https://cloud.google.com/pubsub/docs/access-control>)。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 基於項目的身份驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `auth.params.projectId` | 驗證所需的項目ID [!DNL PubSub]。 |
| `auth.params.credentials` | 驗證所需的憑據或密鑰 [!DNL PubSub]。 |
| `connectionSpec.id` | 的 [!DNL PubSub] 連接規範ID: `70116022-a743-464a-bbfe-e226a7f8210c`。 |

>[!TAB 基於主題和訂閱的身份驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | 驗證所需的憑據或密鑰 [!DNL PubSub]。 |
| `auth.params.topicName` | 項目ID和主題ID對 [!DNL PubSub] 要提供訪問權限的源。 |
| `auth.params.subscriptionName` | 項目ID和訂閱ID對 [!DNL PubSub] 要提供訪問權限的源。 |
| `connectionSpec.id` | 的 [!DNL PubSub] 連接規範ID: `70116022-a743-464a-bbfe-e226a7f8210c`。 |

>[!ENDTABS]

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此基本連接ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

源連接建立並管理與外部源的連接，該連接來自接收資料的位置。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 源連接實例特定於租戶和組織。

要建立源連接，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以提供的可選值，以包含有關源連接的詳細資訊。 |
| `baseConnectionId` | 您的基本連接ID [!DNL PubSub] 在上一步中生成的源。 |
| `connectionSpec.id` | 固定連接規範ID [!DNL PubSub]。 此ID為： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 格式 [!DNL PubSub] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.topicName` | 您的名稱 [!DNL PubSub] 主題。 在 [!DNL PubSub]，主題是表示消息源的命名資源。 |
| `params.subscriptionName` | 與給定主題對應的訂閱名稱。 在 [!DNL PubSub]，訂閱允許您從主題中讀取消息。 可以將一個或多個訂閱分配給單個主題。 |
| `params.dataType` | 此參數定義正在攝取的資料的類型。 支援的資料類型包括： `raw` 和 `xdm`。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在下一教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL PubSub] 源連接使用 [!DNL Flow Service] API。 您可以在下一教程中使用此源連接ID [使用 [!DNL Flow Service] API](../../collect/streaming.md)。
