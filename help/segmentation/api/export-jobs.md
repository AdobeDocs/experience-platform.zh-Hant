---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；匯出工作；api;
solution: Experience Platform
title: 區段匯出作業API端點
description: 匯出工作是非同步程式，可用來將對象區段成員保留至資料集。 您可以在Adobe Experience Platform分段服務API中使用/export/jobs端點，這可讓您以程式設計方式擷取、建立和取消匯出工作。
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: d28cebaf4b9fe5c35240e28653e99424db08d9d2
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 2%

---

# 區段匯出作業端點

匯出工作是非同步程式，可用來將對象區段成員保留至資料集。 您可以使用 `/export/jobs` Adobe Experience Platform分段API中的端點，可讓您以程式設計方式擷取、建立和取消匯出工作。

>[!NOTE]
>
>本指南涵蓋在 [!DNL Segmentation API]. 有關如何管理的導出作業的資訊 [!DNL Real-Time Customer Profile] 資料，請參閱 [匯出設定檔API中的工作](../../profile/api/export-jobs.md)

## 快速入門

本指南中使用的端點屬於 [!DNL Adobe Experience Platform Segmentation Service] API。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 檢索導出作業清單 {#retrieve-list}

您可以向 `/export/jobs` 端點。

**API格式**

此 `/export/jobs` 端點支援數個查詢參數，可協助篩選結果。 雖然這些參數為可選參數，但強烈建議使用這些參數，以幫助降低昂貴的開銷。 對此端點發出呼叫（沒有參數）將檢索組織可用的所有導出作業。 可包含多個參數，以&amp;符號分隔(`&`)。

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | 指定傳回的匯出作業數。 |
| `{OFFSET}` | 指定結果頁的偏移。 |
| `{STATUS}` | 根據狀態篩選結果。 支援的值為「NEW」、「SUCCEEDED」和「FAILED」。 |

**要求**

下列請求會擷取您IMS組織內最後兩個匯出工作。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據請求路徑中提供的查詢參數，傳回HTTP狀態200，並列出已成功完成的匯出作業。

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `destination` | 匯出資料的目的地資訊：<ul><li>`datasetId`:匯出資料的資料集ID。</li><li>`segmentPerBatch`:顯示區段ID是否已整合的布林值。 值「false」表示所有區段ID都會匯出為單一批次ID。 值「true」表示會將一個區段ID匯出為一個批次ID。 **注意：** 將值設定為true可能會影響批導出效能。</li></ul> |
| `fields` | 匯出欄位的清單，以逗號分隔。 |
| `schema.name` | 與要匯出資料的資料集相關聯的結構名稱。 |
| `filter.segments` | 匯出的區段。 包含下列欄位：<ul><li>`segmentId`:要匯出設定檔的區段ID。</li><li>`segmentNs`:指定的區段命名空間 `segmentID`.</li><li>`status`:字串陣列，提供 `segmentID`. 依預設， `status` 將具有值 `["realized"]` 代表目前時間屬於區段的所有設定檔。 可能的值包括： `realized` 和 `exited`. 值 `realized` 表示設定檔符合區段資格。 值 `exiting` 表示設定檔正在退出區段。</li></ul> |
| `mergePolicy` | 合併導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，用於指示導出作業運行所花費的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指出匯出設定檔所花的時間。 |
| `page` | 請求的導出作業的分頁資訊。 |
| `link.next` | 導出作業的下一頁的連結。 |

## 建立新的導出作業 {#create}

您可以向 `/export/jobs` 端點。

**API格式**

```http
POST /export/jobs
```

**要求**

下列請求會建立新的匯出工作，由裝載中提供的參數所設定。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `fields` | 匯出欄位的清單，以逗號分隔。 若保留為空白，則會匯出所有欄位。 |
| `mergePolicy` | 指定用於管理導出資料的合併策略。 有多個要匯出的區段時，請加入此參數。 如果未提供，則導出將採用與給定段相同的合併策略。 |
| `filter` | 一個物件，根據下列子屬性，依ID、資格時間或擷取時間指定要包含在匯出工作中的區段。 若保留為空白，則會匯出所有資料。 |
| `filter.segments` | 指定要匯出的區段。 省略此值會導致所有設定檔的所有資料都匯出。 接受區段物件的陣列，每個物件都包含下列欄位：<ul><li>`segmentId`: **(若使用 `segments`)** 要匯出之設定檔的區段ID。</li><li>`segmentNs` *（可選）* 指定的區段命名空間 `segmentID`.</li><li>`status` *（可選）* 字串陣列，提供 `segmentID`. 依預設， `status` 將具有值 `["realized"]` 代表目前時間屬於區段的所有設定檔。 可能的值包括： `realized` 和 `exited`.  值 `realized` 表示設定檔符合區段資格。 值 `exiting` 表示設定檔正在退出區段。</li></ul> |
| `filter.segmentQualificationTime` | 根據區段資格時間進行篩選。 可以提供開始時間和/或結束時間。 |
| `filter.segmentQualificationTime.startTime` | 指定狀態之區段ID的區段資格開始時間。 若未提供，則不會對區段ID資格的開始時間進行篩選。 時間戳記必須提供於 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 |
| `filter.segmentQualificationTime.endTime` | 指定狀態之區段ID的區段資格結束時間。 若未提供，則不會針對區段ID資格的結束時間進行篩選。 時間戳記必須提供於 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 |
| `filter.fromIngestTimestamp ` | 將匯出的設定檔限制為僅包含在此時間戳記之後更新的設定檔。 時間戳記必須提供於 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式。 <ul><li>`fromIngestTimestamp` for **設定檔**，若提供：包含所有合併的設定檔，其中合併的更新時間戳記大於指定的時間戳記。 支援 `greater_than` 操作數。</li><li>`fromIngestTimestamp` for **事件**:在此時間戳記之後擷取的所有事件都會匯出為與產生的設定檔結果對應。 這不是事件時間本身，而是事件的擷取時間。</li> |
| `filter.emptyProfiles` | 指出是否要篩選空設定檔的布林值。 設定檔可包含設定檔記錄、ExperienceEvent記錄或兩者。 沒有設定檔記錄且只有ExperienceEvent記錄的設定檔稱為「emptyProfiles」。 若要匯出設定檔存放區中的所有設定檔，包括&quot;emptyProfiles&quot;，請設定 `emptyProfiles` to `true`. 若 `emptyProfiles` 設為 `false`，只會匯出儲存中具有設定檔記錄的設定檔。 依預設，若 `emptyProfiles` 屬性，則只會匯出包含設定檔記錄的設定檔。 |
| `additionalFields.eventList` | 通過提供以下一個或多個設定，控制為子對象或關聯對象導出的時間序列事件欄位：<ul><li>`fields`:控制要匯出的欄位。</li><li>`filter`:指定用於限制從關聯對象中包括的結果的標準。 預期匯出所需的最小值，通常為日期。</li><li>`filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳記之後擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li><li>`filter.toIngestTimestamp`:將時間戳記篩選為在提供的時間戳記之前擷取的時間戳記。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）** 匯出資料的相關資訊：<ul><li>`datasetId`: **（必要）** 要匯出資料的資料集ID。</li><li>`segmentPerBatch`: *（可選）* 布林值（若未提供）預設為&quot;false&quot;。 值「false」會將所有區段ID匯出為單一批次ID。 值「true」會將一個區段ID匯出為一個批次ID。 請注意，將值設為「true」可能會影響批次匯出效能。</li></ul> |
| `schema.name` | **（必要）** 與要匯出資料的資料集相關聯的結構名稱。 |
| `evaluationInfo.segmentation` | *（可選）* 布林值（若未提供），預設為 `false`. 值 `true` 指出需要在匯出工作上執行分段。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之匯出工作的詳細資訊。

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統生成的只讀值，用於標識剛建立的導出作業。 |

或者，如果 `destination.segmentPerBatch` 已設為 `true`, `destination` 上方的物件會 `batches` 陣列，如下所示：

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## 檢索特定導出作業 {#get}

您可以向 `/export/jobs` 端點，並提供您要在請求路徑中擷取之匯出作業的ID。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 此 `id` 要訪問的導出作業。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定匯出工作的詳細資訊。

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `destination` | 匯出資料的目的地資訊：<ul><li>`datasetId`:匯出資料的資料集ID。</li><li>`segmentPerBatch`:顯示區段ID是否已整合的布林值。 值 `false` 表示所有區段ID都整合為單一批次ID。 值 `true` 表示會將一個區段ID匯出為一個批次ID。</li></ul> |
| `fields` | 匯出欄位的清單，以逗號分隔。 |
| `schema.name` | 與要匯出資料的資料集相關聯的結構名稱。 |
| `filter.segments` | 匯出的區段。 包含下列欄位：<ul><li>`segmentId`:要匯出之設定檔的區段ID。</li><li>`segmentNs`:指定的區段命名空間 `segmentID`.</li><li>`status`:字串陣列，提供 `segmentID`. 依預設， `status` 將具有值 `["realized"]` 代表目前時間屬於區段的所有設定檔。 可能的值包括： `realized` 和 `exited`.  值 `realized` 表示設定檔符合區段資格。 值 `exiting` 表示設定檔正在退出區段。</li></ul> |
| `mergePolicy` | 合併導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，用於指示導出作業運行所花費的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指出匯出設定檔所花的時間。 |
| `totalExportedProfileCounter` | 所有批中導出的配置檔案總數。 |

## 取消或刪除特定的導出作業 {#delete}

您可以向發出DELETE請求，以請求刪除指定的匯出作業 `/export/jobs` 端點，並提供您要在請求路徑中刪除之匯出作業的ID。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 此 `id` 刪除的導出作業。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204，並顯示下列訊息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 後續步驟

閱讀本指南後，您現在對匯出工作的運作方式有了更深入的了解。
