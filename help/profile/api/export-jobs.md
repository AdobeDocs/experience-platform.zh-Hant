---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 配置檔案導出作業API端點
type: Documentation
description: 即時客戶設定檔可讓您將來自多個來源的資料（包括屬性資料和行為資料）整合在一起，以建立Adobe Experience Platform中個別客戶的單一檢視。 接著，可將設定檔資料匯出至資料集以進一步處理。
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# 配置檔案導出作業端點

[!DNL Real-Time Customer Profile] 可讓您將來自多個來源的資料（包括屬性資料和行為資料）集合在一起，以建立個別客戶的單一檢視。 接著，可將設定檔資料匯出至資料集以進一步處理。 例如，來自 [!DNL Profile] 資料可匯出以供啟用，設定檔屬性可匯出以供報告。

本檔案提供逐步指示，說明如何使用 [設定檔API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>本指南涵蓋在 [!DNL Profile API]. 如需如何管理Adobe Experience Platform Segmentation Service匯出工作的資訊，請參閱 [匯出分段API中的工作](../../profile/api/export-jobs.md).

除了建立匯出工作，您也可以存取 [!DNL Profile] 資料使用 `/entities` 端點，也稱為「[!DNL Profile Access]」。 請參閱 [entities endpoint guide（圖元端點指南）](./entities.md) 以取得更多資訊。 如需存取 [!DNL Profile] 使用UI的資料，請參閱 [使用手冊](../ui/user-guide.md).

## 快速入門

本指南中使用的API端點屬於 [!DNL Real-Time Customer Profile] API。 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 建立匯出作業

匯出 [!DNL Profile] 資料需要先建立要匯出資料的資料集，然後開始執行新的匯出工作。 這兩個步驟皆可透過Experience PlatformAPI來達成，前者使用目錄服務API，後者則使用即時客戶設定檔API。 以下各節將列出完成每個步驟的詳細指示。

### 建立目標資料集

匯出時 [!DNL Profile] 資料，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

其中一項主要考量事項為資料集所依據的結構(`schemaRef.id` （在以下的API範例請求中）。 若要匯出設定檔資料，資料集必須以 [!DNL XDM Individual Profile] 聯合架構(`https://ns.adobe.com/xdm/context/profile__union`)。 聯合架構是系統產生的唯讀架構，可匯總共用相同類別之架構的欄位。 在此案例中， [!DNL XDM Individual Profile] 類別。 如需聯合檢視結構的詳細資訊，請參閱 [綱要構成指南中的union一節](../../xdm/schema/composition.md#union).

本教學課程中後續的步驟將概述如何建立參考資料集 [!DNL XDM Individual Profile] 聯合架構使用 [!DNL Catalog] API。 您也可以使用 [!DNL Platform] 使用者介面，以建立參考聯合結構的資料集。 使用UI的步驟概述於 [此匯出區段的UI教學課程](../../segmentation/tutorials/create-dataset-export-segment.md) 也適用於此。 完成後，您可以返回本教學課程，繼續下列步驟 [啟動新導出作業](#initiate).

如果您已有相容的資料集且知道其ID，可以直接繼續進行 [啟動新導出作業](#initiate).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 與資料集關聯的聯合檢視（結構）ID。 |

**回應**

成功的回應會傳回一個陣列，內含新建立資料集的唯讀、系統產生、唯一ID。 若要成功匯出「設定檔」資料，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 啟動導出作業 {#initiate}

在您擁有持續存在聯合的資料集後，您可以建立匯出工作，對 `/export/jobs` 端點（即時客戶設定檔API中），並在請求內文中提供您要匯出的資料詳細資訊。

**API格式**

```http
POST /export/jobs
```

**要求**

下列請求會建立新的匯出工作，並在裝載中提供設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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
| `fields` | *（可選）* 將匯出中包含的資料欄位限制為僅限此參數中提供的資料欄位。 省略此值會導致匯出資料中包含所有欄位。 |
| `mergePolicy` | *（可選）* 指定用於管理導出資料的合併策略。 有多個要匯出的區段時，請加入此參數。 |
| `mergePolicy.id` | 合併策略的ID。 |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 省略此值會預設為最新版本。 |
| `additionalFields.eventList` | *（可選）* 通過提供以下一個或多個設定，控制為子對象或關聯對象導出的時間序列事件欄位：<ul><li>`eventList.fields`:控制要匯出的欄位。</li><li>`eventList.filter`:指定用於限制從關聯對象中包括的結果的標準。 預期匯出所需的最小值，通常為日期。</li><li>`eventList.filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳記之後擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）** 匯出資料的目的地資訊：<ul><li>`destination.datasetId`: **（必要）** 要匯出資料的資料集ID。</li><li>`destination.segmentPerBatch`: *（可選）* 布林值（若未提供）預設為 `false`. 值 `false` 將所有區段ID匯出為單一批次ID。 值 `true` 將一個區段ID匯出為一個批次ID。 請注意，將值設為 `true` 可能會影響批導出效能。</li></ul> |
| `schema.name` | **（必要）** 與要匯出資料的資料集相關聯的結構名稱。 |

>[!NOTE]
>
>若要僅匯出設定檔資料而不包含相關的時間序列資料，請從請求中移除「additionalFields」物件。

**回應**

成功的回應會傳回以要求中指定的設定檔資料填入的資料集。

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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## 列出所有導出作業

您可以向傳回特定IMS組織的所有匯出工作清單，方法是執行GET請求 `export/jobs` 端點。 請求也支援查詢參數 `limit` 和 `offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| -------- | ----------- |
| `start` | 依照請求的建立時間，偏移傳回的結果頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 根據請求的建立時間，傳回特定的結果頁面。 範例：`page=2` |
| `sort` | 依特定欄位以升序排序結果( **`asc`** )或降序( **`desc`** )順序。 傳回多個結果頁面時，排序參數無法運作。 範例：`sort=updateTime:asc` |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

回應包含 `records` 包含您IMS組織所建立匯出作業的物件。

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
      "imsOrgId": "{ORG_ID}",
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
      "imsOrgId": "{ORG_ID}",
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

若要檢視特定匯出作業的詳細資訊，或在處理時監控其狀態，您可以向 `/export/jobs` 端點和包含 `id` 的URL。 一旦 `status` 欄位返回值「SUCCEEDED」。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 此 `id` 要訪問的導出作業。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `batchId` | 從成功匯出中建立的批次識別碼，用於讀取設定檔資料時的查閱用途。 |

## 取消導出作業

Experience Platform可讓您取消現有的匯出工作，這可能有其用處，原因包括匯出工作未完成或卡在處理階段。 若要取消匯出工作，您可以執行DELETE請求 `/export/jobs` 端點和包含 `id` 的URL。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 此 `id` 要訪問的導出作業。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的刪除請求返回HTTP狀態204（無內容）和空回應正文，表示取消操作成功。

## 後續步驟

匯出成功後，您的資料即可在Data Lake中Experience Platform。 然後，您就可以使用 [資料存取API](https://www.adobe.io/experience-platform-apis/references/data-access/) 若要存取資料，請使用 `batchId` 與匯出相關聯。 視匯出的大小而定，資料可能是區塊，而批次可能包含數個檔案。

如需如何使用資料存取API來存取和下載批次檔案的逐步指示，請遵循 [資料存取教學課程](../../data-access/tutorials/dataset-data.md).

您也可以使用Adobe Experience Platform Query Service存取成功匯出的即時客戶設定檔資料。 Query Service可使用UI或RESTful API，對Data Lake中的資料撰寫、驗證和執行查詢。

如需如何查詢受眾資料的詳細資訊，請檢閱 [查詢服務檔案](../../query-service/home.md).

## 附錄

下節包含有關設定檔API中匯出作業的其他資訊。

### 其他匯出裝載範例

顯示於 [啟動導出作業](#initiate) 建立同時包含設定檔（記錄）和事件（時間系列）資料的作業。 本節提供其他要求裝載範例，以限制您的匯出包含一種或另一種資料類型。

下列裝載會建立僅包含設定檔資料（無事件）的匯出工作：

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

若要建立僅包含事件資料（無設定檔屬性）的匯出工作，裝載可能會如下所示：

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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

您也可以使用匯出作業端點來匯出受眾區段，而非 [!DNL Profile] 資料。 請參閱 [匯出分段API中的工作](../../segmentation/api/export-jobs.md) 以取得更多資訊。
