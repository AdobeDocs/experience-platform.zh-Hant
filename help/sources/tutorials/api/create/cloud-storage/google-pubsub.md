---
title: 使用流程服務API建立Google PubSub Source連線
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Google PubSub帳戶。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f56cdc2dc67f2d4820d80d8e5bdec8306d852891
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# 建立 [!DNL Google PubSub] 使用流服務API的源連接

本教學課程會逐步引導您完成連線步驟 [!DNL Google PubSub] (下稱「[!DNL PubSub]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL PubSub] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL PubSub]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證所需的專案ID [!DNL PubSub]. |
| `credentials` | 驗證所需的憑據或密鑰 [!DNL PubSub]. |
| `topicId` | 的ID [!DNL PubSub] 代表訊息摘要的資源。 如果要提供對中特定資料流的存取權，必須指定主題ID [!DNL Google PubSub] 來源。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基本和源目標連接相關的驗證規範。 此 [!DNL PubSub] 連接規範ID為： `70116022-a743-464a-bbfe-e226a7f8210c`. |

如需這些值的詳細資訊，請參閱 [[!DNL PubSub] 驗證](https://cloud.google.com/pubsub/docs/authentication) 檔案。 若要使用服務帳戶型驗證，請參閱 [[!DNL PubSub] 建立服務帳戶指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以取得如何產生憑證的步驟。

>[!TIP]
>
>如果您使用服務帳戶型驗證，請確定您已授予您服務帳戶的足夠使用者存取權，且複製和貼上憑證時，JSON中沒有額外的空格。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

建立源連接的第一步是驗證您的 [!DNL PubSub] 源和生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL PubSub] 驗證憑證作為要求參數的一部分。

在此步驟中，您可以提供主題ID，以定義您的帳戶可存取的資料。 只能存取與該主題ID相關聯的訂閱。

>[!NOTE]
>
>指派給發佈子專案的承擔者（角色）會繼承在 [!DNL PubSub] 專案。 如果要添加主體（角色）以訪問特定主題，則該主體（角色）也必須添加到主題的相應訂閱中。 如需詳細資訊，請閱讀 [[!DNL PubSub] 存取控制檔案](https://cloud.google.com/pubsub/docs/access-control).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Google PubSub authentication credentials",
          "params": {
              "projectId": "acme-project",
              "credentials": "{CREDENTIALS}",
              "topicID": "acmeProjectAPI"
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
| `auth.params.projectId` | 驗證所需的專案ID [!DNL PubSub]. |
| `auth.params.credentials` | 驗證所需的憑據或密鑰 [!DNL PubSub]. |
| `auth.params.topicID` | 您的 [!DNL PubSub] 要提供訪問權限的源。 |
| `connectionSpec.id` | 此 [!DNL PubSub] 連接規格ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此基本連接ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 源連接實例是租戶和組織特有的。

若要建立來源連線，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。

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
          "topicId": "acme-project",
          "subscriptionId": "{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可提供的選用值，用於包含來源連線的詳細資訊。 |
| `baseConnectionId` | 您的 [!DNL PubSub] 在上一步驟中生成的源。 |
| `connectionSpec.id` | 的固定連接規範ID [!DNL PubSub]. 此ID為： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 格式 [!DNL PubSub] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |
| `params.topicId` | 您的 [!DNL PubSub] 主題。 在 [!DNL PubSub]，主題是代表訊息摘要的已命名資源。 |
| `params.subscriptionId` | 與指定主題對應的訂閱ID。 在 [!DNL PubSub]，訂閱可讓您讀取主題中的訊息。 可為單一主題指派一或多個訂閱。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括： `raw` 和 `xdm`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL PubSub] 源連接使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID [使用 [!DNL Flow Service] API](../../collect/streaming.md).
