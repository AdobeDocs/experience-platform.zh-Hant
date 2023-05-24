---
keywords: Experience Platform；首頁；熱門主題；API教程；流目標API;平台
solution: Experience Platform
title: 使用Adobe Experience Platform的流服務API連接到流目標並激活資料
description: 本文檔介紹使用Adobe Experience PlatformAPI建立流目標
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 1%

---

# 使用流服務API連接到流目標並激活資料

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。
>
>閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

本教程演示如何使用API調用連接到您的Adobe Experience Platform資料，建立到流雲儲存目標([AmazonKinesis](../catalog/cloud-storage/amazon-kinesis.md) 或 [Azure事件中心](../catalog/cloud-storage/azure-event-hubs.md))，將資料流建立到新建立的目標，並將資料激活到新建立的目標。

本教程使用 [!DNL Amazon Kinesis] 所有示例中的目標，但步驟相同 [!DNL Azure Event Hubs]。

![概述 — 建立流目標和激活段的步驟](../assets/api/streaming-destination/overview.png)

如果您希望使用平台中的用戶介面連接到目標並激活資料，請參閱 [連接目標](../ui/connect-destination.md) 和 [將受眾資料激活到流段導出目標](../ui/activate-segment-streaming-destinations.md) 教程。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是記錄Experience Platform中資料位置和沿襲的系統。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便將資料激活到平台中的流目的地。

### 收集所需憑據

要完成本教程中的步驟，您應準備好以下憑據，具體取決於要連接和激活段的目標類型。

* 對於 [!DNL Amazon Kinesis] 連接： `accessKeyId`。 `secretKey`。 `region` 或 `connectionUrl`
* 對於 [!DNL Azure Event Hubs] 連接： `sasKeyName`。 `sasKey`。 `namespace`

### 讀取示例API調用 {#reading-sample-api-calls}

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

### 收集所需和可選標頭的值 {#gather-values}

要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可以隔離到特定的虛擬沙箱。 在對平台API的請求中，可以指定操作將在其中進行的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關Experience Platform中沙箱的詳細資訊，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

### Swagger文檔 {#swagger-docs}

您可以在Swagger中找到本教程中所有API調用的附帶參考文檔。 查看 [流服務API文檔，關於Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/)。 我們建議您並行使用本教程和Swagger文檔頁。

## 獲取可用流目標的清單 {#get-the-list-of-available-streaming-destinations}

![目標步驟概述步驟1](../assets/api/streaming-destination/step1.png)

作為第一步，您應確定要激活資料的流目標。 首先，執行呼叫以請求可連接和激活段到的可用目標的清單。 對執行以下GET請求 `connectionSpecs` 要返回可用目標清單的終結點：

**API格式**

```http
GET /connectionSpecs
```

**要求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**回應**

成功的響應包含可用目標及其唯一標識符的清單(`id`)。 儲存您計畫使用的目標值，因為在後續步驟中需要它。 例如，如果要將段連接和傳送到 [!DNL Amazon Kinesis] 或 [!DNL Azure Event Hubs]，在響應中查找以下代碼段：

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## 連接到Experience Platform資料 {#connect-to-your-experience-platform-data}

![目標步驟概述步驟2](../assets/api/streaming-destination/step2.png)

接下來，必須連接到Experience Platform資料，以便導出配置檔案資料並在首選目標中將其激活。 這包括以下兩個子步驟。

1. 首先，您必須通過設定基本連接來執行呼叫，以授權對Experience Platform中的資料的訪問。
2. 然後，使用基本連接ID，您將進行另一次調用，在其中建立源連接，該連接將建立到Experience Platform資料的連接。


### 授權訪問Experience Platform中的資料

**API格式**

```http
POST /connections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`:使用配置檔案服務的連接規範ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應包含基連接的唯一標識符(`id`)。 在建立源連接的下一步中根據需要儲存此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 連接到Experience Platform資料 {#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`:使用在上一步中獲得的Id。
* `{CONNECTION_SPEC_ID}`:使用配置檔案服務的連接規範ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應返回唯一標識符(`id`)。 這確認您已成功連接到Experience Platform資料。 在後續步驟中根據需要儲存此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 連接到流目標 {#connect-to-streaming-destination}

![目標步驟概述步驟3](../assets/api/streaming-destination/step3.png)

在此步驟中，您將設定到所需流目標的連接。 這包括以下兩個子步驟。

1. 首先，必須通過設定基本連接來執行呼叫以授權對流目標的訪問。
2. 然後，使用基本連接ID，您將進行另一次呼叫，在該呼叫中建立目標連接，該目標連接指定儲存帳戶中要傳送導出資料的位置以及要導出的資料的格式。

### 授權對流目標的訪問

**API格式**

```http
POST /connections
```

**要求**

>[!IMPORTANT]
>
>下面的示例包括帶前置詞的代碼注釋 `//`。 這些注釋突出顯示不同流目標必須使用不同值的位置。 請在使用代碼段之前刪除注釋。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`:使用在步驟中獲得的連接規範ID [獲取可用目標清單](#get-the-list-of-available-destinations)。
* `{AUTHENTICATION_CREDENTIALS}`:填寫流目標的名稱： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`。
* `{ACCESS_ID}`: *對於 [!DNL Amazon Kinesis] 連接。* 您的AmazonKinesis儲存位置的訪問ID。
* `{SECRET_KEY}`: *對於 [!DNL Amazon Kinesis] 連接。* 你AmazonKinesis倉庫的秘鑰。
* `{REGION}`: *對於 [!DNL Amazon Kinesis] 連接。* 您所在的區域 [!DNL Amazon Kinesis] 帳戶平台將在何處傳輸您的資料。
* `{SAS_KEY_NAME}`: *對於 [!DNL Azure Event Hubs] 連接。* 填寫SAS密鑰名稱。 瞭解身份驗證 [!DNL Azure Event Hubs] 在 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{SAS_KEY}`: *對於 [!DNL Azure Event Hubs] 連接。* 填入SAS密鑰。 瞭解身份驗證 [!DNL Azure Event Hubs] 在 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{EVENT_HUB_NAMESPACE}`: *對於 [!DNL Azure Event Hubs] 連接。* 填寫 [!DNL Azure Event Hubs] 平台將流資料的命名空間。 有關詳細資訊，請參見 [建立事件中心命名空間](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) 的 [!DNL Microsoft] 文檔。

**回應**

成功的響應包含基連接的唯一標識符(`id`)。 根據建立目標連接所需儲存此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 指定儲存位置和資料格式

**API格式**

```http
POST /targetConnections
```

**要求**

>[!IMPORTANT]
>
>下面的示例包括帶前置詞的代碼注釋 `//`。 這些注釋突出顯示不同流目標必須使用不同值的位置。 請在使用代碼段之前刪除注釋。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上面的步驟中獲得的基本連接ID。
* `{CONNECTION_SPEC_ID}`:使用步驟中獲得的連接規範 [獲取可用目標清單](#get-the-list-of-available-destinations)。
* `{NAME_OF_DATA_STREAM}`: *對於 [!DNL Amazon Kinesis] 連接。* 在中提供現有資料流的名稱 [!DNL Amazon Kinesis] 帳戶。 平台會將資料導出到此流。
* `{REGION}`: *對於 [!DNL Amazon Kinesis] 連接。* 您的AmazonKinesis帳戶中平台將傳輸您的資料的區域。
* `{EVENT_HUB_NAME}`: *對於 [!DNL Azure Event Hubs] 連接。* 填寫 [!DNL Azure Event Hub] 命名平台將在何處傳輸資料。 有關詳細資訊，請參見 [建立事件中心](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) 的 [!DNL Microsoft] 文檔。

**回應**

成功的響應返回唯一標識符(`id`)。 根據後續步驟中的要求儲存此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 建立資料流

![目標步驟概述步驟4](../assets/api/streaming-destination/step4.png)

使用在前面步驟中獲得的ID，您現在可以在Experience Platform資料與要激活資料的目標之間建立資料流。 將此步驟視為構建Experience Platform和您期望的目標之間的管道，資料稍後將通過管道流動。

要建立資料流，請執行POST請求，如下所示，同時在負載中提供下面提到的值。

執行以下POST請求以建立資料流。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`:基於配置檔案的目標的流規範ID是 `71471eba-b620-49e4-90fd-23f1fa0174d8`。 在呼叫中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用在步驟中獲得的源連接ID [連接到您的Experience Platform](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用在步驟中獲得的目標連接ID [連接到流目標](#connect-to-streaming-destination)。

**回應**

成功的響應返回ID(`id`)和 `etag`。 記下這兩個值。 將在下一步中激活段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 將資料激活到新目標 {#activate-data}

![目標步驟概述步驟5](../assets/api/streaming-destination/step5.png)

建立了所有連接和資料流後，現在您可以將配置檔案資料激活到流平台。 在此步驟中，您將選擇要發送到目標的段和配置檔案屬性，並可以計畫資料並將資料發送到目標。

要將段激活到新目標，必須執行JSONPATCH操作，如下例所示。 您可以在一次調用中激活多個段和配置檔案屬性。 要瞭解有關JSONPATCH的詳細資訊，請參閱 [RFC規範](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

| 屬性 | 說明 |
| --------- | ----------- |
| `{DATAFLOW_ID}` | 在URL中，使用在上一步中建立的資料流的ID。 |
| `{ETAG}` | 獲取 `{ETAG}` 從上一步的反應中， [建立資料流](#create-dataflow)。 上一步中的響應格式已轉義引號。 必須在請求的標題中使用未轉義值。 請參閱以下示例： <br> <ul><li>響應示例： `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>在請求中使用的值： `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> etag值會隨著資料流的每次成功更新而更新。 |
| `{SEGMENT_ID}` | 提供要導出到此目標的段ID。 要檢索要激活的段的段ID，請參見 [檢索段定義](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) Experience PlatformAPI引用中。 |
| `{PROFILE_ATTRIBUTE}` | 例如, `"person.lastName"` |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 要將段添加到資料流，請使用 `add` 的下界。 |
| `path` | 定義要更新的流的部分。 將段添加到資料流時，請使用示例中指定的路徑。 |
| `value` | 要用更新參數的新值。 |
| `id` | 指定要添加到目標資料流的段的ID。 |
| `name` | *可選*. 指定要添加到目標資料流的段的名稱。 請注意，此欄位不是必需欄位，您可以在不提供段名稱的情況下成功將段添加到目標資料流。 |

**回應**

查找202 OK響應。 未返迴響應正文。 要驗證請求是否正確，請參閱下一步驗證資料流。

## 驗證資料流

![目標步驟概述步驟6](../assets/api/streaming-destination/step6.png)

作為本教程的最後一步，您應驗證段和配置檔案屬性確實已正確映射到資料流。

要驗證此操作，請執行以下GET請求：

**API格式**

```http
GET /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:使用上一步中的資料流。
* `{ETAG}`:使用上一步中的etag。

**回應**

返回的響應應包括在 `transformations` 參數在上一步中提交的段和配置檔案屬性。 示例 `transformations` 響應中的參數如下所示：

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**導出的資料**

>[!IMPORTANT]
>
> 除了步驟中的配置檔案屬性和段之外 [將資料激活到新目標](#activate-data)，中的導出資料 [!DNL AWS Kinesis] 和 [!DNL Azure Event Hubs] 還將包括有關身份圖的資訊。 這表示導出的配置檔案的標識(例如 [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html)、移動ID、GoogleID、電子郵件地址等)。 請參閱下面的示例。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 使用 [!DNL Postman] 連接到流目標  {#collections}

要以更簡化的方式連接到本教程中描述的流式傳輸目標，您可以使用 [[!DNL Postman]](https://www.postman.com/)。

[!DNL Postman] 是一種工具，可用於進行API調用和管理預定義調用和環境的庫。

對於本特定教程，請執行以下操作 [!DNL Postman] 已附加集合：

* [!DNL AWS Kinesis] [!DNL Postman] 集合
* [!DNL Azure Event Hubs] [!DNL Postman] 集合

按一下 [這裡](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 下載收集存檔。

每個集合都包括必需的請求和環境變數， [!DNL AWS Kinesis], [!DNL Azure Event Hub]的下界。

### 如何使用 [!DNL Postman] 集合 {#how-to-use-postman-collections}

使用連接的 [!DNL Postman] 收藏，請執行以下步驟：

* 下載並安裝 [!DNL Postman];
* [下載](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 並解壓附帶的收藏；
* 將集合從其相應資料夾導入 [!DNL Postman];
* 根據本文的說明填寫環境變數；
* 運行 [!DNL API] 請求 [!DNL Postman]根據本文的說明。

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) 有關解釋錯誤響應的詳細資訊，請參閱「Platform troubleshooting guide（平台故障排除指南）」。

## 後續步驟 {#next-steps}

按照本教程，您已成功將平台連接到您首選的流式傳輸目標之一，並設定到相應目標的資料流。 傳出資料現在可以在目標中用於客戶分析或您可能希望執行的任何其他資料操作。 有關詳細資訊，請參閱以下頁：

* [目的地概觀](../home.md)
* [目標目錄概述](../catalog/overview.md)
