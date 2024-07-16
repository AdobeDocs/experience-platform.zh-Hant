---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 設定檔匯出作業API端點
type: Documentation
description: 即時客戶個人檔案可讓您結合來自多個來源的資料（包括屬性資料和行為資料），在Adobe Experience Platform中建立個別客戶的單一檢視。 然後，可將設定檔資料匯出至資料集，以供進一步處理。
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: fd5042bee9b09182ac643bcc69482a0a2b3f8faa
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---

# 設定檔匯出作業端點

[!DNL Real-Time Customer Profile]可讓您結合來自多個來源的資料（包括屬性資料和行為資料），以建立個別客戶的單一檢視。 然後，可將設定檔資料匯出至資料集，以供進一步處理。 例如，可透過建立對象來匯出[!DNL Profile]資料以進行啟用，並且可以匯出設定檔屬性以進行報告。

本檔案提供使用[設定檔API](https://www.adobe.com/go/profile-apis-en)建立及管理匯出工作的逐步指示。

>[!NOTE]
>
>本指南涵蓋[!DNL Profile API]中匯出工作的使用。 如需有關如何管理Adobe Experience Platform Segmentation Service之匯出作業的資訊，請參閱Segmentation API](../../profile/api/export-jobs.md)中[匯出作業的指南。

除了建立匯出作業之外，您也可以使用`/entities`端點（也稱為&quot;[!DNL Profile Access]&quot;）存取[!DNL Profile]資料。 如需詳細資訊，請參閱[實體端點指南](./entities.md)。 有關如何使用UI存取[!DNL Profile]資料的步驟，請參閱[使用手冊](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是[!DNL Real-Time Customer Profile] API的一部分。 繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 建立匯出作業

匯出[!DNL Profile]資料需要先建立資料將匯出到的資料集，然後起始新的匯出工作。 這兩個步驟都可以使用Experience PlatformAPI來完成，前者使用目錄服務API，後者使用即時客戶設定檔API。 完成每個步驟的詳細指示在以下各節中概述。

### 建立目標資料集

匯出[!DNL Profile]資料時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

重要考量事項之一是資料集所依據的結構描述（在以下API範例要求中為`schemaRef.id`）。 為了匯出設定檔資料，資料集必須以[!DNL XDM Individual Profile]聯合結構描述(`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合結構描述是系統產生的唯讀結構描述，可彙總共用相同類別的結構描述欄位。 在此案例中，這是[!DNL XDM Individual Profile]類別。 如需聯合檢視結構描述的詳細資訊，請參閱結構描述組合基本概念指南](../../xdm/schema/composition.md#union)中的[聯合區段。

本教學課程後續步驟概述如何使用[!DNL Catalog] API建立參照[!DNL XDM Individual Profile]聯合結構描述的資料集。 您也可以使用[!DNL Platform]使用者介面來建立參考聯合結構描述的資料集。 此UI教學課程匯出對象](../../segmentation/tutorials/create-dataset-export-segment.md)中概述了使用UI的步驟，但也適用於此處。 [完成後，您可以返回此教學課程，繼續進行[起始新匯出工作](#initiate)的步驟。

如果您已有相容的資料集且知道其識別碼，您可以直接進行[起始新匯出工作](#initiate)的步驟。

**API格式**

```http
POST /dataSets
```

**要求**

以下請求會建立新資料集，在承載中提供設定引數。

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
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
| `schemaRef.id` | 與資料集建立關聯的聯合檢視（結構描述）的ID。 |

**回應**

成功的回應會傳回陣列，其中包含新建立資料集的唯讀、系統產生的唯一ID。 需要正確設定的資料集ID才能成功匯出設定檔資料。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 啟動匯出工作 {#initiate}

擁有聯合持續資料集後，您可以建立匯出工作，透過對即時客戶設定檔API中的`/export/jobs`端點發出POST請求並在請求內文中提供您要匯出資料的詳細資訊，將設定檔資料持續存在資料集。

**API格式**

```http
POST /export/jobs
```

**要求**

以下請求會建立新的匯出作業，在承載中提供設定引數。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
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
    },
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
| `fields` | *（選擇性）*&#x200B;將匯出中包含的資料欄位限製為僅包含在此引數中提供的那些欄位。 省略此值將導致所有欄位包含在匯出的資料中。 |
| `mergePolicy` | *（選擇性）*&#x200B;指定合併原則以控管匯出的資料。 如果有多個要匯出的對象，請包含此引數。 |
| `mergePolicy.id` | 合併原則的ID。 |
| `mergePolicy.version` | 要使用的合併原則的特定版本。 省略此值將預設為最新版本。 |
| `additionalFields.eventList` | *（選擇性）*&#x200B;提供下列一或多個設定，控制為子或關聯物件匯出的時間序列事件欄位：<ul><li>`eventList.fields`：控制要匯出的欄位。</li><li>`eventList.filter`：指定限制關聯物件所含結果的條件。 需要匯出所需的最小值，通常是日期。</li><li>`eventList.filter.fromIngestTimestamp`：將時間序列事件篩選為提供的時間戳記之後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）**&#x200B;已匯出資料的目的地資訊：<ul><li>`destination.datasetId`： **（必要）**&#x200B;要匯出資料之資料集的識別碼。</li><li>`destination.segmentPerBatch`： *（選擇性）*&#x200B;布林值，如果未提供，預設值為`false`。 值為`false`會將所有區段定義ID匯出至單一批次ID。 值為`true`會將一個區段定義ID匯出到一個批次ID中。 請注意，將值設定為`true`可能會影響批次匯出效能。</li></ul> |
| `schema.name` | **（必要）**&#x200B;與要匯出資料的資料集相關聯的結構描述名稱。 |

>[!NOTE]
>
>若只要匯出設定檔資料，而不包含相關時間序列資料，請從請求中移除「additionalFields」物件。

**回應**

成功的回應會傳回填入設定檔資料的資料集，如請求中所指定。

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

## 列出所有匯出工作

您可以透過對`export/jobs`端點執行GET要求，傳回特定組織的所有匯出工作清單。 要求也支援查詢引數`limit`和`offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| -------- | ----------- |
| `start` | 根據請求的建立時間，位移傳回結果的頁面。 範例：`start=4` |
| `limit` | 限制傳回的結果數。 範例：`limit=10` |
| `page` | 根據請求的建立時間，傳回結果的特定頁面。 範例：`page=2` |
| `sort` | 依特定欄位以遞增( **`asc`** )或遞減( **`desc`** )順序排序結果。 傳回多個結果頁面時，排序引數無法運作。 範例：`sort=updateTime:asc` |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**回應**

回應包含`records`物件，其中包含貴組織建立的匯出工作。

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

## 監視匯出進度

若要檢視特定匯出作業的詳細資料，或監視其處理狀態，您可以對`/export/jobs`端點發出GET要求，並在路徑中包含匯出作業的`id`。 當`status`欄位傳回「SUCCEEDED」值時，匯出作業即已完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要存取之匯出工作的`id`。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
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
| `batchId` | 成功匯出後建立的批次識別碼，在讀取設定檔資料時用於查詢。 |

## 取消匯出工作

Experience Platform可讓您取消現有的匯出作業，這可能是由於許多原因所造成，包括匯出作業未完成或卡在處理階段中。 若要取消匯出作業，您可以對`/export/jobs`端點執行DELETE要求，並將您要取消的匯出作業`id`納入要求路徑。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要存取之匯出工作的`id`。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的刪除請求會傳回HTTP狀態204 （無內容）和空白的回應內文，指出取消作業成功。

## 後續步驟

成功完成匯出後，您的資料就可以在Experience Platform的資料湖中使用。 然後，您就可以使用[資料存取API](https://www.adobe.io/experience-platform-apis/references/data-access/)，使用與匯出相關聯的`batchId`存取資料。 視匯出大小而定，資料可能會以區塊為單位，而批次可能包含數個檔案。

如需如何使用資料存取API來存取及下載批次檔案的逐步指示，請遵循[資料存取教學課程](../../data-access/tutorials/dataset-data.md)。

您也可以使用Adobe Experience Platform查詢服務存取成功匯出的即時客戶設定檔資料。 查詢服務可讓您使用UI或RESTful API，針對Data Lake內的資料寫入、驗證及執行查詢。

如需有關如何查詢對象資料的詳細資訊，請檢閱[查詢服務檔案](../../query-service/home.md)。

## 附錄

下節包含有關設定檔API中匯出作業的其他資訊。

### 其他匯出裝載範例

在[起始匯出工作](#initiate)的區段中顯示的範例API呼叫會建立同時包含設定檔（記錄）和事件（時間序列）資料的工作。 本節提供其他請求裝載範例，將匯出限製為包含一種資料型別或另一種資料型別。

以下裝載會建立僅包含設定檔資料（無事件）的匯出作業：

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

若要建立僅包含事件資料（無設定檔屬性）的匯出作業，裝載可能會如下所示：

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

### 匯出對象

您也可以使用匯出作業端點來匯出對象，而非[!DNL Profile]資料。 如需詳細資訊，請參閱分段API](../../segmentation/api/export-jobs.md)中[匯出作業的指南。
