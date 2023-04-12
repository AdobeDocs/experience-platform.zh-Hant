---
keywords: Experience Platform；首頁；熱門主題；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流服務API建立Azure事件集線器源連接
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Azure事件中心帳戶。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---


# 建立 [!DNL Azure Event Hubs] 源連接使用 [!DNL Flow Service] API

本教學課程會逐步引導您完成連線步驟 [!DNL Azure Event Hubs] (下稱「[!DNL Event Hubs]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL Event Hubs] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Event Hubs] 帳戶，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 的主鍵 [!DNL Event Hubs] 命名空間。 此 `sasPolicy` the `sasKey` 對應到必須有 `manage` 為 [!DNL Event Hubs] 清單。 |
| `namespace` | 的命名空間 [!DNL Event Hubs] 您正在存取。 安 [!DNL Event Hubs] 命名空間提供唯一的範圍界定容器，您可在其中建立一或多個 [!DNL Event Hubs]. |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 此 [!DNL Event Hubs] 連接規範ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

如需這些值的詳細資訊，請參閱 [此事件中心文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

建立源連接的第一步是驗證您的 [!DNL Event Hubs] 源和生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Event Hubs] 驗證憑證作為要求參數的一部分。

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
| `auth.params.namespace` | 的命名空間 [!DNL Event Hubs] 您正在存取。 |
| `connectionSpec.id` | 此 [!DNL Event Hubs] 連接規範ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此連接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接

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
| `baseConnectionId` | 您的 [!DNL Event Hubs] 在上一步驟中生成的源。 |
| `connectionSpec.id` | 的固定連接規範ID [!DNL Event Hubs]. 此ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 格式 [!DNL Event Hubs] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |
| `params.eventHubName` | 您的 [!DNL Event Hubs] 來源。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括： `raw` 和 `xdm`. |
| `params.reset` | 此參數會定義資料的讀取方式。 使用 `latest` 從最新資料開始讀取，並使用 `earliest` 從資料流中的第一個可用資料開始讀取。 此參數為選用，預設值為 `earliest` 若未提供。 |
| `params.consumerGroup` | 要用於的發佈或訂閱機制 [!DNL Event Hubs]. 此參數為選用，預設值為 `$Default` 若未提供。 請參閱 [[!DNL Event Hubs] 活動使用者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 以取得更多資訊。 |

## 後續步驟

依照本教學課程，您已建立 [!DNL Event Hubs] 源連接使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID [使用 [!DNL Flow Service] API](../../collect/streaming.md).
