---
keywords: Experience Platform; home；熱門主題；API教學課程；串流目標API;平台
solution: Experience Platform
title: 使用Adobe Experience Platform的Flow Service API連線至串流目的地並啟動資料
description: 本檔案涵蓋使用Adobe Experience PlatformAPI建立串流目的地
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 1%

---


# 使用Flow Service API連線至串流目的地並啟用資料

>[!NOTE]
>
>平台中的[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目標目前處於測試階段。 文件和功能可能會有所變更。

本教學課程示範如何使用API呼叫連線至您的Adobe Experience Platform資料、建立串流雲端儲存目的地([Amazon·Kinesis](../catalog/cloud-storage/amazon-kinesis.md)或[Azure事件中樞](../catalog/cloud-storage/azure-event-hubs.md))、建立資料流至您新建立的目的地，並啟用資料至您新建立的目的地。

本教程在所有示例中都使用[!DNL Amazon Kinesis]目標，但[!DNL Azure Event Hubs]的步驟完全相同。

![概觀——建立串流目的地和啟用區段的步驟](../assets/api/streaming-destination/overview.png)

如果您偏好使用平台中的使用者介面來連接目標並啟用資料，請參閱[連接目標](../ui/connect-destination.md)和[啟用描述檔和區段至目標](../ui/activate-destinations.md)教學課程。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是Experience Platform中資料位置和世系的記錄系統。
* [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便將資料啟動至平台中的串流目的地。

### 收集必要的認證

要完成本教學課程中的步驟，您應準備好下列憑證，這取決於您要連接和啟用區段的目標類型。

* 對於[!DNL Amazon Kinesis]連接：`accessKeyId`、`secretKey`、`region`或`connectionUrl`
* 對於[!DNL Azure Event Hubs]連接：`sasKeyName`、`sasKey`、`namespace`

### 讀取範例API呼叫{#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要和可選標題的值{#gather-values}

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* 授權：載體`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的資源可以隔離到特定的虛擬沙盒。 在對平台API的請求中，您可以指定要進行操作的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* Content-Type: `application/json`

### Swagger文檔{#swagger-docs}

您可在Swagger的本教學課程中，找到所有API呼叫的隨附參考檔案。 請參閱Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)上的[Flow Service API文檔。 建議您同時使用本教學課程和Swagger檔案頁面。

## 取得可用的串流目的地清單{#get-the-list-of-available-streaming-destinations}

![目標步驟概述步驟1](../assets/api/streaming-destination/step1.png)

首先，您應決定要啟動資料的串流目的地。 首先，請執行呼叫以請求可連接並啟用區段至的可用目的地清單。 對`connectionSpecs`端點執行以下GET請求以返回可用目標清單：

**API格式**

```http
GET /connectionSpecs
```

**請求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**回應**

成功的響應包含可用目標及其唯一標識符的清單(`id`)。 儲存您計畫使用之目的地的值，因為後續步驟中將會要求它。 例如，如果您想要連線區段並傳送至[!DNL Amazon Kinesis]或[!DNL Azure Event Hubs]，請在回應中尋找下列程式碼片段：

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

## 連線至您的Experience Platform資料{#connect-to-your-experience-platform-data}

![目標步驟概述步驟2](../assets/api/streaming-destination/step2.png)

接著，您必須連線至您的Experience Platform資料，以便匯出描述檔資料並在您偏好的目的地啟用它。 這包括兩個子步驟，如下所述。

1. 首先，您必須通過設定基本連接來執行呼叫，以授權對Experience Platform中資料的訪問。
2. 然後，使用基本連接ID，您將進行另一次調用，在該調用中建立源連接，從而建立與Experience Platform資料的連接。


### 授權存取Experience Platform中的資料

**API格式**

```http
POST /connections
```

**請求**

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


* `{CONNECTION_SPEC_ID}`:使用統一配置式服務的連接規範ID -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一步驟中根據需要儲存此值以建立源連接。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 連線至您的Experience Platform資料{#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**請求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
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

* `{BASE_CONNECTION_ID}`:使用您在上一步驟中取得的ID。
* `{CONNECTION_SPEC_ID}`:使用統一配置式服務的連接規範ID -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應返回新建立的源連接到統一配置檔案服務的唯一標識符(`id`)。 這可確認您已成功連線至Experience Platform資料。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 連線至串流目的地{#connect-to-streaming-destination}

![目標步驟概述步驟3](../assets/api/streaming-destination/step3.png)

在此步驟中，您要設定與所要串流目的地的連線。 這包括兩個子步驟，如下所述。

1. 首先，您必須通過設定基本連接來執行授權訪問流目的地的呼叫。
2. 然後，使用基本連接ID，您將進行另一次調用，在其中建立目標連接，該調用指定將傳送導出資料的儲存帳戶中的位置以及將導出的資料的格式。

### 授權存取串流目的地

**API格式**

```http
POST /connections
```

**請求**

>[!IMPORTANT]
>
>下列範例包含前置有`//`的程式碼註解。 這些註解會反白標示不同串流目的地必須使用不同值的位置。 請先移除注釋，再使用程式碼片段。

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

* `{CONNECTION_SPEC_ID}`:使用在步驟獲取可用目標清單 [中獲得的連接規範ID](#get-the-list-of-available-destinations)。
* `{AUTHENTICATION_CREDENTIALS}`:填寫您的串流目的地名稱： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`者。
* `{ACCESS_ID}`: *用於 [!DNL Amazon Kinesis] 連接。* 您的AmazonKinesis儲存位置的訪問ID。
* `{SECRET_KEY}`: *用於 [!DNL Amazon Kinesis] 連接。* 你的Amazon·Kinesis儲藏室的秘密鑰匙。
* `{REGION}`: *用於 [!DNL Amazon Kinesis] 連接。* 您帳戶中平台 [!DNL Amazon Kinesis] 將串流您資料的地區。
* `{SAS_KEY_NAME}`: *用於 [!DNL Azure Event Hubs] 連接。* 填寫您的SAS密鑰名稱。瞭解如何在[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS密鑰驗證[!DNL Azure Event Hubs]。
* `{SAS_KEY}`: *用於 [!DNL Azure Event Hubs] 連接。* 填寫SAS密鑰。瞭解如何在[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS密鑰驗證[!DNL Azure Event Hubs]。
* `{EVENT_HUB_NAMESPACE}`: *用於 [!DNL Azure Event Hubs] 連接。* 填寫Platform將 [!DNL Azure Event Hubs] 在其中串流您資料的命名空間。有關詳細資訊，請參閱[!DNL Microsoft]文檔中的[建立事件集線器命名空間](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下個步驟中，如需儲存此值以建立目標連線。

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

**請求**

>[!IMPORTANT]
>
>下列範例包含前置有`//`的程式碼註解。 這些註解會反白標示不同串流目的地必須使用不同值的位置。 請先移除注釋，再使用程式碼片段。

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
* `{CONNECTION_SPEC_ID}`:使用在步驟獲取可用目標列 [表中獲得的連接規範](#get-the-list-of-available-destinations)。
* `{NAME_OF_DATA_STREAM}`: *用於 [!DNL Amazon Kinesis] 連接。* 提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。平台會將資料匯出至此串流。
* `{REGION}`: *用於 [!DNL Amazon Kinesis] 連接。* 您的AmazonKinesis帳戶中平台將串流您資料的地區。
* `{EVENT_HUB_NAME}`: *用於 [!DNL Azure Event Hubs] 連接。* 填寫平台 [!DNL Azure Event Hub] 將串流您資料的名稱。如需詳細資訊，請參閱[!DNL Microsoft]檔案中的[建立事件中樞](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)。

**回應**

成功的回應會傳回新建立的串流目的地目標連線的唯一識別碼(`id`)。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 建立資料流

![目標步驟概述步驟4](../assets/api/streaming-destination/step4.png)

使用您在前述步驟中取得的ID，您現在可以在Experience Platform資料和要啟用資料的目標之間建立資料流。 將此步驟設想成在Experience Platform和您所要的目的地之間建立資料稍後會透過的管道。

要建立資料流，請執行POST請求，如下所示，同時在裝載中提供以下提及的值。

執行以下POST請求以建立資料流。

**API格式**

```http
POST /flows
```

**請求**

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

* `{FLOW_SPEC_ID}`:基於配置檔案的目標的流規範ID是 `71471eba-b620-49e4-90fd-23f1fa0174d8`。在呼叫中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用在步驟「連接至Experience Platform」中 [獲得的源連接ID](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在步驟「連線至串流目的地」中 [取得的目標連線ID](#connect-to-streaming-destination)。

**回應**

成功的響應返回新建立的資料流的ID(`id`)和`etag`。 請記下這兩個值。 如同您在下個步驟中所做的，啟動區段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 將資料激活到新目標{#activate-data}

![目標步驟概述步驟5](../assets/api/streaming-destination/step5.png)

建立完所有連線和資料流後，您現在可以將個人檔案資料啟動至串流平台。 在此步驟中，您可以選擇要傳送至目的地的區段和描述檔屬性，並可排程資料並傳送至目的地。

若要將區段啟用至新目的地，您必須執行JSONPATCH作業，類似以下範例。 您可以在一次呼叫中啟用多個區段和描述檔屬性。 若要進一步瞭解JSONPATCH，請參閱[RFC規格](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**請求**

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
* `{SEGMENT_ID}`:提供您要匯出至此目的地的區段ID。若要擷取您要啟用之區段的區段ID，請前往&#x200B;**https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**，在左側導覽功能表中選取&#x200B;**[!UICONTROL 分段服務API]**，並在&#x200B;**[!UICONTROL 區段定義]**&#x200B;中尋找`GET /segment/definitions`操作。
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或  `person.lastName`

**回應**

尋找202 OK回應。 不會傳回任何回應內文。 若要驗證請求是否正確，請參閱下一步「驗證資料流」。

## 驗證資料流

![目標步驟概述步驟6](../assets/api/streaming-destination/step6.png)

在教學課程的最後一個步驟中，您應驗證區段和描述檔屬性確實已正確對應至資料流。

要驗證此GET，請執行以下請求：

**API格式**

```http
GET /flows
```

**請求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:使用上一步驟的資料流。
* `{ETAG}`:使用上一步驟的etag。

**回應**

傳回的回應應包含在`transformations`參數中，您在上一步驟中提交的區段和描述檔屬性。 回應中的範例`transformations`參數可能如下所示：

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
> 除了步驟[將資料啟動至新目的地](#activate-data)中的描述檔屬性和區段外，[!DNL AWS Kinesis]和[!DNL Azure Event Hubs]中的匯出資料也會包含有關識別映射的資訊。 這代表匯出的設定檔身分（例如[ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html)、行動ID、Google ID、電子郵件地址等）。 請參閱以下範例。

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

## 使用Postman集合連接到流目標{#collections}

若要以更簡化的方式連接至本教學課程中所述的串流目的地，您可使用[[!DNL Postman]](https://www.postman.com/)。

[!DNL Postman] 是一種工具，可用來進行API呼叫並管理預先定義之呼叫和環境的程式庫。

在本特定教學課程中，已附上下列[!DNL Postman]系列：

* [!DNL AWS Kinesis] [!DNL Postman] 系列
* [!DNL Azure Event Hubs] [!DNL Postman] 系列

按一下[這裡](../assets/api/streaming-destination/DestinationPostmanCollection.zip)下載系列封存。

每個系列分別包含[!DNL AWS Kinesis]和[!DNL Azure Event Hub]的必要請求和環境變數。

### 如何使用郵遞員系列

要使用附加的[!DNL Postman]系列成功連接到目標，請執行以下步驟：

* 下載並安裝[!DNL Postman];
* [下](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 載並解壓縮所附的系列；
* 將收藏集從對應的資料夾匯入郵遞員；
* 根據本文的說明填寫環境變數；
* 根據本文中的說明，執行Postman的[!DNL API]請求。

## 後續步驟

在本教學課程中，您已成功將平台連接至您偏好的串流目的地，並設定資料流至個別目的地。 傳出資料現在可用於客戶分析或您想要執行的任何其他資料作業的目標。 如需詳細資訊，請參閱下列頁面：

* [目的地概觀](../home.md)
* [目標目錄概觀](../catalog/overview.md)
