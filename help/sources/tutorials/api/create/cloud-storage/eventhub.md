---
keywords: Experience Platform；首頁；熱門主題；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流服務API建立Azure事件集線器源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Azure事件中心帳戶。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 091f6751f4377a25844328ce924f3c33899b3344
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API建立[!DNL Azure Event Hubs]源連接

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)將[!DNL Azure Event Hubs]（以下稱為「[!DNL Event Hubs]」）連線至Experience Platform的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
- [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功將[!DNL Event Hubs]連線至Platform。

### 收集所需憑據

為了使[!DNL Flow Service]與[!DNL Event Hubs]帳戶連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 生成的共用訪問簽名。 |
| `namespace` | 您正在訪問的[!DNL Event Hubs]的命名空間。 [!DNL Event Hubs]命名空間提供唯一的範圍界定容器，您可在其中建立一或多個[!DNL Event Hubs]。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Event Hubs]連接規範ID為：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

有關這些值的詳細資訊，請參閱[此事件中心文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證[!DNL Event Hubs]源並生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Event Hubs]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

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
| `auth.params.sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `auth.params.sasKey` | 生成的共用訪問簽名。 |
| `auth.params.namespace` | 您正在訪問的[!DNL Event Hubs]的命名空間。 |
| `connectionSpec.id` | [!DNL Event Hubs]連接規範ID為：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此連接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接

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
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可提供的選用值，用於包含來源連線的詳細資訊。 |
| `baseConnectionId` | 在上一步中生成的[!DNL Event Hubs]源的連接ID。 |
| `connectionSpec.id` | [!DNL Event Hubs]的固定連接規範ID。 此ID為：`bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |
| `data.format` | 您要擷取的[!DNL Event Hubs]資料格式。 目前，唯一支援的資料格式是`json`。 |
| `params.eventHubName` | [!DNL Event Hubs]源的名稱。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括：`raw`和`xdm`。 |
| `params.reset` | 此參數會定義資料的讀取方式。 使用`latest`開始從最新資料中讀取，並使用`earliest`開始從流中第一個可用資料中讀取。 此參數為選用，若未提供，則預設為`earliest`。 |
| `params.consumerGroup` | 用於[!DNL Event Hubs]的發佈或訂閱機制。 此參數為選用，若未提供，則預設為`$Default`。 如需詳細資訊，請參閱本[[!DNL Event Hubs] 事件使用者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)。 |

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Event Hubs]來源連線。 您可以在[的下一個教程中使用此源連接ID，以使用 [!DNL Flow Service] API](../../collect/streaming.md)建立流資料流。
