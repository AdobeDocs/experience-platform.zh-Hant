---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 導出作業端點
topic: developer guide
translation-type: tm+mt
source-git-commit: 6ddb420ad3c4df3096dac456c58afc7a4916ce51
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---


# 導出作業端點

匯出工作是非同步程式，用來將讀者區段成員持續存留至資料集。 您可以使用 `/export/jobs` Adobe Experience Platform Segmentation API中的端點，此端點可讓您以程式設計方式擷取、建立和取消匯出工作。

>[!NOTE]
>
>本指南涵蓋在中使用匯出工作 [!DNL Segmentation API]。 如需如何管理資料匯出工作的詳細 [!DNL Real-time Customer Profile] 資訊，請參閱描述檔API [中的匯出工作指南](../../profile/api/export-jobs.md)

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請先檢閱 [快速入門手冊](./getting-started.md) ，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 檢索導出作業清單 {#retrieve-list}

您可以向端點提出GET請求，以擷取IMS組織所有匯出工作的清 `/export/jobs` 單。

**API格式**

端點 `/export/jobs` 支援數個查詢參數，以協助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們，以幫助降低昂貴的開銷。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的匯出工作。 可包含多個參數，由&amp;符號(`&`)分隔。

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | 指定傳回的匯出工作數。 |
| `{OFFSET}` | 指定結果頁的偏移。 |
| `{STATUS}` | 根據狀態篩選結果。 支援的值為「NEW」、「SUCCEEDED」和「FAILED」。 |

**請求**

下列請求將擷取您IMS組織中最後兩個匯出工作。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據請求路徑中提供的查詢參數，傳回HTTP狀態200，並列出成功完成的匯出工作。

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
                        "status": ["realized", "existing"]
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
| `destination` | 匯出資料的目標資訊：<ul><li>`datasetId`:匯出資料的資料集的ID。</li><li>`segmentPerBatch`:顯示區段ID是否整合的布林值。 值「false」表示所有區段ID都會匯出為單一批次ID。 值&quot;true&quot;表示將一個區段ID匯出為一個批次ID。 **注意：** 將值設為true可能會影響批次匯出效能。</li></ul> |
| `fields` | 匯出欄位的清單，以逗號分隔。 |
| `schema.name` | 與要導出資料的資料集關聯的方案的名稱。 |
| `filter.segments` | 匯出的區段。 包含下列欄位：<ul><li>`segmentId`:將描述檔匯出至的區段ID。</li><li>`segmentNs`:指定的區段名稱空間 `segmentID`。</li><li>`status`:為提供狀態過濾器的字串陣列 `segmentID`。 依預設， `status` 將會有值， `["realized", "existing"]` 代表目前時段屬於區段的所有描述檔。 可能的值包括：「已實現」、「現有」和「已退出」。</li></ul> |
| `mergePolicy` | 合併已導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，指示導出作業所用的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指示導出配置檔案所花費的時間。 |
| `page` | 請求匯出工作的編頁資訊。 |
| `link.next` | 匯出工作下一頁的連結。 |

## 建立新的匯出工作 {#create}

您可以通過向端點發出POST請求來建立新的導出 `/export/jobs` 作業。

**API格式**

```http
POST /export/jobs
```

**請求**

下列請求會建立新的匯出工作，由裝載中提供的參數設定。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `fields` | 匯出欄位的清單，以逗號分隔。 如果保留為空白，則將導出所有欄位。 |
| `mergePolicy` | 指定用於管理導出資料的合併策略。 當有多個區段要匯出時，請加入此參數。 如果未提供，則匯出會採用與指定區段相同的合併政策。 |
| `filter` | 指定將依ID、資格時間或收錄時間納入匯出工作的區段的物件，視下列子屬性而定。 如果保留為空白，則將導出所有資料。 |
| `filter.segments` | 指定要匯出的區段。 省略此值將導致導出所有配置檔案中的所有資料。 接受區段物件的陣列，每個物件都包含下列欄位：<ul><li>`segmentId`: **（若使用）`segments`** 「區段ID」，則需要匯出描述檔。</li><li>`segmentNs` *（可選）* ，指定的區段名稱空間 `segmentID`。</li><li>`status` *（可選）* ，提供狀態篩選的字串陣列 `segmentID`。 依預設， `status` 將會有值， `["realized", "existing"]` 代表目前時段屬於區段的所有描述檔。 Possible values include: `"realized"`, `"existing"`, and `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | 根據區段限定時間進行篩選。 可以提供開始時間和／或結束時間。 |
| `filter.segmentQualificationTime.startTime` | 指定狀態之區段ID的區段資格開始時間。 未提供，區段ID資格的開始時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.segmentQualificationTime.endTime` | 指定狀態之區段ID的區段資格結束時間。 未提供，區段ID資格的結束時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp ` | 限制匯出的描述檔僅包含在此時間戳記後更新的描述檔。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 <ul><li>`fromIngestTimestamp` 如果 **提供**，則適用於描述檔：包含所有合併的描述檔，其中合併的更新時間戳記大於指定的時間戳記。 支援操 `greater_than` 作數。</li><li>`fromIngestTimestamp` 對於 **事件**:在此時間戳記之後收錄的所有事件都會匯出，以對應於產生的描述檔結果。 這不是事件時間本身，而是事件的擷取時間。</li> |
| `filter.emptyProfiles` | 指示是否篩選空配置檔案的布爾值。 設定檔可以包含設定檔記錄、ExperienceEvent記錄或兩者。 沒有設定檔記錄且只有ExperienceEvent記錄的設定檔稱為「emptyProfiles」。 要導出配置檔案儲存中的所有配置檔案，包括「emptyProfiles」，請將值設 `emptyProfiles` 置為 `true`。 如果 `emptyProfiles` 設定為 `false`，則只導出儲存中具有配置檔案記錄的配置檔案。 預設情況下，如果不 `emptyProfiles` 包括屬性，則僅導出包含配置檔案記錄的配置檔案。 |
| `additionalFields.eventList` | 通過提供以下一個或多個設定，控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`fields`:控制要匯出的欄位。</li><li>`filter`:指定限制關聯對象所包含結果的標準。 預期匯出所需的最低值，通常為日期。</li><li>`filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳記後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。</li><li>`filter.toIngestTimestamp`:將時間戳記篩選為在提供時間戳記之前已收錄的時間戳記。 這不是事件時間本身，而是事件的擷取時間。</li></ul> |
| `destination` | **（必要）** ，匯出資料的相關資訊：<ul><li>`datasetId`: **（必要）** ，要匯出資料的資料集ID。</li><li>`segmentPerBatch`: *（選用）* ，若未提供，則預設為&quot;false&quot;的布林值。 值「false」會將所有區段ID匯出為單一批次ID。 值&quot;true&quot;會將一個區段ID匯出為一個批次ID。 請注意，將值設為&quot;true&quot;可能會影響批次匯出效能。</li></ul> |
| `schema.name` | **（必要）** ，與要匯出資料的資料集關聯的架構名稱。 |
| `evaluationInfo.segmentation` | *（選用）* ，若未提供，則預設為布林值 `false`。 值表示 `true` 需要在匯出工作上執行分段。 |

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
    "imsOrgId": "{IMS_ORG}",
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
| `id` | 系統生成的唯讀值，用於標識剛建立的導出作業。 |

或者，如 `destination.segmentPerBatch` 果已設為 `true`，則上 `destination` 述物件會有一個陣列，如 `batches` 下所示：

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
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

## 擷取特定匯出工作 {#get}

通過向端點發出GET請求，並在請求路徑中提供要檢索的導出作業的ID，可以檢索有關特定導出作業的詳細資訊。 `/export/jobs`

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 您 `id` 要存取的匯出工作。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定匯出工作的詳細資訊。

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
    "imsOrgId": "{IMS_ORG}",
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
| `destination` | 匯出資料的目標資訊：<ul><li>`datasetId`:匯出資料的資料集ID。</li><li>`segmentPerBatch`:顯示區段ID是否整合的布林值。 值表示 `false` 所有區段ID都已整合為單一批次ID。 值表示 `true` 一個區段ID會匯出為一個批次ID。</li></ul> |
| `fields` | 匯出欄位的清單，以逗號分隔。 |
| `schema.name` | 與要導出資料的資料集關聯的方案的名稱。 |
| `filter.segments` | 匯出的區段。 包含下列欄位：<ul><li>`segmentId`:要匯出描述檔的區段ID。</li><li>`segmentNs`:指定的區段名稱空間 `segmentID`。</li><li>`status`:為提供狀態過濾器的字串陣列 `segmentID`。 依預設， `status` 將會有值， `["realized", "existing"]` 代表目前時段屬於區段的所有描述檔。 可能的值包括：「已實現」、「現有」和「已退出」。</li></ul> |
| `mergePolicy` | 合併已導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，指示導出作業所用的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指示導出配置檔案所花費的時間。 |
| `totalExportedProfileCounter` | 所有批導出的配置檔案總數。 |

## 取消或刪除特定的導出作業 {#delete}

您可以向端點發出DELETE請求，並在請求路徑中提供您要刪除的導出作業的 `/export/jobs` ID，以請求刪除指定的導出作業。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 您 `id` 要刪除的匯出工作。 |

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

閱讀本指南後，您現在更能瞭解匯出工作的運作方式。