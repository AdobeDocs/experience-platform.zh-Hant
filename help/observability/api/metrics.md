---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 度量API終結點
description: 瞭解如何使用Oncebrity Insights API在Experience Platform中檢索可觀性度量。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---

# 度量終結點

可觀性指標可提供Adobe Experience Platform各種功能的使用情況統計、歷史趨勢和效能指標的洞見。 的 `/metrics` 端點 [!DNL Observability Insights API] 允許您以寫程式方式檢索組織活動的度量資料 [!DNL Platform]。

>[!NOTE]
>
>以前版本的度量終結點(V1)已棄用。 本文檔專門介紹當前版本(V2)。 有關舊式實現的V1端點的詳細資訊，請參閱 [API引用](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1)。

## 快速入門

本指南中使用的API終結點是 [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 檢索可觀測度量

您可以通過向Web站點發出POST請求來檢索度量資料 `/metrics` 端點，指定要在負載中檢索的度量。

**API格式**

```http
POST /metrics
```

**要求**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `start` | 檢索度量資料的最早日期/時間。 |
| `end` | 從中檢索度量資料的最新日期/時間。 |
| `granularity` | 一個可選欄位，它指示按度量資料除法的時間間隔。 例如， `DAY` 返回間隔的每天的度量 `start` 和 `end` 日期，而值 `MONTH` 將按月對度量結果分組。 使用此欄位時， `downsample` 還必須提供屬性，以指示資料分組所依據的聚合函式。 |
| `metrics` | 對象陣列，每個要檢索的度量各一個。 |
| `name` | 可觀性透視識別的度量的名稱。 查看 [附錄](#available-metrics) 的子菜單。 |
| `filters` | 可選欄位，允許您按特定資料集篩選度量。 該欄位是對象陣列（每個篩選器對應一個對象），每個對象包含以下屬性： <ul><li>`name`:要篩選度量的實體類型。 當前，僅 `dataSets` 支援。</li><li>`value`:一個或多個資料集的ID。 可以將多個資料集ID作為單個字串提供，每個ID由垂直條形字元分隔(`\|`)。</li><li>`groupBy`:設定為true時，表示 `value` 表示多個資料集，其度量結果應單獨返回。 如果設定為false，則將這些資料集的度量結果分組在一起。</li></ul> |
| `aggregator` | 指定應用於將多次序列記錄分組為單個結果的聚合函式。 有關可用聚合器的詳細資訊，請參閱 [OpenTSDB文檔](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators)。 |
| `downsample` | 可選欄位，它允許您指定聚合函式，通過將欄位分類為間隔（或「儲存段」）來降低度量資料的採樣率。 下採樣的間隔由 `granularity` 屬性。 有關縮減採樣的詳細資訊，請參閱 [OpenTSDB文檔](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators)。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回請求中指定的度量和篩選器的結果資料點。

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `metricResponses` | 一個陣列，其對象表示請求中指定的每個度量。 每個對象都包含有關篩選器配置和返回的度量資料的資訊。 |
| `metric` | 請求中提供的度量之一的名稱。 |
| `filters` | 指定度量的篩選器配置。 |
| `datapoints` | 其對象表示指定度量和篩選器的結果的陣列。 陣列中的對象數取決於請求中提供的篩選器選項。 如果未提供篩選器，則陣列將只包含一個表示所有資料集的對象。 |
| `groupBy` | 如果在 `filter` 度量的屬性，以及 `groupBy` 選項在請求中設定為true，此對象將包含相應的資料集的ID `dps` 屬性。<br><br>如果此對象在響應中顯示為空，則 `dps` 屬性適用於在 `filters` 陣列（或所有資料集） [!DNL Platform] )。 |
| `dps` | 給定度量、篩選器和時間範圍的返回資料。 此對象中的每個鍵都表示一個時間戳，其中具有指定度量的相應值。 每個資料點之間的時間段取決於 `granularity` 在請求中指定的值。 |

{style="table-layout:auto"}

## 附錄

以下部分包含有關使用 `/metrics` 端點。

### 可用度量 {#available-metrics}

下表列出了由 [!DNL Observability Insights]，按 [!DNL Platform] 服務。 每個度量都包括描述和接受的ID查詢參數。

>[!NOTE]
>
>除非另有說明，否則所有列出的ID查詢參數都是可選的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述Adobe Experience Platform的指標 [!DNL Data Ingestion]。 指標 **粗** 是流式接收度量。

| 洞察度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 為一個資料集或所有資料集所攝取的所有資料的累計大小。 | 資料集 ID |
| timeseries.ingestion.dataset.dailysize | 針對一個資料集或所有資料集按每日使用情況接收的資料大小。 | 資料集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集失敗的批處理數。 | 資料集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 為一個資料集或所有資料集所攝取的批次數。 | 資料集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 為一個資料集或所有資料集所攝取的記錄數。 | 資料集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」消息的總數。 | 資料集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 為一個資料入口或所有資料入口接收的消息總數。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 為一個資料入口或所有資料入口接收的資料的總大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 成功調用一個資料入口或所有資料入口的HTTP總數。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 對一個資料入口或所有資料入口的失敗HTTP調用總數。 | 入口ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述Adobe Experience Platform的指標 [!DNL Identity Service]。

| 洞察度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 寫入其資料源的記錄數 [!DNL Identity Service]，用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.identity.dataset.recordfailed.count | 失敗的記錄數 [!DNL Identity Service]，用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 命名空間失敗的標識記錄數。 | 命名空間ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空間跳過的標識記錄數。 | 命名空間ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 組織的標識圖中儲存的唯一標識數。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 命名空間的標識圖中儲存的唯一標識數。 | 命名空間ID(**必需**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 特定圖形強度（「未知」、「弱」或「強」）在組織的標識圖中儲存的唯一標識數。 | 圖形強度(**必需**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述了 [!DNL Real-Time Customer Profile]。

| 洞察度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 從 [!DNL Data Lake] 按 [!DNL Profile]，用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 寫入其資料源的記錄數 [!DNL Profile]，用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 數量 [!DNL Profile] 為資料集或所有資料集接收的批處理。 | 資料集 ID |

{style="table-layout:auto"}

### 錯誤訊息

來自 `/metrics` 在某些條件下，終結點可能返回錯誤消息。 這些錯誤消息將以下格式返回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `title` | 包含錯誤消息的字串以及可能發生錯誤的原因。 |
| `report` | 包含有關錯誤的上下文資訊，包括觸發該錯誤的操作中使用的沙盒和組織。 |

{style="table-layout:auto"}

下表列出了API可返回的不同錯誤代碼：

| 錯誤代碼 | 標題 | 說明 |
| --- | --- | --- |
| `INSGHT-1000-400` | 錯誤的請求負載 | 請求負載出現問題。 確保與顯示的負載格式完全匹配 [上](#v2)。 任何可能的原因都可能觸發此錯誤：<ul><li>缺少必填欄位，如 `aggregator`</li><li>無效的度量</li><li>請求包含無效的聚合器</li><li>開始日期在結束日期之後</li></ul> |
| `INSGHT-1001-400` | 度量查詢失敗 | 由於請求錯誤或查詢本身不可解析，嘗試查詢度量資料庫時出錯。 請確保請求的格式正確，然後再重試。 |
| `INSGHT-1001-500` | 度量查詢失敗 | 由於伺服器錯誤，嘗試查詢度量資料庫時出錯。 請重試請求，如果問題仍然存在，請與Adobe支援聯繫。 |
| `INSGHT-1002-500` | 服務錯誤 | 由於內部錯誤，無法處理該請求。 請重試請求，如果問題仍然存在，請與Adobe支援聯繫。 |
| `INSGHT-1003-401` | 沙盒驗證錯誤 | 由於沙盒驗證錯誤，無法處理該請求。 確保在中提供的沙盒名稱 `x-sandbox-name` 標頭表示組織的有效已啟用沙盒，然後再次嘗試請求。 |

{style="table-layout:auto"}
