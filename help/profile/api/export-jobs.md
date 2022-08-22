---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 配置檔案導出作業API終結點
topic-legacy: guide
type: Documentation
description: 即時客戶概要資訊使您能夠通過將來自多個來源的資料（包括屬性資料和行為資料）匯集在一起，構建Adobe Experience Platform內單個客戶的單一視圖。 然後可將配置檔案資料導出到資料集以進一步處理。
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# 配置檔案導出作業終結點

[!DNL Real-time Customer Profile] 使您能夠通過將來自多個來源的資料（包括屬性資料和行為資料）匯集在一起，構建單個客戶視圖。 然後可將配置檔案資料導出到資料集以進一步處理。 例如，從 [!DNL Profile] 資料可以導出以用於激活，配置檔案屬性可以導出以用於報告。

本文檔提供了使用 [配置檔案API](https://www.adobe.com/go/profile-apis-en)。

>[!NOTE]
>
>本指南介紹在 [!DNL Profile API]。 有關如何管理Adobe Experience Platform細分服務的導出作業的資訊，請參見 [導出分段API中的作業](../../profile/api/export-jobs.md)。

除了建立導出作業外，您還可以訪問 [!DNL Profile] 使用 `/entities` 端點，也稱為「[!DNL Profile Access]。 查看 [實體端點指南](./entities.md) 的子菜單。 有關如何訪問的步驟 [!DNL Profile] 使用UI的資料，請參閱 [使用手冊](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是 [!DNL Real-time Customer Profile] API。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 建立導出作業

導出 [!DNL Profile] 資料需要首先建立資料集，資料將導出到該資料集，然後啟動新的導出作業。 這兩個步驟都可以使用Experience PlatformAPI實現，前者使用目錄服務API，後者使用即時客戶配置檔案API。 以下各節概述了完成每個步驟的詳細說明。

### 建立目標資料集

導出時 [!DNL Profile] 資料，必須首先建立目標資料集。 必須正確配置資料集以確保導出成功。

關鍵注意事項之一是資料集所基於的架構(`schemaRef.id` 中)。 要導出配置檔案資料，資料集必須基於 [!DNL XDM Individual Profile] 聯合架構(`https://ns.adobe.com/xdm/context/profile__union`)。 聯合架構是系統生成的只讀架構，它聚合共用同一類的架構的欄位。 在這個例子中， [!DNL XDM Individual Profile] 類。 有關聯合視圖架構的詳細資訊，請參閱 [架構組合指南基礎中的union部分](../../xdm/schema/composition.md#union)。

本教程中接下來的步驟概述了如何建立引用 [!DNL XDM Individual Profile] 聯合架構使用 [!DNL Catalog] API。 您也可以使用 [!DNL Platform] 用戶介面，用於建立引用聯合模式的資料集。 有關使用UI的步驟，請參見 [導出段的本UI教程](../../segmentation/tutorials/create-dataset-export-segment.md) 但也適用於此。 完成後，您可以返回本教程，繼續執行 [啟動新導出作業](#initiate)。

如果已有相容的資料集並知道其ID，則可以直接執行該步驟 [啟動新導出作業](#initiate)。

**API格式**

```http
POST /dataSets
```

**要求**

以下請求建立新資料集，在負載中提供配置參數。

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
| `schemaRef.id` | 資料集將與之關聯的聯合視圖（架構）的ID。 |

**回應**

成功的響應返回包含新建立的資料集的只讀、系統生成的唯一ID的陣列。 要成功導出配置檔案資料，需要正確配置的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 啟動導出作業 {#initiate}

一旦您擁有了聯合持續資料集，就可以建立導出作業，通過向Web站點發出POST請求，將配置檔案資料永續到資料集 `/export/jobs` 即時客戶配置檔案API中的端點，並提供您希望在請求正文中導出的資料的詳細資訊。

**API格式**

```http
POST /export/jobs
```

**要求**

以下請求將建立新導出作業，在負載中提供配置參數。

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
| `fields` | *（可選）* 將要包含在導出中的資料欄位限制為僅此參數中提供的資料欄位。 忽略此值將導致導出資料中包含所有欄位。 |
| `mergePolicy` | *（可選）* 指定用於管理導出資料的合併策略。 在導出多個段時包括此參數。 |
| `mergePolicy.id` | 合併策略的ID。 |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 忽略此值將預設為最新版本。 |
| `additionalFields.eventList` | *（可選）* 通過提供以下一個或多個設定，控制為子對象或關聯對象導出的時間系列事件欄位：<ul><li>`eventList.fields`:控制要導出的欄位。</li><li>`eventList.filter`:指定限制從關聯對象中包括的結果的條件。 需要導出所需的最小值，通常為日期。</li><li>`eventList.filter.fromIngestTimestamp`:將時間序列事件篩選為在提供的時間戳後已接收的事件。 這不是事件時間本身，而是事件的攝取時間。</li></ul> |
| `destination` | **（必需）** 導出資料的目標資訊：<ul><li>`destination.datasetId`: **（必需）** 要導出資料的資料集的ID。</li><li>`destination.segmentPerBatch`: *（可選）* 一個布爾值，如果未提供，則預設為 `false`。 值 `false` 將所有段ID導出為單個批ID。 值 `true` 將一個段ID導出為一個批ID。 請注意，將值設定為 `true` 可能會影響批導出效能。</li></ul> |
| `schema.name` | **（必需）** 與要導出資料的資料集關聯的架構的名稱。 |

>[!NOTE]
>
>要僅導出配置檔案資料而不包括相關的時間系列資料，請從請求中刪除「additionalFields」對象。

**回應**

成功的響應將返回一個資料集，該資料集包含請求中指定的配置檔案資料。

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

通過向IMS組織執行GET請求，您可以返回特定IMS組織的所有導出作業清單 `export/jobs` 端點。 該請求還支援查詢參數 `limit` 和 `offset`，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| -------- | ----------- |
| `start` | 按請求的建立時間偏移返回的結果頁。 範例：`start=4` |
| `limit` | 限制返回的結果數。 範例：`limit=10` |
| `page` | 按照請求的建立時間返回特定結果頁。 範例：`page=2` |
| `sort` | 按特定欄位按升序對結果排序( **`asc`** )或降序( **`desc`** )順序。 返回多頁結果時，排序參數不起作用。 範例：`sort=updateTime:asc` |

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

響應包括 `records` 包含由IMS組織建立的導出作業的對象。

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

要查看特定導出作業的詳細資訊，或監視其處理時的狀態，您可以向 `/export/jobs` 並包括 `id` 的子菜單。 導出作業一旦完成 `status` 欄位返回值「SUCCEEDED」。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 的子菜單。 |

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
| `batchId` | 從成功導出建立的批的標識符，在讀取配置檔案資料時用於查找。 |

## 取消導出作業

Experience Platform允許您取消現有導出作業，這可能因多種原因而有用，包括導出作業未完成或在處理階段卡住。 要取消導出作業，您可以向 `/export/jobs` 並包括 `id` 要取消的導出作業到請求路徑。

**API格式**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 的 `id` 的子菜單。 |

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

成功的刪除請求返回HTTP狀態204（無內容）和空響應正文，表示取消操作成功。

## 後續步驟

成功完成導出後，您的資料可以在Experience Platform中的資料湖中使用。 然後，您可以使用 [資料存取API](https://www.adobe.io/experience-platform-apis/references/data-access/) 使用 `batchId` 與導出關聯。 根據導出的大小，資料可能以塊為單位，而批可能由幾個檔案組成。

有關如何使用資料存取API訪問和下載批處理檔案的逐步說明，請按照 [資料存取教程](../../data-access/tutorials/dataset-data.md)。

您還可以使用Adobe Experience Platform查詢服務訪問成功導出的即時客戶配置檔案資料。 使用UI或REST風格的API，查詢服務允許您對資料湖中的資料寫入、驗證和運行查詢。

有關如何查詢受眾資料的詳細資訊，請查看 [查詢服務文檔](../../query-service/home.md)。

## 附錄

以下部分包含有關配置檔案API中導出作業的其他資訊。

### 其他導出負載示例

上一節中顯示的示例API調用 [啟動導出作業](#initiate) 建立同時包含配置檔案（記錄）和事件（時間系列）資料的作業。 本節提供了其他請求負載示例，以限制導出包含一種或另一種資料類型。

以下負載將建立一個僅包含配置檔案資料（無事件）的導出作業：

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

要建立僅包含事件資料（無配置檔案屬性）的導出作業，負載可能與以下操作類似：

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

### 導出段

也可以使用導出作業終結點導出受眾段，而不是 [!DNL Profile] 資料。 請參閱上的指南 [導出分段API中的作業](../../segmentation/api/export-jobs.md) 的子菜單。
