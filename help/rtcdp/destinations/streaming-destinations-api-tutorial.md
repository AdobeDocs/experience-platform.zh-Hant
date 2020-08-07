---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: 連線至串流目的地並啟動資料
topic: tutorial
translation-type: tm+mt
source-git-commit: dce9a7040ad25d5bb08de95fce7655f1fec7c226
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 2%

---


# 使用API連線至串流目的地，並在Adobe的即時客戶資料平台中啟動資料

>[!NOTE]
>
>Adobe [!DNL Amazon Kinesis] 即時 [!DNL Azure Event Hubs] CDP中的目標和目標目前都在測試中。 文件和功能可能會有所變更。

本教學課程示範如何使用API呼叫來連線至您的Adobe Experience Platform資料、建立串流雲端儲存目的地([Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) 或 [Azure事件中樞](/help/rtcdp/destinations/azure-event-hubs-destination.md))的連線、建立資料流至新建立的目的地，以及將資料啟動至新建立的目的地。

本教學課程在所 [!DNL Amazon Kinesis] 有範例中都使用目標，但步驟完全相同 [!DNL Azure Event Hubs]。

![概觀——建立串流目的地和啟用區段的步驟](/help/rtcdp/destinations/assets/flow-prelim.png)

如果您偏好使用Adobe即時CDP中的使用者介面來連線至目標並啟用資料，請參閱 [Connect destination](../../rtcdp/destinations/connect-destination.md)[and Activate profiles and segments to a destinational](../../rtcdp/destinations/activate-destinations.md) 。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [!DNL Experience Data Model (XDM) System](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [!DNL Catalog Service](../../catalog/home.md): [!DNL Catalog] 是Experience Platform中資料位置和世系的記錄系統。
* [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便在Adobe即時CDP中將資料啟動至串流目的地。

### 收集必要的認證

要完成本教學課程中的步驟，您應準備好下列憑證，這取決於您要連接和啟用區段的目標類型。

* 對於連 [!DNL Amazon Kinesis] 接： `accessKeyId`、 `secretKey`、 `region` or `connectionUrl`
* 對於連 [!DNL Azure Event Hubs] 接： `sasKeyName`, `sasKey``namespace`

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要和選用標題的值 {#gather-values}

若要呼叫平台API，您必須先完成驗證教 [學課程](/help/tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的資源可以隔離至特定虛擬沙盒。 在對平台API的請求中，您可以指定要進行操作的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

### Swagger檔案 {#swagger-docs}

您可在Swagger的本教學課程中，找到所有API呼叫的隨附參考檔案。 請參閱 [Adobe.io上的Flow Service API檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。 建議您同時使用本教學課程和Swagger檔案頁面。

## 取得可用串流目的地清單 {#get-the-list-of-available-streaming-destinations}

![目標步驟概述步驟1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

首先，您應決定要啟動資料的串流目的地。 首先，請執行呼叫以請求可連接並啟用區段至的可用目的地清單。 對端點執行以下GET請 `connectionSpecs` 求以返回可用目標清單：

**API格式**

```http
GET /connectionSpecs
```

**請求**

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**回應**

成功的響應包含可用目標及其唯一標識符(`id`)的清單。 儲存您計畫使用之目的地的值，因為後續步驟中將會要求它。 例如，如果您想要連線區段並傳送至或 [!DNL Amazon Kinesis] ，請 [!DNL Azure Event Hubs]在回應中尋找下列程式碼片段：

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

![目標步驟概述步驟2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

接著，您必須連線至您的Experience Platform資料，以便匯出描述檔資料並在您偏好的目的地啟用它。 這包括兩個子步驟，如下所述。

1. 首先，您必須透過設定基本連線，執行呼叫以授權存取Experience Platform中的資料。
2. 然後，使用基本連線ID，您將進行另一次呼叫，以建立來源連線，以建立與您的Experience Platform資料的連線。


### 授權存取Experience Platform中的資料

**API格式**

```http
POST /connections
```

**請求**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
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


* `{CONNECTION_SPEC_ID}`:使用統一配置式服務的連接規範ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應包含基本連接的唯一標識符(`id`)。 在下一步驟中根據需要儲存此值以建立源連接。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 連線至您的Experience Platform資料

**API格式**

```http
POST /sourceConnections
```

**請求**

```
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
* `{CONNECTION_SPEC_ID}`:使用統一配置式服務的連接規範ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**回應**

成功的響應返回新建立的源連接`id`到統一配置檔案服務的唯一標識符()。 這可確認您已成功連線至您的Experience Platform資料。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 連接至串流目的地 {#connect-to-streaming-destination}

![目標步驟概述步驟3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

在此步驟中，您要設定與所要串流目的地的連線。 這包括兩個子步驟，如下所述。

1. 首先，您必須通過設定基本連接來執行授權訪問流目的地的呼叫。
2. 然後，使用基本連接ID，您將進行另一次調用，在其中建立目標連接，該調用指定將傳送導出資料的儲存帳戶中的位置以及將導出的資料的格式。

### 授權存取串流目的地

**API格式**

```http
POST /connections
```

**請求**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "your company's holiday campaign",
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
* `{AUTHENTICATION_CREDENTIALS}`:填寫您的串流目的地名稱，例如： `Amazon Kinesis authentication credentials` 或 `Azure Event Hubs authentication credentials`者。
* `{ACCESS_ID}`: *用於[!DNL Amazon Kinesis]連接。* Amazon Kinesis儲存位置的訪問ID。
* `{SECRET_KEY}`: *用於[!DNL Amazon Kinesis]連接。* Amazon Kinesis儲存位置的密鑰。
* `{REGION}`: *用於[!DNL Amazon Kinesis]連接。* 您帳戶中Adobe [!DNL Amazon Kinesis] 即時CDP將串流您資料的地區。
* `{SAS_KEY_NAME}`: *用於[!DNL Azure Event Hubs]連接。* 填寫您的SAS密鑰名稱。 瞭解 [!DNL Azure Event Hubs] Microsoft文檔中 [如何使用SAS密鑰驗證](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{SAS_KEY}`: *用於[!DNL Azure Event Hubs]連接。* 填寫SAS密鑰。 瞭解 [!DNL Azure Event Hubs] Microsoft文檔中 [如何使用SAS密鑰驗證](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{EVENT_HUB_NAMESPACE}`: *用於[!DNL Azure Event Hubs]連接。* 填寫Adobe [!DNL Azure Event Hubs] 即時CDP將串流您資料的命名空間。 如需詳細資訊，請 [參閱檔案中的建立事件中樞](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) ，命名 [!DNL Microsoft] 空間。

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

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
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
* `{NAME_OF_DATA_STREAM}`: *用於[!DNL Amazon Kinesis]連接。* 提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。 Adobe即時CDP會將資料匯出至此串流。
* `{REGION}`: *用於[!DNL Amazon Kinesis]連接。* Amazon Kinesis帳戶中Adobe即時CDP將流資料的區域。
* `{EVENT_HUB_NAME}`: *用於[!DNL Azure Event Hubs]連接。* 填寫Adobe [!DNL Azure Event Hub] 即時CDP將串流您資料的名稱。 如需詳細資訊，請 [參閱檔案中的建立事件](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)[!DNL Microsoft] 中心。

**回應**

成功的回應會傳回新建立之目標連線`id`的唯一識別碼()，以連至您的串流目的地。 在後續步驟中，視需要儲存此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 建立資料流

![目標步驟概述步驟4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

使用您在前述步驟中取得的ID，您現在可以在Experience Platform資料和要啟用資料的目標之間建立資料流。 將此步驟設想成在Experience Platform和您所要的目的地之間建構資料稍後會透過的管道。

要建立資料流，請執行如下所示的POST請求，同時在裝載中提供以下提及的值。

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
   
        "name": "Create dataflow to Amazon Kinesis/ Azure Event Hubs",
        "description": "This operation creates a dataflow to Amazon Kinesis/ Azure Event Hubs",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ]
    }
```

* `{FLOW_SPEC_ID}`:基於配置檔案的目標的流規範ID是 `71471eba-b620-49e4-90fd-23f1fa0174d8`。 在呼叫中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用您在步驟「連線至您的Experience Platform」中 [取得的來源連線ID](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在步驟「連線至串流目的地」中 [取得的目標連線ID](#connect-to-streaming-destination)。

**回應**

成功的響應返回新創`id`建的資料流的ID()和 `etag`。 請記下這兩個值。 如同您在下個步驟中所做的，啟動區段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 將資料啟動至您的新目的地 {#activate-data}

![目標步驟概述步驟5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

建立完所有連線和資料流後，您現在可以將個人檔案資料啟動至串流平台。 在此步驟中，您可以選擇要傳送至目的地的區段和描述檔屬性，並可排程資料並傳送至目的地。

若要將區段啟用至新目的地，您必須執行JSON PATCH作業，如下例所示。 您可以在一次呼叫中啟用多個區段和描述檔屬性。 若要進一步瞭解JSON修補程式，請參閱 [RFC規格](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**請求**

```
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
    },
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
* `{SEGMENT_ID}`:提供您要匯出至此目的地的區段ID。 若要擷取您要啟用之區段的區段ID，請前往https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/，在左側導覽功能表中選取 **[!UICONTROL Segmentation Service API]** ，並尋找該操 `GET /segment/jobs` 作。
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或 `person.lastName`

**回應**

尋找202 OK回應。 不會傳回任何回應內文。 若要驗證請求是否正確，請參閱下一步「驗證資料流」。

## 驗證資料流

![目標步驟概述步驟6](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

在教學課程的最後一個步驟中，您應驗證區段和描述檔屬性確實已正確對應至資料流。

若要驗證此功能，請執行下列GET要求：

**API格式**

```http
GET /flows
```

**請求**

```
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

傳回的回應應包含在參 `transformations` 數中您在上一步驟中提交的區段和描述檔屬性。 回應中 `transformations` 的範例參數可能如下所示：

```
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
> 除了設定檔屬性和步驟「啟用資料至新目的地」中的區段外 [，和中的匯出資](#activate-data)料也 [!DNL AWS Kinesis][!DNL Azure Event Hubs] 會包含有關識別地圖的資訊。 這代表匯出的設定檔身分(例如 [ECID](https://docs.adobe.com/content/help/zh-Hant/id-service/using/intro/id-request.html)、行動ID、Google ID、電子郵件地址等)。 請參閱以下範例。

```
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

## 後續步驟

通過本教程，您成功將即時CDP連接到您首選的流目標之一，並設定資料流到相應目標。 傳出資料現在可用於客戶分析或您想要執行的任何其他資料作業的目標。 如需詳細資訊，請參閱下列頁面：

* [目的地概觀](../../rtcdp/destinations/destinations-overview.md)
* [目標目錄概觀](../../rtcdp/destinations/destinations-catalog.md)
