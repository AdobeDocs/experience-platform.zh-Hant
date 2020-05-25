---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API匯出資料
topic: tutorial
translation-type: tm+mt
source-git-commit: d0b9223aebca0dc510a7457e5a5c65ac4a567933
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---


# 使用API匯出描述檔資料

即時客戶個人檔案可讓您將來自多個來源的資料（包括屬性資料和行為資料）整合在一起，以建立個別客戶的單一檢視。 然後，可將描述檔中的可用資料匯出至資料集，以進一步處理。 本教學課程提供使用區段API來建立和管理匯出工作的逐 [步指示](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

除了建立匯出工作，您也可以使用描述檔存取API並透過預測來存取描述檔資料。 如需這些其 [他存取模式的詳細資訊，請參閱「描述檔存](../../profile/api/entities.md) 取API」教學課程 [，或](../../profile/api/edge-projections.md) 是設定邊緣目的地和預測的教學課程。

## 快速入門

本教學課程需要對使用描述檔資料時涉及的各種Adobe Experience Platform服務有正確的認識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [即時客戶個人檔案](../../profile/home.md): 根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
- [Adobe Experience Platform細分服務](../home.md): 可讓您從即時客戶個人檔案資料建立受眾細分。
- [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
- [沙盒](../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 必要的標題

本教學課程也要求您完成驗證教 [學課程](../../tutorials/authentication.md) ，才能成功呼叫平台API。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 對平台API的請求需要一個標題，該標題指定要在中執行操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要附加標題：

- 內容類型： application/json

## 建立匯出工作

匯出描述檔資料需要先建立資料要匯出到的資料集，然後開始新的匯出工作。 這兩個步驟都可使用Experience Platform API來完成，前者使用Catalog Service API，後者則使用即時客戶設定檔API。 以下各節將列出完成每個步驟的詳細說明。

- [建立目標資料集](#create-a-target-dataset) -建立資料集以儲存匯出的資料。
- [啟動新的匯出工作](#initiate-export-job) -將XDM個別描述檔資料填入資料集。

### 建立目標資料集

匯出描述檔資料時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構(在下`schemaRef.id` 面的API範例請求中)。 若要匯出區段，資料集必須以XDM個別描述檔結合架構(`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合共用相同類的模式的欄位（在本例中為XDM Individual Profile類）。 有關聯合視圖方案的詳細資訊，請參閱 [方案註冊開發人員指南的「即時客戶概要檔案」部分](../../xdm/schema/composition.md#union)。

本教學課程中的後續步驟概述如何使用目錄API建立參照XDM個別描述檔結合架構的資料集。 您也可以使用Adobe Experience Platform使用者介面來建立參照聯合架構的資料集。 使用UI的步驟在本UI教學課程中 [列出，可匯出區段](./create-dataset-export-segment.md) ，但也適用於此處。 完成後，您可以返回本教學課程，繼續啟動新 [導出作業的步驟](#initiate-export-job)。

如果您已擁有相容的資料集並知道其ID，則可直接執行開始新匯 [出工作的步驟](#initiate-export-job)。

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

### 啟始匯出工作

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `fields` | *（可選）* ，將要包含在導出中的資料欄位限制為僅限此參數中提供的資料欄位。 建立區段時也可使用相同的參數，因此區段中的欄位可能已經過篩選。 省略此值會導致所有欄位都包含在匯出的資料中。 |
| `mergePolicy` | *（可選）* 指定用於管理導出資料的合併策略。 當有多個區段要匯出時，請加入此參數。 省略此值將導致Export Service使用區段提供的合併原則。 |
| `mergePolicy.id` | 合併策略的ID。 |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 省略此值將預設為最新版本。 |
| `filter` | *（可選）* 指定在匯出前套用至區段的下列一或多個篩選。 |
| `filter.segments` | *（選用）* ，指定要匯出的區段。 省略此值將導致導出所有配置檔案中的所有資料。 接受區段物件的陣列，每個物件都包含下列欄位：<ul><li>`segmentId`: **（若使用）`segments`** 「區段ID」，則需要匯出描述檔。</li><li>`segmentNs` *（可選）* ，指定的區段名稱空間 `segmentID`。</li><li>`status` *（可選）* ，提供狀態篩選的字串陣列 `segmentID`。 依預設， `status` 將會有值， `["realized", "existing"]` 代表目前時段屬於區段的所有描述檔。 可能的值包括： `"realized"`、 `"existing"`和 `"exited"`。</br></br>如需詳細資訊，請參閱「建立 [區段」教學課程](./create-a-segment.md)。</li></ul> |
| `filter.segmentQualificationTime` | *（選用）* ，根據區段限定時間篩選。 可以提供開始時間和／或結束時間。 |
| `filter.segmentQualificationTime.startTime` | *（可選）* ，指定狀態之區段ID的區段資格開始時間。 未提供，區段ID資格的開始時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.segmentQualificationTime.endTime` | *（可選）* ，指定狀態之區段ID的區段資格結束時間。 未提供，區段ID資格的結束時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp ` | *（可選）* 「限制」匯出的描述檔僅包含在此時間戳記後更新的描述檔。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 <ul><li>`fromIngestTimestamp` 如果 **提供**，則適用於描述檔： 包含所有合併的描述檔，其中合併的更新時間戳記大於指定的時間戳記。 支援操 `greater_than` 作數。</li><li>`fromTimestamp` 對於 **事件**: 在此時間戳記之後收錄的所有事件都會匯出，以對應於產生的描述檔結果。 這不是事件時間本身，而是事件的擷取時間。</li> |
| `filter.emptyProfiles` | *（可選）* Boolean。 設定檔可以包含設定檔記錄、ExperienceEvent記錄或兩者。 沒有設定檔記錄且只有ExperienceEvent記錄的設定檔稱為「emptyProfiles」。 要導出配置檔案儲存中的所有配置檔案，包括「emptyProfiles」，請將值設 `emptyProfiles` 置為 `true`。 如果 `emptyProfiles` 設定為， `false`則只導出儲存中具有配置檔案記錄的配置檔案。 預設情況下，如果不包 `emptyProfiles` 含屬性，則僅導出包含配置檔案記錄的配置檔案。 |
| `additionalFields.eventList` | *（可選）* ，通過提供以下一個或多個設定來控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`eventList.fields`: 控制要匯出的欄位。</li><li>`eventList.filter`: 指定限制關聯對象所包含結果的標準。 預期匯出所需的最低值，通常為日期。</li><li>`eventList.filter.fromIngestTimestamp`: 將時間系列事件篩選為在提供時間戳記後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）** ，匯出資料的目標資訊：<ul><li>`destination.datasetId`: **（必要）** ，要匯出資料的資料集ID。</li><li>`destination.segmentPerBatch`: *（可選）* ，一個布爾值，如果未提供，則預設為 `false`。 值將所有 `false` 區段ID匯出為單一批次ID。 值將一個 `true` 區段ID匯出為一個批次ID。 請注意，將值設定為可能 `true` 會影響批導出效能。</li></ul> |
| `schema.name` | **（必要）** ，與要匯出資料的資料集關聯的架構名稱。 |
| `evaluationInfo.segmentation` | *（選用）* ，若未提供，則預設為布林值 `false`。 值表示 `true` 需要在匯出工作上執行分段。 |

>[!NOTE] 若要僅匯出描述檔資料，而不要包含相關的ExperienceEvent資料，請從請求中移除「additionalFields」物件。

**回應**

成功的回應會傳回填入「描述檔」資料的資料集，如請求中所指定。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

如 `destination.segmentPerBatch` 果請求中未包含(如果不存在，則預設為 `false`)或值已設為 `false`，則上述回應中的物件將不會包含陣列，而只會包含一個 `destination``batches``batchId`，如下所示。 該單一批次會包含所有區段ID，而上述回應則會針對每個批次ID顯示單一區段ID。

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## 列出所有匯出工作

您可以執行GET請求至端點，傳回特定IMS組織所有匯出工作的清 `export/jobs` 單。 請求也支援查詢參 `limit` 數 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 屬性 | 說明 |
| -------- | ----------- |
| `limit` | 指定要傳回的記錄數。 |
| `offset` | 將要傳回的結果頁面偏移所提供的數字。 |

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
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

| 屬性 | 說明 |
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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

| 屬性 | 說明 |
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