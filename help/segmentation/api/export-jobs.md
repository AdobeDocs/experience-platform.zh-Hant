---
solution: Experience Platform
title: 區段匯出作業API端點
description: 匯出作業是用來將受眾區段成員保留至資料集的非同步程式。 您可以使用Adobe Experience Platform Segmentation Service API中的/export/jobs端點，以程式設計方式擷取、建立和取消匯出作業。
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# 區段匯出作業端點

匯出作業是用來將受眾區段成員保留至資料集的非同步程式。 您可以使用Adobe Experience Platform Segmentation API中的`/export/jobs`端點，以程式設計方式擷取、建立和取消匯出作業。

>[!NOTE]
>
>本指南涵蓋[!DNL Segmentation API]中匯出工作的使用。 如需有關如何管理[!DNL Real-Time Customer Profile]資料之匯出工作的資訊，請參閱設定檔API[&#128279;](../../profile/api/export-jobs.md)中匯出工作的指南

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

## 擷取匯出作業清單 {#retrieve-list}

您可以對`/export/jobs`端點發出GET要求，以擷取組織的所有匯出工作清單。

**API格式**

`/export/jobs`端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數來協助減少昂貴的額外負荷。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有匯出作業。 可以包含多個引數，以&amp;符號(`&`)分隔。

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**查詢引數**

+++ 可用查詢引數的清單。

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `limit` | 指定傳回的匯出工作數目。 | `limit=10` |
| `offset` | 指定結果頁面的位移。 | `offset=1540974701302_96` |
| `status` | 根據狀態篩選結果。 支援的值為「NEW」、「SUCCEEDED」和「FAILED」。 | `status=NEW` |

+++

**要求**

下列請求將會擷取組織內最後兩個匯出工作。

+++ 擷取匯出作業的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

下列回應會根據請求路徑中提供的查詢引數，傳回HTTP狀態200，其中包含已成功完成的匯出作業清單。

+++ 擷取匯出作業時的範例回應。

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
| `destination` | 已匯出資料的目的地資訊：<ul><li>`datasetId`：資料匯出所在資料集的識別碼。</li><li>`segmentPerBatch`：顯示是否合併區段ID的布林值。 「false」值表示所有區段ID都會匯出至單一批次ID。 值為「true」表示會將一個區段ID匯出至一個批次ID。 **注意：**&#x200B;將值設定為True可能會影響批次匯出效能。</li></ul> |
| `fields` | 匯出的欄位清單，以逗號分隔。 |
| `schema.name` | 與要匯出資料的資料集相關聯的結構描述名稱。 |
| `filter.segments` | 匯出的區段。 包括下列欄位：<ul><li>`segmentId`：要匯出設定檔的目的地區段ID。</li><li>`segmentNs`：指定`segmentID`的區段名稱空間。</li><li>`status`：為`segmentID`提供狀態篩選的字串陣列。 根據預設，`status`的值將為`["realized"]`，該值代表目前屬於該區段的所有設定檔。 可能的值包括： `realized`和`exited`。 值為`realized`表示設定檔符合區段的資格。 值`exiting`表示設定檔正在退出區段。</li></ul> |
| `mergePolicy` | 合併已匯出資料的原則資訊。 |
| `metrics.totalTime` | 表示執行匯出作業所花費總時間的欄位。 |
| `metrics.profileExportTime` | 表示設定檔匯出所需時間的欄位。 |
| `page` | 請求之匯出作業分頁的相關資訊。 |
| `link.next` | 匯出作業下一頁的連結。 |

+++

## 建立新的匯出工作 {#create}

您可以對`/export/jobs`端點發出POST要求，以建立新的匯出作業。

**API格式**

```http
POST /export/jobs
```

**要求**

以下請求會建立新的匯出作業，並依據承載中提供的引數加以設定。

+++ 建立匯出作業的範例請求。

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
| `fields` | 匯出的欄位清單，以逗號分隔。 如果保留為空白，則會匯出所有欄位。 |
| `mergePolicy` | 指定合併原則以控管匯出的資料。 匯出多個區段時包含此引數。 如果未提供，匯出將會採用與指定區段相同的合併原則。 |
| `filter` | 此物件會根據下列子屬性來指定要依據ID、資格時間或擷取時間包含在匯出作業中的區段。 如果保留為空白，將會匯出所有資料。 |
| `filter.segments` | 指定要匯出的區段。 省略此值將導致所有設定檔中的所有資料被匯出。 接受區段物件的陣列，每個物件包含下列欄位：<ul><li>`segmentId`： **（若使用要匯出的設定檔的`segments`）**&#x200B;區段識別碼，則為必要。</li><li>`segmentNs` *（選擇性）*&#x200B;給定`segmentID`的區段名稱空間。</li><li>`status` *（選擇性）*&#x200B;為`segmentID`提供狀態篩選器的字串陣列。 根據預設，`status`的值將為`["realized"]`，該值代表目前屬於該區段的所有設定檔。 可能的值包括： `realized`和`exited`。  值為`realized`表示設定檔符合區段的資格。 值`exiting`表示設定檔正在退出區段。</li></ul> |
| `filter.segmentQualificationTime` | 根據區段資格時間進行篩選。 可提供開始時間及/或結束時間。 |
| `filter.segmentQualificationTime.startTime` | 指定狀態的區段ID的區段資格開始時間。 若未提供，區段ID資格的開始時間將沒有篩選器。 時間戳記必須以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 |
| `filter.segmentQualificationTime.endTime` | 指定狀態的區段ID的區段資格結束時間。 若未提供，區段ID資格的結束時間將沒有篩選器。 時間戳記必須以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 |
| `filter.fromIngestTimestamp ` | 限制匯出的設定檔，以僅包含在此時間戳記之後更新的設定檔。 時間戳記必須以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式提供。 <ul><li>**個設定檔**&#x200B;的`fromIngestTimestamp` （如果提供）：包含合併更新時間戳記大於指定時間戳記的所有合併設定檔。 支援`greater_than`運算元。</li><li>**個事件**&#x200B;的`fromIngestTimestamp`：在此時間戳記之後擷取的所有事件，都會匯出為對應的結果設定檔結果。 這不是事件時間本身，而是事件的擷取時間。</li> |
| `filter.emptyProfiles` | 布林值，指示是否篩選空白設定檔。 設定檔可包含設定檔記錄、ExperienceEvent記錄，或同時包含兩者。 沒有設定檔記錄且只有ExperienceEvent記錄的設定檔稱為「emptyProfiles」。 若要匯出設定檔存放區中的所有設定檔，包括「emptyProfiles」，請將`emptyProfiles`的值設定為`true`。 如果`emptyProfiles`設為`false`，則只會匯出存放區中具有設定檔記錄的設定檔。 根據預設，如果未包含`emptyProfiles`屬性，則只會匯出包含設定檔記錄的設定檔。 |
| `additionalFields.eventList` | 提供下列一或多個設定，控制為子或關聯物件匯出的時間序列事件欄位：<ul><li>`fields`：控制要匯出的欄位。</li><li>`filter`：指定限制關聯物件所含結果的條件。 需要匯出所需的最小值，通常是日期。</li><li>`filter.fromIngestTimestamp`：將時間序列事件篩選為提供的時間戳記之後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li><li>`filter.toIngestTimestamp`：將時間戳記篩選為提供的時間戳記之前所擷取的日期。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）**&#x200B;有關匯出資料的資訊：<ul><li>`datasetId`： **（必要）**&#x200B;要匯出資料之資料集的識別碼。</li><li>`segmentPerBatch`： *（選擇性）*&#x200B;布林值，若未提供，預設值為「false」。 若值為「false」，則會將所有區段ID匯出至單一批次ID。 若值為「true」，會將一個區段ID匯出為一個批次ID。 請注意，將該值設為「true」可能會影響批次匯出效能。</li></ul> |
| `schema.name` | **（必要）**&#x200B;與要匯出資料的資料集相關聯的結構描述名稱。 |
| `evaluationInfo.segmentation` | *（選擇性）*&#x200B;布林值，若未提供，預設值為`false`。 值為`true`表示需要對匯出作業執行分段。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及您新建立的匯出工作的詳細資訊。

+++ 建立匯出作業時的範例回應。

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
| `id` | 系統產生的唯讀值，用於識別剛建立的匯出作業。 |

或者，如果`destination.segmentPerBatch`已設定為`true`，則上述`destination`物件將具有`batches`陣列，如下所示：

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

+++

## 擷取特定匯出作業 {#get}

您可以向`/export/jobs`端點發出GET要求，並在要求路徑中提供您要擷取之匯出作業的識別碼，以擷取特定匯出作業的詳細資訊。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要存取之匯出工作的`id`。 |

**要求**

+++ 擷取匯出作業的範例請求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定匯出工作的詳細資訊。

+++ 擷取匯出作業時的範例回應。

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
| `destination` | 已匯出資料的目的地資訊：<ul><li>`datasetId`：資料匯出所在資料集的識別碼。</li><li>`segmentPerBatch`：顯示是否合併區段ID的布林值。 值為`false`表示所有區段ID都放入單一批次ID中。 值為`true`表示一個區段ID會匯出到一個批次ID。</li></ul> |
| `fields` | 匯出的欄位清單，以逗號分隔。 |
| `schema.name` | 與要匯出資料的資料集相關聯的結構描述名稱。 |
| `filter.segments` | 匯出的區段。 包括下列欄位：<ul><li>`segmentId`：要匯出的設定檔的區段識別碼。</li><li>`segmentNs`：指定`segmentID`的區段名稱空間。</li><li>`status`：為`segmentID`提供狀態篩選的字串陣列。 根據預設，`status`的值將為`["realized"]`，該值代表目前屬於該區段的所有設定檔。 可能的值包括： `realized`和`exited`。  值為`realized`表示設定檔符合區段的資格。 值`exiting`表示設定檔正在退出區段。</li></ul> |
| `mergePolicy` | 合併已匯出資料的原則資訊。 |
| `metrics.totalTime` | 表示執行匯出作業所花費總時間的欄位。 |
| `metrics.profileExportTime` | 表示設定檔匯出所需時間的欄位。 |
| `totalExportedProfileCounter` | 跨所有批次匯出的設定檔總數。 |

+++

## 取消或刪除特定匯出工作 {#delete}

您可以向`/export/jobs`端點發出DELETE要求，並在要求路徑中提供您要刪除之匯出作業的識別碼，以要求刪除指定的匯出作業。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 您要刪除之匯出工作的`id`。 |

**要求**

+++ 刪除匯出作業的範例請求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態204，並出現以下訊息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 後續步驟

閱讀本指南後，您現在已能更清楚瞭解匯出工作的運作方式。
