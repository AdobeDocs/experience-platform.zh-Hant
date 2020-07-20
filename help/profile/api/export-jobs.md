---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 匯出工作——即時客戶個人檔案API
topic: guide
translation-type: tm+mt
source-git-commit: 2c0466bf0534d09e3cad54caef213def122d948b
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 2%

---


# 導出作業端點

[!DNL Real-time Customer Profile] 可讓您將來自多個來源的資料（包括屬性資料和行為資料）匯集在一起，以建立個別客戶的單一檢視。 然後，可將內 [!DNL Profile] 部可用的資料匯出至資料集，以進一步處理。 例如，可從資料匯出 [!DNL Profile] 受眾區段以進行啟動，並匯出描述檔屬性以進行報告。

本檔案提供使用描述檔API建立和管理匯出工作的逐 [步指示](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

>[!NOTE]
>
>本指南涵蓋在中使用匯出工作 [!DNL Profile API]。 如需如何管理Adobe Experience Platform Segmentation Service匯出工作的詳細資訊，請參閱「分段API」 [中的匯出工作指南](../../profile/api/export-jobs.md)。

除了建立導出作業外，您還可以使 [!DNL Profile] 用端點 `/entities` (也稱為「[!DNL Profile Access]」)訪問資料。 See the [entities endpoint guide](./entities.md) for more information. 如需如何使用UI存 [!DNL Profile] 取資料的步驟，請參閱使 [用指南](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是 [!DNL Real-time Customer Profile] API的一部分。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 建立匯出工作

匯出 [!DNL Profile] 資料需要先建立資料要匯出到的資料集，然後開始新的匯出工作。 這兩個步驟都可使用Experience Platform API來完成，前者使用Catalog Service API，後者則使用即時客戶設定檔API。 以下各節將列出完成每個步驟的詳細說明。

### 建立目標資料集

匯出資 [!DNL Profile] 料時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構(在下`schemaRef.id` 面的API範例請求中)。 為了匯出描述檔資料，資料集必須以 [!DNL XDM Individual Profile] Union Schema(`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合了共用相同類的模式的欄位。 在這種情況下，這就是 [!DNL XDM Individual Profile] 班。 有關聯合視圖方案的詳細資訊，請參 [閱方案構成指南基礎中的聯合部分](../../xdm/schema/composition.md#union)。

本教學課程中後續的步驟概述如何使用API建立參照 [!DNL XDM Individual Profile] Union Schema的資 [!DNL Catalog] 料集。 您也可以使用使 [!DNL Platform] 用使用者介面來建立參照聯合架構的資料集。 使用UI的步驟在本UI教學課程中 [列出，可匯出區段](../../segmentation/tutorials/create-dataset-export-segment.md) ，但也適用於此處。 完成後，您可以返回本教學課程，繼續啟動新 [導出作業的步驟](#initiate)。

如果您已擁有相容的資料集並知道其ID，則可直接執行開始新匯 [出工作的步驟](#initiate)。

**API格式**

```http
POST /dataSets
```

**請求**

下列請求會建立新資料集，提供裝載中的設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合檢視（結構）ID。 |
| `fileDescription.persisted` | 布爾值，設定為 `true`時，可讓資料集在聯合檢視中持續存在。 |

**回應**

成功的回應會傳回包含新建立資料集之唯讀、系統產生、唯一ID的陣列。 要成功匯出描述檔資料，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 啟始匯出工作 {#initiate}

在您擁有持續統一的資料集後，可以建立匯出工作，將描述檔資料保存至資料集，方法是對即時客戶描述檔API中的端點提出POST請求，並提供您要在請求正文中匯出的資料詳細資訊。 `/export/jobs`

**API格式**

```http
POST /export/jobs
```

**請求**

下列請求會建立新的匯出工作，提供裝載中的設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| 屬性 | 說明 |
| -------- | ----------- |
| `fields` | *（可選）* ，將要包含在導出中的資料欄位限制為僅限此參數中提供的資料欄位。 省略此值會導致所有欄位都包含在匯出的資料中。 |
| `mergePolicy` | *（可選）* 指定用於管理導出資料的合併策略。 當有多個區段要匯出時，請加入此參數。 |
| `mergePolicy.id` | 合併策略的ID。 |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 省略此值將預設為最新版本。 |
| `additionalFields.eventList` | *（可選）* ，提供下列一或多個設定，以控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`eventList.fields`: 控制要匯出的欄位。</li><li>`eventList.filter`: 指定限制關聯對象所包含結果的標準。 預期匯出所需的最低值，通常為日期。</li><li>`eventList.filter.fromIngestTimestamp`: 將時間序列事件篩選為在提供的時間戳記後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）** ，匯出資料的目標資訊：<ul><li>`destination.datasetId`: **（必要）** ，要匯出資料的資料集ID。</li><li>`destination.segmentPerBatch`: *（可選）* ，一個布爾值，如果未提供，則預設為 `false`。 值將所有 `false` 區段ID匯出為單一批次ID。 值將一個 `true` 區段ID匯出為一個批次ID。 請注意，將值設定為可能 `true` 會影響批導出效能。</li></ul> |
| `schema.name` | **（必要）** ，與要匯出資料的資料集關聯的架構名稱。 |

>[!NOTE] 若要僅匯出描述檔資料而不包含相關的時間系列資料，請從請求中移除「additionalFields」物件。

**回應**

成功的回應會傳回填入「描述檔」資料的資料集，如請求中所指定。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## 列出所有匯出工作

您可以執行GET請求至端點，傳回特定IMS組織所有匯出工作的清 `export/jobs` 單。 請求也支援查詢參 `limit` 數 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| -------- | ----------- |
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例: `start=4` |
| `limit` | 限制傳回的結果數。 範例: `limit=10` |
| `page` | 依照請求的建立時間傳回特定的結果頁面。 範例: `page=2` |
| `sort` | 按特定欄位的遞增( **`asc`** )或遞減( **`desc`** )順序排序結果。 傳回多頁結果時，排序參數無法運作。 範例: `sort=updateTime:asc` |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

回應包含包 `records` 含由IMS組織建立之匯出工作的物件。

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## 監視導出進度

要查看特定導出作業的詳細資訊，或在其處理過程中監視其狀態，可以向端點發出GET請求，並將導出作業的 `/export/jobs``id` 內容包括在路徑中。 一旦欄位傳回值&quot;SUCCEEDED&quot;, `status` 匯出工作就會完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您 `id` 要存取的匯出工作。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `batchId` | 從成功匯出建立的批次識別碼，在讀取描述檔資料時用於查閱。 |

## 取消匯出工作

Experience Platform可讓您取消現有的匯出工作，這在許多原因（包括匯出工作未完成或在處理階段卡住）中可能很有用。 為了取消導出作業，可以對端點執行DELETE請 `/export/jobs` 求，並將要取消 `id` 的導出作業包括到請求路徑。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您 `id` 要存取的匯出工作。 |

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的刪除請求會傳回HTTP狀態204（無內容）和空回應主體，指出取消作業成功。

## 後續步驟

匯出成功後，您的資料就可在Experience Platform的資料湖中使用。 然後，您就可以使 [用「資料存取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 」，使用與匯出相 `batchId` 關的資料來存取資料。 視匯出大小而定，資料可能以區塊為單位，而批次可能由數個檔案組成。

如需如何使用資料存取API存取和下載批次檔案的逐步指示，請依照資料存取教 [學課程](../../data-access/tutorials/dataset-data.md)。

您也可以使用Adobe Experience Platform Query Service，存取成功匯出的即時客戶個人檔案資料。 使用UI或REST風格的API，查詢服務可讓您在資料湖中寫入、驗證及執行資料查詢。

如需如何查詢觀眾資料的詳細資訊，請參閱查詢服 [務檔案](../../query-service/home.md)。

## 附錄

下節包含描述檔API中匯出工作的其他資訊。

### 其他匯出裝載範例

啟始匯出工作一節中顯示的範例API [呼叫](#initiate) ，會建立同時包含描述檔（記錄）和事件（時間系列）資料的工作。 本節提供其他請求裝載範例，以限制您的匯出包含一種或另一種資料類型。

下列裝載會建立僅包含描述檔資料（無事件）的匯出工作：

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

若要建立僅包含事件資料（無描述檔屬性）的匯出工作，裝載的外觀可能類似下列：

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### 匯出區段

您也可以使用匯出工作端點來匯出讀者區段，而非匯出 [!DNL Profile] 資料。 如需詳細資訊，請 [參閱區段API中的匯出工作指南](../../segmentation/api/export-jobs.md) 。