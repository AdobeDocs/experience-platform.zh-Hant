---
keywords: Experience Platform；首頁；熱門主題；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流服務API建立Azure事件中心源連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Azure事件中心帳戶。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---


# 建立 [!DNL Azure Event Hubs] 源連接使用 [!DNL Flow Service] API

本教程將指導您完成連接的步驟 [!DNL Azure Event Hubs] (以下簡稱：[!DNL Event Hubs]&quot;)到Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
- [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL Event Hubs] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Event Hubs] 帳戶，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 主鍵 [!DNL Event Hubs] 命名空間。 的 `sasPolicy` 那個 `sasKey` 必須對應 `manage` 為 [!DNL Event Hubs] 清單。 |
| `namespace` | 命名空間 [!DNL Event Hubs] 您正在訪問。 安 [!DNL Event Hubs] 命名空間提供了唯一的作用域容器，您可以在該容器中建立一個或多個 [!DNL Event Hubs]。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的 [!DNL Event Hubs] 連接規範ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

有關這些值的詳細資訊，請參閱 [此事件中心文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證 [!DNL Event Hubs] 源並生成基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Event Hubs] 身份驗證憑據作為請求參數的一部分。

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
| `auth.params.namespace` | 命名空間 [!DNL Event Hubs] 您正在訪問。 |
| `connectionSpec.id` | 的 [!DNL Event Hubs] 連接規範ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 下一步建立源連接時需要此連接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以提供的可選值，以包含有關源連接的詳細資訊。 |
| `baseConnectionId` | 您的連接ID [!DNL Event Hubs] 在上一步中生成的源。 |
| `connectionSpec.id` | 固定連接規範ID [!DNL Event Hubs]。 此ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |
| `data.format` | 格式 [!DNL Event Hubs] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.eventHubName` | 您的名稱 [!DNL Event Hubs] 源。 |
| `params.dataType` | 此參數定義正在攝取的資料的類型。 支援的資料類型包括： `raw` 和 `xdm`。 |
| `params.reset` | 此參數定義資料的讀取方式。 使用 `latest` 開始讀取最新資料，並使用 `earliest` 開始從流中的第一個可用資料讀取。 此參數是可選的，預設為 `earliest` 的下界。 |
| `params.consumerGroup` | 要用於的發佈或訂閱機制 [!DNL Event Hubs]。 此參數是可選的，預設為 `$Default` 的下界。 請參閱此 [[!DNL Event Hubs] 活動消費者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 的子菜單。 |

## 後續步驟

按照本教程，您建立了 [!DNL Event Hubs] 源連接使用 [!DNL Flow Service] API。 您可以在下一教程中使用此源連接ID [使用 [!DNL Flow Service] API](../../collect/streaming.md)。
