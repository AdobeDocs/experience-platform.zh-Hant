---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；導出作業；api;
solution: Experience Platform
title: 段導出作業API終結點
topic-legacy: developer guide
description: 導出作業是用於將受眾段成員保留到資料集的非同步進程。 可以在Adobe Experience Platform分段服務API中使用/export/jobs終結點，它允許您以寫程式方式檢索、建立和取消導出作業。
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---

# 段導出作業終結點

導出作業是用於將受眾段成員保留到資料集的非同步進程。 您可以使用 `/export/jobs` Adobe Experience Platform分段API中的端點，它允許您以寫程式方式檢索、建立和取消導出作業。

>[!NOTE]
>
>本指南介紹在 [!DNL Segmentation API]。 有關如何管理導出作業的資訊 [!DNL Real-time Customer Profile] 資料，請參閱上的指南 [導出配置檔案API中的作業](../../profile/api/export-jobs.md)

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 檢索導出作業清單 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索IMS組織的所有導出作業的清單 `/export/jobs` 端點。

**API格式**

的 `/export/jobs` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們以幫助降低昂貴的開銷。 調用此終結點時沒有參數將檢索組織可用的所有導出作業。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | 指定返回的導出作業數。 |
| `{OFFSET}` | 指定結果頁的偏移。 |
| `{STATUS}` | 根據狀態篩選結果。 支援的值為&quot;NEW&quot;、&quot;SUCCEEDED&quot;和&quot;FAILED&quot;。 |

**要求**

以下請求將檢索IMS組織中最後兩個導出作業。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應根據請求路徑中提供的查詢參數返回HTTP狀態200，其中列出了成功完成的導出作業。

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
| `destination` | 導出資料的目標資訊：<ul><li>`datasetId`:導出資料的資料集的ID。</li><li>`segmentPerBatch`:一個布爾值，它顯示段ID是否已合併。 值「false」表示所有段ID都導出為單個批ID。 值「true」表示將一個段ID導出為一個批ID。 **注：** 將值設定為true可能會影響批導出效能。</li></ul> |
| `fields` | 導出欄位的清單，用逗號分隔。 |
| `schema.name` | 與要導出資料的資料集關聯的架構的名稱。 |
| `filter.segments` | 導出的段。 包括以下欄位：<ul><li>`segmentId`:配置檔案將導出到的段ID。</li><li>`segmentNs`:給定的段命名空間 `segmentID`。</li><li>`status`:提供用於PC的狀態過濾器的字串的陣列 `segmentID`。 預設情況下， `status` 將具有值 `["realized", "existing"]` 表示當前時間段中的所有配置檔案。 可能的值包括：「已實現」、「現有」和「已退出」。 值「已實現」表示配置檔案正在輸入段。 「現有」值表示配置檔案繼續在段中。 值「exiting」表示配置檔案正在退出段。</li></ul> |
| `mergePolicy` | 合併導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，指示導出作業運行所用的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指示導出配置檔案所花的時間。 |
| `page` | 有關請求的導出作業的分頁的資訊。 |
| `link.next` | 指嚮導出作業下一頁的連結。 |

## 新建導出作業 {#create}

您可以通過向POST請求 `/export/jobs` 端點。

**API格式**

```http
POST /export/jobs
```

**要求**

以下請求將建立一個新的導出作業，該作業由負載中提供的參數配置。

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
| `fields` | 導出欄位的清單，用逗號分隔。 如果留空，則將導出所有欄位。 |
| `mergePolicy` | 指定用於管理導出資料的合併策略。 在導出多個段時包括此參數。 如果未提供，則導出將採用與給定段相同的合併策略。 |
| `filter` | 一個對象，它根據下面列出的子屬性，按ID、限定時間或接收時間指定要包括在導出作業中的段。 如果保留為空，則將導出所有資料。 |
| `filter.segments` | 指定要導出的段。 忽略此值將導致導出所有配置檔案中的所有資料。 接受段對象陣列，每個陣列都包含以下欄位：<ul><li>`segmentId`: **(使用時需要 `segments`)** 要導出的配置檔案的段ID。</li><li>`segmentNs` *（可選）* 給定的段命名空間 `segmentID`。</li><li>`status` *（可選）* 提供用於PC的狀態過濾器的字串的陣列 `segmentID`。 預設情況下， `status` 將具有值 `["realized", "existing"]` 表示當前時間段中的所有配置檔案。 可能的值包括： `"realized"`。 `"existing"`, `"exited"`。  值「已實現」表示配置檔案正在輸入段。 「現有」值表示配置檔案繼續在段中。 值「exiting」表示配置檔案正在退出段。</li></ul> |
| `filter.segmentQualificationTime` | 基於段限定時間進行篩選。 可以提供開始時間和/或結束時間。 |
| `filter.segmentQualificationTime.startTime` | 給定狀態的段ID的段資格起始時間。 它未提供，對段ID資格的開始時間將沒有篩選器。 必須在中提供時間戳 [RFC 3339](https://tools.ietf.org/html/rfc3339) 的子菜單。 |
| `filter.segmentQualificationTime.endTime` | 給定狀態的段ID的段資格結束時間。 未提供，在段ID資格的結束時間上將不存在篩選器。 必須在中提供時間戳 [RFC 3339](https://tools.ietf.org/html/rfc3339) 的子菜單。 |
| `filter.fromIngestTimestamp ` | 將導出的配置檔案限制為只包括在此時間戳後更新的配置檔案。 必須在中提供時間戳 [RFC 3339](https://tools.ietf.org/html/rfc3339) 的子菜單。 <ul><li>`fromIngestTimestamp` 為 **配置檔案**，如果提供：包括所有合併的配置檔案，其中合併的更新時間戳大於給定時間戳。 支援 `greater_than` 操作數。</li><li>`fromIngestTimestamp` 為 **事件**:在此時間戳之後接收的所有事件都將導出與結果配置檔案結果相對應的事件。 這不是事件時間本身，而是事件的攝取時間。</li> |
| `filter.emptyProfiles` | 一個布爾值，指示是否篩選空配置檔案。 配置檔案可以包含配置檔案記錄、ExperienceEvent記錄或兩者。 沒有配置檔案記錄且只有ExperienceEvent記錄的配置檔案稱為「emptyProfiles」。 要導出配置檔案儲存中的所有配置檔案，請設定 `emptyProfiles` 至 `true`。 如果 `emptyProfiles` 設定為 `false`，只導出儲存中具有配置檔案記錄的配置檔案。 預設情況下，如果 `emptyProfiles` 屬性未包括，只導出包含配置檔案記錄的配置檔案。 |
| `additionalFields.eventList` | 通過提供以下一個或多個設定，控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`fields`:控制要導出的欄位。</li><li>`filter`:指定限制從關聯對象中包括的結果的條件。 需要導出所需的最小值，通常為日期。</li><li>`filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳後已接收的事件。 這不是事件時間本身，而是事件的攝取時間。</li><li>`filter.toIngestTimestamp`:將時間戳篩選為在提供時間戳之前已接收的時間戳。 這不是事件時間本身，而是事件的攝取時間。</li></ul> |
| `destination` | **（必需）** 有關導出資料的資訊：<ul><li>`datasetId`: **（必需）** 要導出資料的資料集的ID。</li><li>`segmentPerBatch`: *（可選）* 一個布爾值（如果未提供），預設為&quot;false&quot;。 值「false」將所有段ID導出為單個批ID。 值「true」將一個段ID導出為一個批ID。 請注意，將值設定為&quot;true&quot;可能會影響批導出效能。</li></ul> |
| `schema.name` | **（必需）** 與要導出資料的資料集關聯的架構的名稱。 |
| `evaluationInfo.segmentation` | *（可選）* 一個布爾值，如果未提供，則預設為 `false`。 值 `true` 表示需要在導出作業上執行分段。 |

**回應**

成功的響應返回HTTP狀態200，其中包含您新建立的導出作業的詳細資訊。

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
| `id` | 系統生成的只讀值，標識剛建立的導出作業。 |

或者，如果 `destination.segmentPerBatch` 已經準備好 `true`，也請參見Wiki頁。 `destination` 上面的物體 `batches` 陣列，如下所示：

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

您可以通過向GET請求來檢索有關特定導出作業的詳細資訊 `/export/jobs` 端點，並提供要在請求路徑中檢索的導出作業的ID。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 的子菜單。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定導出作業的詳細資訊。

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
| `destination` | 導出資料的目標資訊：<ul><li>`datasetId`:導出資料的資料集的ID。</li><li>`segmentPerBatch`:一個布爾值，它顯示段ID是否已合併。 值 `false` 表示所有段ID都是一個批ID。 值 `true` 表示將一個段ID導出為一個批ID。</li></ul> |
| `fields` | 導出欄位的清單，用逗號分隔。 |
| `schema.name` | 與要導出資料的資料集關聯的架構的名稱。 |
| `filter.segments` | 導出的段。 包括以下欄位：<ul><li>`segmentId`:要導出的配置檔案的段ID。</li><li>`segmentNs`:給定的段命名空間 `segmentID`。</li><li>`status`:提供用於PC的狀態過濾器的字串的陣列 `segmentID`。 預設情況下， `status` 將具有值 `["realized", "existing"]` 表示當前時間段中的所有配置檔案。 可能的值包括：「已實現」、「現有」和「已退出」。  值「已實現」表示配置檔案正在輸入段。 「現有」值表示配置檔案繼續在段中。 值「exiting」表示配置檔案正在退出段。</li></ul> |
| `mergePolicy` | 合併導出資料的策略資訊。 |
| `metrics.totalTime` | 一個欄位，指示導出作業運行所用的總時間。 |
| `metrics.profileExportTime` | 一個欄位，指示導出配置檔案所花的時間。 |
| `totalExportedProfileCounter` | 所有批導出的配置檔案總數。 |

## 取消或刪除特定導出作業 {#delete}

您可以請求刪除指定的導出作業，方法是向 `/export/jobs` 端點，並提供您希望在請求路徑中刪除的導出作業的ID。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 的子菜單。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204，並顯示以下消息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 後續步驟

讀完本指南後，您現在對出口工作的工作方式有了更好的瞭解。
