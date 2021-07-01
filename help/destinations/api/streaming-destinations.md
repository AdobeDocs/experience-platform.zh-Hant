---
keywords: Experience Platform；首頁；熱門主題；API教學課程；串流目的地API;平台
solution: Experience Platform
title: 使用Adobe Experience Platform中的「流量服務API」連線至串流目的地並啟用資料
description: 本檔案說明如何使用Adobe Experience Platform API建立串流目的地
topic-legacy: tutorial
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 0bc85d79bab690d433dc29d558a4d9caf086586d
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 1%

---

# 使用流量服務API連線至串流目的地並啟用資料

>[!NOTE]
>
>Platform中的[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目的地目前為測試版。 文件和功能可能會有所變更。

本教學課程示範如何使用API呼叫連線至您的Adobe Experience Platform資料、建立串流雲端儲存目的地([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md)或[Azure事件樞紐](../catalog/cloud-storage/azure-event-hubs.md))的連線、建立資料流至您新建立的目的地，以及啟用資料至您新建立的目的地。

本教學課程在所有範例中都使用[!DNL Amazon Kinesis]目的地，但[!DNL Azure Event Hubs]的步驟相同。

![概述 — 建立串流目的地和啟用區段的步驟](../assets/api/streaming-destination/overview.png)

如果您偏好使用Platform中的使用者介面來連線至目的地並啟用資料，請參閱[連線目的地](../ui/connect-destination.md)和[啟用設定檔和區段至目的地](../ui/activate-destinations.md)教學課程。

## 開始使用

本指南需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是記錄Experience Platform內資料位置和世系的系統。
* [沙箱](../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要了解的其他資訊，以便將資料啟用至Platform中的串流目的地。

### 收集所需憑據

若要完成本教學課程中的步驟，您應根據您要連線和啟用區段的目的地類型，備妥下列憑證。

* 對於[!DNL Amazon Kinesis]連接：`accessKeyId`、`secretKey`、`region`或`connectionUrl`
* 對於[!DNL Azure Event Hubs]連接：`sasKeyName`, `sasKey`, `namespace`

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的區段。

### 收集必要和選用標題的值 {#gather-values}

若要呼叫Platform API，您必須先完成[authentication教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載`{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的資源可以隔離至特定虛擬沙箱。 在向Platform API提出的請求中，您可以指定要執行操作之沙箱的名稱和ID。 這些是選用參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* Content-Type: `application/json`

### Swagger檔案 {#swagger-docs}

您可以在Swagger中找到本教學課程中所有API呼叫的隨附參考檔案。 請參閱[Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)上的流量服務API檔案。 建議您同時使用本教學課程和Swagger檔案頁面。

## 取得可用串流目的地的清單 {#get-the-list-of-available-streaming-destinations}

![目標步驟概述步驟1](../assets/api/streaming-destination/step1.png)

首先，您應決定要啟用資料的串流目的地。 若要開始使用，請執行呼叫，以要求可供連線及啟用區段的可用目的地清單。 向`connectionSpecs`端點執行以下GET請求以返回可用目的地清單：

**API格式**

```http
GET /connectionSpecs
```

**要求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**回應**

成功的回應包含可用目的地及其唯一識別碼的清單(`id`)。 儲存您打算使用的目的地值，因為後續步驟將需要它。 例如，如果您要連線並將區段傳送至[!DNL Amazon Kinesis]或[!DNL Azure Event Hubs]，請在回應中尋找下列程式碼片段：

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

## 連線至您的Experience Platform資料 {#connect-to-your-experience-platform-data}

![目標步驟概述步驟2](../assets/api/streaming-destination/step2.png)

接下來，您必須連線至您的Experience Platform資料，以便匯出設定檔資料並在您偏好的目的地啟用。 這包含兩個子步驟，如下所述。

1. 首先，您必須透過設定基本連線，執行呼叫，授權存取Experience Platform中的資料。
2. 然後，使用基本連線ID，您將進行另一個呼叫，在其中建立來源連線，以建立與Experience Platform資料的連線。


### 授權存取Experience Platform中的資料

**API格式**

```http
POST /connections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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


* `{CONNECTION_SPEC_ID}`:使用配置檔案服務的連接規範ID  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一步建立源連接時，按需要儲存此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 連線至您的Experience Platform資料 {#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上一步中取得的ID。
* `{CONNECTION_SPEC_ID}`:使用配置檔案服務的連接規範ID  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應返回新建立的源連接到配置檔案服務的唯一標識符(`id`)。 這可確認您已成功連線至Experience Platform資料。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 連線至串流目的地 {#connect-to-streaming-destination}

![目標步驟概述步驟3](../assets/api/streaming-destination/step3.png)

在此步驟中，您會設定與所需串流目的地的連線。 這包含兩個子步驟，如下所述。

1. 首先，您必須透過設定基本連線，執行呼叫以授權存取串流目的地。
2. 然後，使用基本連接ID，您將進行另一個呼叫，在其中建立目標連接，指定儲存帳戶中要傳送匯出資料的位置，以及要匯出的資料格式。

### 授權存取串流目的地

**API格式**

```http
POST /connections
```

**要求**

>[!IMPORTANT]
>
>以下範例包含前置詞為`//`的程式碼註解。 這些註解會反白標示必須針對不同串流目的地使用不同值的位置。 使用此代碼段之前，請刪除這些注釋。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{CONNECTION_SPEC_ID}`:使用在獲取可用目的地清單中 [獲得的連接規範ID](#get-the-list-of-available-destinations)。
* `{AUTHENTICATION_CREDENTIALS}`:填入串流目的地的名稱： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`。
* `{ACCESS_ID}`: *用於 [!DNL Amazon Kinesis] 連接。* Amazon Kinesis儲存位置的存取ID。
* `{SECRET_KEY}`: *用於 [!DNL Amazon Kinesis] 連接。* Amazon Kinesis儲存位置的機密金鑰。
* `{REGION}`: *用於 [!DNL Amazon Kinesis] 連接。* Platform將串流您 [!DNL Amazon Kinesis] 資料的帳戶地區。
* `{SAS_KEY_NAME}`: *用於 [!DNL Azure Event Hubs] 連接。* 填寫SAS密鑰名。了解[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中的SAS密鑰驗證[!DNL Azure Event Hubs]。
* `{SAS_KEY}`: *用於 [!DNL Azure Event Hubs] 連接。* 填入SAS密鑰。了解[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中的SAS密鑰驗證[!DNL Azure Event Hubs]。
* `{EVENT_HUB_NAMESPACE}`: *用於 [!DNL Azure Event Hubs] 連接。* 填入Platform將 [!DNL Azure Event Hubs] 用來串流您資料的命名空間。有關詳細資訊，請參閱[!DNL Microsoft]文檔中的[建立事件集線器命名空間](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一步建立目標連線時，視需要儲存此值。

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
>以下範例包含前置詞為`//`的程式碼註解。 這些註解會反白標示必須針對不同串流目的地使用不同值的位置。 使用此代碼段之前，請刪除這些注釋。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{BASE_CONNECTION_ID}`:使用您在上述步驟中取得的基本連線ID。
* `{CONNECTION_SPEC_ID}`:使用在獲取可用目的地清單 [中獲得的連接規格](#get-the-list-of-available-destinations)。
* `{NAME_OF_DATA_STREAM}`: *用於 [!DNL Amazon Kinesis] 連接。* 提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。Platform會將資料匯出至此資料流。
* `{REGION}`: *用於 [!DNL Amazon Kinesis] 連接。* Amazon Kinesis帳戶中Platform將串流您資料的地區。
* `{EVENT_HUB_NAME}`: *用於 [!DNL Azure Event Hubs] 連接。* 填入Platform [!DNL Azure Event Hub] 將串流您資料的名稱。如需詳細資訊，請參閱[!DNL Microsoft]檔案中的[建立事件中樞](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) 。

**回應**

成功的回應會傳回新建立的目標連線唯一識別碼(`id`)，以連線至您的串流目的地。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 建立資料流

![目標步驟概述步驟4](../assets/api/streaming-destination/step4.png)

您現在可以使用在前述步驟中取得的ID，在Experience Platform資料與要啟用資料的目標之間建立資料流。 請將此步驟想像成建構管道，資料稍後會透過管道在Experience Platform和您想要的目的地之間流動。

若要建立資料流，請執行POST請求，如下所示，同時在裝載中提供以下提及的值。

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
-H 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{FLOW_SPEC_ID}`:基於配置檔案的目的地的流規範ID為 `71471eba-b620-49e4-90fd-23f1fa0174d8`。在呼叫中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用在「連線至您的Experience Platform」步驟中 [取得的來源連線ID](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在「連線至串流目的地」步驟中取 [得的目標連線ID](#connect-to-streaming-destination)。

**回應**

成功的響應返回新建立的資料流的ID(`id`)和`etag`。 請記下這兩個值。 如同您在下一步中啟動區段時一樣。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 將資料啟用到新目的地 {#activate-data}

![目標步驟概述步驟5](../assets/api/streaming-destination/step5.png)

建立了所有連線和資料流後，您就可以將設定檔資料啟用至串流平台。 在此步驟中，您可以選取要傳送至目的地的區段以及設定檔屬性，並可排程及傳送資料至目的地。

若要將區段啟用至新目的地，您必須執行JSONPATCH作業，如下列範例所示。 您可以在一個呼叫中啟用多個區段和設定檔屬性。 若要深入了解JSONPATCH，請參閱[RFC規格](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{DATAFLOW_ID}`:使用您在上一步驟中取得的資料流。
* `{ETAG}`:使用您在上一步驟中取得的標籤。
* `{SEGMENT_ID}`:提供您要匯出至此目的地的區段ID。若要擷取您要啟用之區段的區段ID，請前往&#x200B;**https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**，在左側導覽功能表中選取&#x200B;**[!UICONTROL 分段服務API]**，然後在&#x200B;**[!UICONTROL 區段定義]**&#x200B;中尋找`GET /segment/definitions`操作。
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或  `person.lastName`

**回應**

尋找202 OK回應。 未傳回回應內文。 若要驗證請求是否正確，請參閱下一步「驗證資料流」。

## 驗證資料流

![目標步驟概述步驟6](../assets/api/streaming-destination/step6.png)

作為本教學課程的最後一步，您應驗證區段和設定檔屬性確實已正確對應至資料流。

若要驗證，請執行下列GET要求：

**API格式**

```http
GET /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:使用上一步的資料流。
* `{ETAG}`:使用上一步的標籤。

**回應**

傳回的回應應包含在`transformations`參數中，亦即您在上一步驟中提交的區段和設定檔屬性。 回應中的範例`transformations`參數可能如下所示：

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

**匯出的資料**

>[!IMPORTANT]
>
> 除了設定檔屬性和步驟[啟用資料至新目的地](#activate-data)中的區段外， [!DNL AWS Kinesis]和[!DNL Azure Event Hubs]中的匯出資料也包含身分對應的相關資訊。 這代表匯出設定檔的身分（例如[ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html)、行動ID、Google ID、電子郵件地址等）。 請參閱下列範例。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
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

## 使用Postman集合連線至串流目的地  {#collections}

若要以更簡化的方式連線至本教學課程中說明的串流目的地，您可以使用[[!DNL Postman]](https://www.postman.com/)。

[!DNL Postman] 是一種工具，可用來進行API呼叫，以及管理預先定義之呼叫和環境的程式庫。

針對此特定教學課程，已附加下列[!DNL Postman]集合：

* [!DNL AWS Kinesis] [!DNL Postman] 集合
* [!DNL Azure Event Hubs] [!DNL Postman] 集合

按一下[這裡](../assets/api/streaming-destination/DestinationPostmanCollection.zip)以下載集合封存檔。

每個集合分別包含[!DNL AWS Kinesis]和[!DNL Azure Event Hub]所需的要求和環境變數。

### 如何使用Postman集合

若要使用附加的[!DNL Postman]集合成功連線至目的地，請執行下列步驟：

* 下載並安裝[!DNL Postman];
* [](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 下載並解壓縮附加的集合；
* 將集合從其對應的資料夾匯入Postman;
* 根據本文的指示填入環境變數；
* 根據本文的指示，執行Postman的[!DNL API]請求。

## 後續步驟

依照本教學課程，您已成功將Platform連線至您其中一個偏好的串流目的地，並設定連線至個別目的地的資料流。 傳出資料現在可用於客戶分析的目的地，或您可能想執行的任何其他資料作業。 如需詳細資訊，請參閱下列頁面：

* [目的地概觀](../home.md)
* [目的地目錄概觀](../catalog/overview.md)
