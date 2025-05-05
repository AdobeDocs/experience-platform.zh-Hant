---
title: 使用流程服務API建立Azure事件中樞Source連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Azure事件中樞帳戶。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Event Hubs]來源連線

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將[!DNL Azure Event Hubs] （以下稱為&quot;[!DNL Event Hubs]&quot;）連線至Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
- [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功將[!DNL Event Hubs]連線至Experience Platform。

### 收集必要的認證

為了讓[!DNL Flow Service]與您的[!DNL Event Hubs]帳戶連線，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 標準驗證]

| 認證 | 說明 |
| --- | --- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `sasKey` | [!DNL Event Hubs]名稱空間的主索引鍵。 `sasKey`對應的`sasPolicy`必須已設定`manage`許可權，才能填入[!DNL Event Hubs]清單。 |
| `namespace` | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

>[!TAB SAS驗證]

| 認證 | 說明 |
| --- | --- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `sasKey` | [!DNL Event Hubs]名稱空間的主索引鍵。 `sasKey`對應的`sasPolicy`必須已設定`manage`許可權，才能填入[!DNL Event Hubs]清單。 |
| `namespace` | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |
| `eventHubName` | 填寫您的[!DNL Azure Event Hub]名稱。 閱讀[Microsoft檔案](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)以瞭解[!DNL Event Hub]名稱的詳細資訊。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

如需有關[!DNL Event Hubs]的共用存取簽章(SAS)驗證的詳細資訊，請閱讀使用SAS[&#128279;](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)的[!DNL Azure] 指南。

>[!TAB 事件中心Azure Active Directory驗證]

| 認證 | 說明 |
| --- | --- |
| `tenantId` | 您要向其請求許可權的租使用者ID。 您可以將您的租使用者ID格式化為GUID或友好名稱。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| `clientId` | 指派給應用程式的應用程式ID。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取此ID。 |
| `clientSecretValue` | 使用者端密碼與使用者端ID搭配使用，用來驗證您的應用程式。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取您的使用者端密碼。 |
| `namespace` | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |

如需[!DNL Azure Active Directory]的詳細資訊，請閱讀[使用Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)的Azure指南。

>[!TAB 事件中樞範圍的Azure Active Directory驗證]

| 認證 | 說明 |
| --- | --- |
| `tenantId` | 您要向其請求許可權的租使用者ID。 您可以將您的租使用者ID格式化為GUID或友好名稱。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| `clientId` | 指派給應用程式的應用程式ID。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取此ID。 |
| `clientSecretValue` | 使用者端密碼與使用者端ID搭配使用，用來驗證您的應用程式。 您可以從您註冊[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]入口網站擷取您的使用者端密碼。 |
| `namespace` | 您正在存取的[!DNL Event Hub]的名稱空間。 [!DNL Event Hub]名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個[!DNL Event Hubs]。 |
| `eventHubName` | 填寫您的[!DNL Azure Event Hub]名稱。 閱讀[Microsoft檔案](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)以瞭解[!DNL Event Hub]名稱的詳細資訊。 |

>[!ENDTABS]

如需這些值的詳細資訊，請參閱[此「事件中樞」檔案](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL Event Hubs]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

建立來源連線的第一個步驟是驗證您的[!DNL Event Hubs]來源並產生基本連線識別碼。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Event Hubs]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 標準驗證]

若要使用標準驗證建立帳戶，請在提供您`sasKeyName`、`sasKey`和`namespace`的值時對`/connections`端點提出POST要求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `auth.params.sasKey` | 產生的共用存取權簽章。 |
| `auth.params.namespace` | 您正在存取的[!DNL Event Hubs]的名稱空間。 |
| `connectionSpec.id` | [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此連線ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS驗證]

若要使用SAS驗證建立帳戶，請在提供您`sasKeyName`、`sasKey`、`namespace`和`eventHubName`的值時對`/connections`端點提出POST要求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `auth.params.sasKey` | 產生的共用存取權簽章。 |
| `auth.params.namespace` | 您正在存取的[!DNL Event Hubs]的名稱空間。 |
| `params.eventHubName` | 您的[!DNL Event Hubs]來源的名稱。 |
| `connectionSpec.id` | [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此連線ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 事件中心Azure Active Directory驗證]

若要使用Azure Active Directory驗證建立帳戶，請在提供您的`tenantId`、`clientId`、`clientSecretValue`和`namespace`的值時，對`/connections`端點提出POST要求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.tenantId` | 您應用程式的租使用者ID。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| `auth.params.clientId` | 您組織的使用者端ID。 |
| `auth.params.clientSecretValue` | 您組織的使用者端密碼值。 |
| `auth.params.namespace` | 您正在存取的[!DNL Event Hubs]的名稱空間。 |
| `connectionSpec.id` | [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此連線ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 事件中樞範圍的Azure Active Directory驗證]

若要使用Azure Active Directory驗證建立帳戶，請在提供您的`tenantId`、`clientId`、`clientSecretValue`、`namespace`和`eventHubName`的值時，對`/connections`端點提出POST要求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.tenantId` | 您應用程式的租使用者ID。 **注意**：租使用者ID在[!DNL Microsoft Azure]介面中稱為「目錄ID」。 |
| `auth.params.clientId` | 您組織的使用者端ID。 |
| `auth.params.clientSecretValue` | 您組織的使用者端密碼值。 |
| `auth.params.namespace` | 您正在存取的[!DNL Event Hubs]的名稱空間。 |
| `auth.params.eventHubName` | 您的[!DNL Event Hubs]來源的名稱。 |
| `connectionSpec.id` | [!DNL Event Hubs]連線規格識別碼為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此連線ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## 建立來源連線

>[!TIP]
>
>[!DNL Event Hubs]使用者群組只能在指定時間用於單一流量。

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
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的詳細資訊。 |
| `baseConnectionId` | 您在上一步中產生的[!DNL Event Hubs]來源的連線ID。 |
| `connectionSpec.id` | [!DNL Event Hubs]的固定連線規格識別碼。 此ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |
| `data.format` | 您要擷取的[!DNL Event Hubs]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.eventHubName` | 您的[!DNL Event Hubs]來源的名稱。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw`和`xdm`。 |
| `params.reset` | 此引數會定義資料的讀取方式。 使用`latest`開始讀取最近的資料，並使用`earliest`開始讀取資料流中第一個可用的資料。 此引數為選用引數，若未提供，則預設為`earliest`。 |
| `params.consumerGroup` | 要用於[!DNL Event Hubs]的發佈或訂閱機制。 此引數為選用引數，若未提供，則預設為`$Default`。 如需詳細資訊，請參閱此[[!DNL Event Hubs] 活動消費者](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)指南。 **注意**： [!DNL Event Hubs]消費者群組只能在指定時間用於單一流量。 |

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Event Hubs]來源連線。 您可以在下一個教學課程中使用此來源連線ID來[使用 [!DNL Flow Service] API](../../collect/streaming.md)建立串流資料流。
