---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 匯出工作API端點
topic: 指南
type: Documentation
description: 即時客戶個人檔案可讓您將來自多個來源的資料（包括屬性資料和行為資料）整合在一起，以建立Adobe Experience Platform地區個別客戶的單一檢視。 然後可將描述檔資料匯出至資料集以進一步處理。
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 2%

---

# 導出作業端點

[!DNL Real-time Customer Profile] 可讓您將來自多個來源的資料（包括屬性資料和行為資料）匯集在一起，以建立個別客戶的單一檢視。然後可將描述檔資料匯出至資料集以進一步處理。 例如，[!DNL Profile]資料的讀者區段可匯出以進行啟動，而描述檔屬性則可匯出以進行報告。

本檔案提供使用[描述檔API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)建立和管理匯出工作的逐步指示。

>[!NOTE]
>
>本指南涵蓋[!DNL Profile API]中導出作業的使用。 如需如何管理Adobe Experience Platform分段服務匯出工作的詳細資訊，請參閱分段API](../../profile/api/export-jobs.md)中[匯出工作的指南。

除了建立導出作業外，您還可以使用`/entities`端點訪問[!DNL Profile]資料，也稱為&quot;[!DNL Profile Access]&quot;。 如需詳細資訊，請參閱[entities端點指南](./entities.md)。 有關如何使用UI訪問[!DNL Profile]資料的步驟，請參閱[使用手冊](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是[!DNL Real-time Customer Profile] API的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 建立匯出工作

匯出[!DNL Profile]資料需要先建立資料匯出至的資料集，然後開始新的匯出工作。 這兩個步驟都可透過Experience PlatformAPI來達成，前者使用目錄服務API，後者則使用即時客戶設定檔API。 以下各節將列出完成每個步驟的詳細說明。

### 建立目標資料集

匯出[!DNL Profile]資料時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構（以下API範例請求中的`schemaRef.id`）。 為了匯出描述檔資料，資料集必須以[!DNL XDM Individual Profile]聯合結構(`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合了共用相同類的模式的欄位。 在本例中，這是[!DNL XDM Individual Profile]類。 有關聯合視圖方案的詳細資訊，請參閱方案構成指南的基本資訊](../../xdm/schema/composition.md#union)中的[union部分。

本教學課程中後續的步驟概述如何使用[!DNL Catalog] API建立參照[!DNL XDM Individual Profile]聯合架構的資料集。 您也可以使用[!DNL Platform]使用者介面來建立參照聯合架構的資料集。 使用UI的步驟在[本UI教學課程中說明，以匯出區段](../../segmentation/tutorials/create-dataset-export-segment.md)，但也適用於此處。 完成後，您可以返回本教程，繼續[啟動新導出作業的步驟](#initiate)。

如果您已擁有相容的資料集並知道其ID，則可直接執行啟動新匯出工作的步驟[。](#initiate)

**API格式**

```http
POST /dataSets
```

**要求**

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
          "persisted": true
        }
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合檢視（結構）ID。 |
| `fileDescription.persisted` | 布爾值，設為`true`時，可讓資料集持續存留在聯合檢視中。 |

**回應**

成功的回應會傳回包含新建立資料集之唯讀、系統產生、唯一ID的陣列。 要成功匯出描述檔資料，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 啟動導出作業{#initiate}

在您擁有持續統一的資料集後，您可以建立匯出工作，將描述檔資料保存至資料集，方法是在即時客戶描述檔API中向`/export/jobs`端點提出POST要求，並提供您要在請求內文中匯出的資料詳細資訊。

**API格式**

```http
POST /export/jobs
```

**要求**

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
| `fields` | *（可選）* 將要包含在導出中的資料欄位限制為僅限此參數中提供的資料欄位。省略此值會導致所有欄位都包含在匯出的資料中。 |
| `mergePolicy` | *（可選）指* 定用於管理導出資料的合併策略。當有多個區段要匯出時，請加入此參數。 |
| `mergePolicy.id` | 合併策略的ID。 |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 省略此值將預設為最新版本。 |
| `additionalFields.eventList` | *（可選）* 通過提供以下一個或多個設定來控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`eventList.fields`:控制要匯出的欄位。</li><li>`eventList.filter`:指定限制關聯對象所包含結果的標準。預期匯出所需的最低值，通常為日期。</li><li>`eventList.filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳記後所擷取的事件。這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）匯** 出資料的目標資訊：<ul><li>`destination.datasetId`: **（必要）** 要匯出資料的資料集ID。</li><li>`destination.segmentPerBatch`: *（選用）* 布林值，若未提供，預設為 `false`。值`false`會將所有區段ID匯出為單一批次ID。 值`true`會將一個區段ID匯出為一個批次ID。 請注意，將值設定為`true`可能會影響批導出效能。</li></ul> |
| `schema.name` | **（必要）** 與要匯出資料的資料集關聯的架構名稱。 |

>[!NOTE]
>
>若要僅匯出描述檔資料而不包含相關的時間系列資料，請從請求中移除「additionalFields」物件。

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

您可以對`export/jobs`端點執行GET請求，以傳回特定IMS組織的所有匯出作業清單。 此請求也支援查詢參數`limit`和`offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| -------- | ----------- |
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 依照請求的建立時間傳回特定的結果頁面。 範例：`page=2` |
| `sort` | 按特定欄位的升序(**`asc`**)或降序(**`desc`**)排序結果。 傳回多頁結果時，排序參數無法運作。 範例：`sort=updateTime:asc` |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

回應包含`records`物件，其中包含由IMS組織建立的匯出工作。

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

要查看特定導出作業的詳細資訊或監視其處理時的狀態，可以向`/export/jobs`端點發出GET請求，並將導出作業的`id`包含在路徑中。 在`status`欄位返回值&quot;SUCCEEDED&quot;後，導出作業即完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要訪問的導出作業的`id`。 |

**要求**

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

Experience Platform允許您取消現有的導出作業，這可能有用於許多原因，包括如果導出作業未完成或在處理階段卡住。 為了取消導出作業，可以對`/export/jobs`端點執行DELETE請求，並將要取消的導出作業的`id`包含到請求路徑。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 要訪問的導出作業的`id`。 |

**要求**

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

匯出成功後，您的資料就可在Experience Platform的資料湖中使用。 然後，您可以使用[資料存取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)，使用與匯出相關聯的`batchId`存取資料。 視匯出大小而定，資料可能以區塊為單位，而批次可能由數個檔案組成。

有關如何使用Data Access API存取和下載批處理檔案的逐步說明，請遵循[資料存取教程](../../data-access/tutorials/dataset-data.md)。

您也可以使用Adobe Experience Platform查詢服務訪問成功導出的即時客戶概要檔案資料。 使用UI或REST風格的API，查詢服務可讓您編寫、驗證及執行資料湖中資料的查詢。

有關如何查詢受眾資料的更多資訊，請參閱[查詢服務檔案](../../query-service/home.md)。

## 附錄

下節包含描述檔API中匯出工作的其他資訊。

### 其他匯出裝載範例

[啟始匯出工作](#initiate)一節中顯示的範例API呼叫會建立同時包含描述檔（記錄）和事件（時間系列）資料的工作。 本節提供其他請求裝載範例，以限制您的匯出包含一種或另一種資料類型。

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

您也可以使用匯出工作端點來匯出對象區段，而非[!DNL Profile]資料。 如需詳細資訊，請參閱區段API](../../segmentation/api/export-jobs.md)中[匯出工作的指南。
