---
title: 使用流量服務API建立Google PubSub Source連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Google PubSub帳戶。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 2%

---

# 使用流量服務API建立[!DNL Google PubSub] Source連線

>[!IMPORTANT]
>
>[!DNL Google PubSub]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)，將[!DNL Google PubSub] （以下稱為&quot;[!DNL PubSub]&quot;）連線至Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功將[!DNL PubSub]連線至Experience Platform。

### 收集必要的認證

您必須提供下列連線屬性的值，才能將您的[!DNL PubSub]帳戶連線至[!DNL Flow Service]。 如需有關驗證和先決條件設定的詳細資訊，請閱讀[[!DNL PubSub source] 總覽](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites)。

>[!BEGINTABS]

>[!TAB 以專案為基礎的驗證]

| 認證 | 說明 |
| --- | --- |
| `projectId` | 驗證[!DNL PubSub]所需的專案識別碼。 |
| `credentials` | 驗證[!DNL PubSub]所需的認證。 您必須確保在移除認證的空格後，放入完整的JSON檔案。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器特性，包括與建立基礎和來源目標連線相關的驗證規格。 [!DNL PubSub]連線規格識別碼為： `70116022-a743-464a-bbfe-e226a7f8210c`。 |

>[!TAB 主題和訂閱式驗證]

| 認證 | 說明 |
| --- | --- |
| `credentials` | 驗證[!DNL PubSub]所需的認證。 您必須確保在移除認證的空格後，放入完整的JSON檔案。 |
| `topicName` | 代表訊息摘要的資源名稱。 如果要提供您[!DNL PubSub]來源中特定資料流的存取權，您必須指定主題名稱。 主題名稱格式為： `projects/{PROJECT_ID}/topics/{TOPIC_ID}`。 |
| `subscriptionName` | 您的[!DNL PubSub]訂閱名稱。 在[!DNL PubSub]中，訂閱可讓您訂閱訊息發佈至的主題，以接收訊息。 **注意**：單一[!DNL PubSub]訂閱只能用於一個資料流。 若要建立多個資料流，您必須有多個訂閱。 訂閱名稱格式為： `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器特性，包括與建立基礎和來源目標連線相關的驗證規格。 [!DNL PubSub]連線規格識別碼為： `70116022-a743-464a-bbfe-e226a7f8210c`。 |

>[!ENDTABS]

如需這些值的詳細資訊，請閱讀此[[!DNL PubSub] 驗證](https://cloud.google.com/pubsub/docs/authentication)檔案。 若要使用以服務帳戶為基礎的驗證，請閱讀此[[!DNL PubSub] 建立服務帳戶指南](https://cloud.google.com/docs/authentication/production#create_service_account)，以瞭解如何產生認證的步驟。

>[!TIP]
>
>如果您使用以服務帳戶為基礎的驗證，在複製和貼上認證時，請確保您已授予足夠的使用者存取權給您的服務帳戶，並且JSON中沒有額外的空格。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL Google PubSub]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

建立來源連線的第一個步驟是驗證您的[!DNL PubSub]來源並產生基本連線識別碼。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL PubSub]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

[!DNL PubSub]來源可讓您指定在驗證期間允許使用的存取型別。 您可以將帳戶設定為擁有根存取權，或限制特定[!DNL PubSub]主題和訂閱的存取權。

>[!NOTE]
>
>指派給[!DNL PubSub]專案的主體（角色）會繼承[!DNL PubSub]專案內建立的所有主題和訂閱。 如果您希望主參與者（角色）能夠存取特定主題，則也必須將該主參與者（角色）新增到主題的對應訂閱中。 如需詳細資訊，請閱讀有關存取控制](<https://cloud.google.com/pubsub/docs/access-control>)的[[!DNL PubSub] 檔案。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 以專案為基礎的驗證]

若要使用專案型驗證建立基底連線，請對`/connections`端點提出POST要求，並在要求內文中提供您的`projectId`和`credentials`。

+++要求

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
| `auth.params.projectId` | 驗證[!DNL PubSub]所需的專案識別碼。 |
| `auth.params.credentials` | 驗證[!DNL PubSub]所需的認證或金鑰。 |
| `connectionSpec.id` | [!DNL PubSub]連線規格識別碼： `70116022-a743-464a-bbfe-e226a7f8210c`。 |

++++

+++回應

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此基本連線ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB 主題和訂閱式驗證]

若要使用主題和訂閱式驗證建立基底連線，請對`/connections`端點發出POST要求，並在要求內文中提供您的`credentials`、`topicName`和`subscriptionName`。

+++要求

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
| `auth.params.credentials` | 驗證[!DNL PubSub]所需的認證或金鑰。 |
| `auth.params.topicName` | 您要提供存取權之[!DNL PubSub]來源的專案識別碼和主題識別碼配對。 |
| `auth.params.subscriptionName` | 您要提供存取權之[!DNL PubSub]來源的專案識別碼與訂閱識別碼配對。 |
| `connectionSpec.id` | [!DNL PubSub]連線規格識別碼： `70116022-a743-464a-bbfe-e226a7f8210c`。 |

+++

+++回應

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此基本連線ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## 建立來源連線 {#source}

來源連線會建立和管理與擷取資料的外部來源的連線。 來源連線包含資料來源、資料格式等資訊，以及建立資料流所需的來源連線ID。 租使用者和組織專屬的來源連線例項。

若要建立來源連線，請對[!DNL Flow Service] API的`/sourceConnections`端點提出POST要求。

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
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的詳細資訊。 |
| `baseConnectionId` | 在上一步中產生的[!DNL PubSub]來源的基本連線識別碼。 |
| `connectionSpec.id` | [!DNL PubSub]的固定連線規格識別碼。 此ID為： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 您要擷取的[!DNL PubSub]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.topicName` | [!DNL PubSub]主題的名稱。 在[!DNL PubSub]中，主題是代表訊息摘要的已命名資源。 |
| `params.subscriptionName` | 與指定主題對應的訂閱名稱。 在[!DNL PubSub]中，訂閱可讓您讀取主題中的訊息。 可以將一個或多個訂閱指派給單一主題。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw`和`xdm`。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在下一個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>在您建立或更新串流資料流後，需要短暫暫停資料擷取5分鐘，以防止任何可能的資料遺失或資料中斷情況。

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL PubSub]來源連線。 您可以在下一個教學課程中使用此來源連線ID來[使用 [!DNL Flow Service] API](../../collect/streaming.md)建立串流資料流。
