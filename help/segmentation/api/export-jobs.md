---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 匯出工作
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# 匯出工作

介紹

- 檢索導出作業清單
- 建立新的匯出工作
- 擷取特定匯出工作
- 取消或刪除特定的導出作業

## 快速入門

本指南中使用的API端點是區段API的一部分。 在繼續之前，請先閱讀區 [段開發人員指南](./getting-started.md)。

尤其是，區 [段開發人員指南的](./getting-started.md#getting-started) 「快速入門」區段包含相關主題的連結、閱讀檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 檢索導出作業清單

您可以向端點提出GET請求，以擷取IMS組織所有匯出工作的清 `/export/jobs` 單。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(可&#x200B;*選*)新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，由&amp;符號(`&`)分隔。 以下列出可用參數。

**查詢參數**

以下是列出導出作業的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的匯出工作。

| 參數 | 說明 |
| --------- | ----------- |
| `limit` | 指定傳回的匯出工作數。 |
| `offset` | 指定結果頁的偏移。 |
| `status` | 根據狀態篩選結果。 支援的值 `NEW`有 `SUCCEEDED`、和 `FAILED`。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的匯出工作清單列為JSON。 下列回應會傳回IMS組織所有成功匯出工作的清單。

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
        "batches": {
          "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
          "segmentNs": "ups",
          "status": [
            "realized"
          ],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        }
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
            "fromIngestTimestamp": "2018-01-01T00:00:00Z"
          }
        }
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
        "aCPDatasetWriteTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        }
      },
      "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
        "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "creationTime": 1538615973895,
      "updateTime": 1538616233239,
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
    }
  ],
  "page": {
    "sortField": "createdTime",
    "sort": "desc",
    "pageOffset": "1540974701302_96",
    "pageSize": 10
  },
  "link": {
    "next": "string"
  }
}
```

## 建立新的匯出工作

您可以通過向端點發出POST請求來建立新的導出 `/export/jobs` 作業。

**API格式**

```http
POST /export/jobs
```

**請求**

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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df"
  },
  "schema": {
    "name": "_xdm.context.profile"
  }
 }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `fields` | 可選. 匯出欄位的清單，以逗號分隔。 如果保留為空白，則將導出所有欄位。 |
| `mergePolicy` | 可選. 如果未提供，則匯出會採用與指定區段相同的合併政策。 |
| `filter` | 可選. 如果保留為空白，則將導出所有資料。 |
| `filter.segments` | 可選. 匯出工作的區段篩選。 |
| `filter.segmentQualificationTime` | 可選. 區段限定時間的篩選。 可以提供開始和／或結束時間。 |
| `filter.fromIngestTimestamp` | 可選. RFC-3339格式化時間戳。 |
| `destination.datasetId` | 必填.資料 `id` 匯出至的資料集的值。 |
| `segments.segmentId` | 必填.要 `id` 導出的段的值。 |
| `segments.sgementNs` | 可選. 給 `namespace` 定區段的。 |



**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之匯出工作的詳細資訊。

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## 擷取特定匯出工作

通過向端點發出GET請求並在請求路徑中提供導出作業的值，可以檢索有關特 `/export/jobs` 定導出作 `id` 業的詳細資訊。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:要 `id` 檢索的導出作業的值。

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定匯出工作的詳細資訊。

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## 取消或刪除特定的導出作業

您可以向端點發出DELETE請求並在請求路徑中提供導出作業的值，以 `/export/jobs` 請求刪除指定 `id` 的導出作業。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:要 `id` 刪除的導出作業的值。

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並顯示下列訊息：

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 後續步驟
