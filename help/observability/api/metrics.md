---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用量度
topic: developer guide
translation-type: tm+mt
source-git-commit: ae6f220cdec54851fb78b7ba8a8eb19f2d06b684
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 2%

---


# 量度端點

可觀測度量可針對Adobe Experience Platform中的各種功能，提供使用統計資料、歷史趨勢和績效指標的深入資訊。 中 `/metrics` 的端點 [!DNL Observability Insights API] 可讓您以程式設計方式擷取組織活動的量度資料 [!DNL Platform]。

## 快速入門

本指南中使用的API端點是 [[!DNL Observability Insights] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。 在繼續之前，請先閱讀快速入門 [指南](./getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 擷取可觀測度量

使用API擷取量度資料時，支援兩種方法：

* [第1版](#v1):使用查詢參數指定量度。
* [第2版](#v2):使用JSON裝載指定篩選並套用至量度。

### Version 1 {#v1}

您可以透過對端點提出GET請求，透過使 `/metrics` 用查詢參數指定量度，來擷取量度資料。

**API格式**

參數中必須至少提供一個量 `metric` 度。 其他查詢參數是篩選結果的可選參數。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 參數 | 說明 |
| --- | --- |
| `{METRIC}` | 您要公開的量度。 在單一呼叫中合併多個量度時，您必須使用&amp;符號(`&`)來分隔個別量度。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 您要公開其度 [!DNL Platform] 量的特定資源的識別碼。 此ID可能是選用、必要或不適用，視使用的量度而定。 請參 [閱附錄](#available-metrics) ，以取得可用度量的清單，包括每個度量的支援ID（必要和選用）。 |
| `{DATE_RANGE}` | 您要公開的量度日期範圍，使用ISO 8601格式(例如 `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`)。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回對象清單，每個對象都包含提供的時間戳和請求路徑中 `dateRange` 指定的度量的相應值。 如果請 `id` 求路 [!DNL Platform] 徑中包含資源，則結果將僅適用於該特定資源。 若省略 `id` 此項目，結果將套用至IMS組織內的所有適用資源。

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Version 2 {#v2}

您可以透過向端點提出POST請求，並指 `/metrics` 定您要在裝載中擷取的量度，來擷取量度資料。

**API格式**

```http
POST /metrics
```

**請求**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `start` | 擷取量度資料的最早日期／時間。 |
| `end` | 擷取量度資料的最新日期／時間。 |
| `granularity` | 可選欄位，指出依量度資料除以的時間間隔。 例如，值若是傳回 `DAY` 日期與日期之間每日的量度， `start``end` 則值若是， `MONTH` 則會依月將量度結果分組。 使用此欄位時，還必須提 `downsample` 供相應的屬性，以指示資料分組所依據的聚合函式。 |
| `metrics` | 物件陣列，每個要擷取的量度各一個。 |
| `name` | 可觀察性洞察所識別之量度的名稱。 請參閱附 [錄](#available-metrics) ，以取得已接受量度名稱的完整清單。 |
| `filters` | 可選欄位，可讓您依特定資料集篩選量度。 此欄位是物件的陣列（每個篩選器各一個），每個物件包含下列屬性： <ul><li>`name`:要篩選量度的實體類型。 目前僅支 `dataSets` 援。</li><li>`value`:一或多個資料集的ID。 多個資料集ID可提供為單一字串，每個ID由垂直橫條字元(`|`)分隔。</li><li>`groupBy`:設為true時，表示對應的代表多 `value` 個資料集，其量度結果應個別傳回。 如果設為false，這些資料集的度量結果會分組在一起。</li></ul> |
| `aggregator` | 指定應用於將多個時間序列記錄分組為單個結果的聚合函式。 有關可用聚合器的詳細資訊，請參閱 [OpenTSDB文檔](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)。 |
| `downsample` | 可選欄位，可讓您指定匯總函式，透過將欄位排序至間隔（或「區間」）來降低量度資料的取樣率。 縮減採樣的間隔由屬性確 `granularity` 定。 有關縮減取樣的詳細資訊，請參閱 [OpenTSDB檔案](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)。 |

**回應**

成功的回應會傳回請求中指定之量度和篩選器的產生資料點。

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
| `metricResponses` | 陣列，其物件代表請求中指定的每個度量。 每個物件都包含篩選設定和傳回量度資料的相關資訊。 |
| `metric` | 請求中提供之其中一個度量的名稱。 |
| `filters` | 指定量度的篩選設定。 |
| `datapoints` | 一個陣列，其對象表示指定度量和篩選器的結果。 陣列中的物件數目取決於請求中提供的篩選選項。 如果未提供篩選器，則陣列將只包含一個表示所有資料集的對象。 |
| `groupBy` | 如果在度量的屬性中指 `filter` 定了多個資料集，而請求中的選項設定為 `groupBy` true，此物件將包含對應屬性套用之資料集 `dps` 的ID。<br><br>如果此對象在響應中顯示為空，則相應的屬 `dps` 性將應用於陣列中提供的所有資料集(或 `filters` 未提供篩選器的 [!DNL Platform] 所有資料集)。 |
| `dps` | 指定量度、篩選和時間範圍的傳回資料。 此物件中的每個索引鍵代表具有指定量度對應值的時間戳記。 每個資料點之間的時段取決於請 `granularity` 求中指定的值。 |

## 附錄

下節包含有關使用端點的其他 `/metrics` 資訊。

### 可用量度 {#available-metrics}

下表列出依服務劃分的所有公 [!DNL Observability Insights]開度 [!DNL Platform] 量。 每個度量都包含說明和接受的ID查詢參數。

>[!NOTE]
>
>除非另有說明，否則所有列出的ID查詢參數都是選用的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述Adobe Experience Platform的量度 [!DNL Data Ingestion]。 粗體量 **度是串流** 擷取量度。

| 前瞻分析度量 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 建立的資料集總數。 | 不適用 |
| timeseries.ingestion.dataset.size | 針對一個資料集或所有資料集所擷取的所有資料累積大小。 | 資料集ID |
| timeseries.ingestion.dataset.dailysize | 針對一個資料集或所有資料集，依每日使用量而擷取的資料大小。 | 資料集ID |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集的批處理失敗數。 | 資料集ID |
| timeseries.ingestion.dataset.batchsuccess.count | 針對一個資料集或所有資料集所吸收的批次數。 | 資料集ID |
| timeseries.ingestion.dataset.recordsuccess.count | 一個資料集或所有資料集所吸收的記錄數。 | 資料集ID |
| **timeseries.data.collection.validation.total.messages.rate** | 一個資料集或所有資料集的消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.valid.messages.rate** | 一個資料集或所有資料集的有效消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一個資料集或所有資料集的無效消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.type.count** | 一個資料集或所有資料集的無效「類型」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.range.count** | 一個資料集或所有資料集的無效「範圍」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.format.count** | 一個資料集或所有資料集的無效「格式」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.pattern.count** | 一個資料集或所有資料集的無效「模式」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.enum.count** | 一個資料集或所有資料集的無效「列舉」訊息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.unclassified.count** | 一個資料集或所有資料集的無效「未分類」消息總數。 | 資料集ID |
| **timeseries.data.collection.validation.category.unknown.count** | 一個資料集或所有資料集的無效「未知」消息總數。 | 資料集ID |
| **timeseries.data.collection.inlet.total.messages.received** | 為一個資料入口或所有資料入口接收的消息總數。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 為一個資料入口或所有資料入口接收的資料的總大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 成功呼叫一個資料入口或所有資料入口的HTTP呼叫總數。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 對一個資料入口或所有資料入口的失敗HTTP呼叫總數。 | 入口ID |

#### [!DNL Identity Service] {#identity}

下表概述Adobe Experience Platform的量度 [!DNL Identity Service]。

| 前瞻分析度量 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 一個資料集或所有資料集寫入 [!DNL Identity Service]到其資料源的記錄數。 | 資料集ID |
| timeseries.identity.dataset.recordfailed.count | 失敗的記錄數 [!DNL Identity Service]，對於一個資料集或所有資料集。 | 資料集ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 成功接收命名空間的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 名稱空間失敗的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空間跳過的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 儲存在IMS組織身分圖表中的獨特身分數。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 名稱空間的識別圖中儲存的獨特身份數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | 儲存在IMS組織之識別圖中的唯一圖形識別數。 | 不適用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS組織在識別圖中針對特定圖形強度（「未知」、「弱」或「強」）儲存的獨特身分數。 | 圖形強度(**必要**) |

#### [!DNL Privacy Service] {#privacy}

下表概述Adobe Experience Platform的量度 [!DNL Privacy Service]。

| 前瞻分析度量 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 從GDPR建立的工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.completedjobs.count | 來自GDPR的已完成工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.errorjobs.count | 來自GDPR的錯誤工作總數。 | ENV(必&#x200B;**要**) |

#### [!DNL Query Service] {#query}

下表概述Adobe Experience Platform的量度 [!DNL Query Service]。

| 前瞻分析度量 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非週期性排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.scheduledrecurring.count | 循環排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.batchquery.count | 執行的批次查詢總數。 | 不適用 |
| timeseries.queryservice.query.scheduledquery.count | 已執行的計畫查詢總數。 | 不適用 |
| timeseries.queryservice.query.interactivequery.count | 執行的互動式查詢總數。 | 不適用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 來自PSQL的已執行批次查詢總數。 | 不適用 |

#### [!DNL Real-time Customer Profile] {#profile}

下表概述的量度 [!DNL Real-time Customer Profile]。

| 前瞻分析度量 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 從中讀取的記錄數 [!DNL Data Lake] 量，對於 [!DNL Profile]一個資料集或所有資料集。 | 資料集ID |
| timeseries.profiles.dataset.recordsuccess.count | 通過、對一個資料集或所有資料集 [!DNL Profile]寫入其資料源的記錄數。 | 資料集ID |
| timeseries.profiles.dataset.recordfailed.count | 失敗的記錄數 [!DNL Profile]，對於一個資料集或所有資料集。 | 資料集ID |
| timeseries.profiles.dataset.batchsuccess.count | 資料集 [!DNL Profile] 或所有資料集所吸收的批次數。 | 資料集ID |
| timeseries.profiles.dataset.batchfailed.count | 一個資料 [!DNL Profile] 集或所有資料集的批次數失敗。 | 資料集ID |
| platform.ups.ingest.streaming.request.m1_rate | 傳入請求率。 | IMS組織(必&#x200B;**要**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 擷取成功率。 | IMS組織(必&#x200B;**要**) |
| platform.ups.ingest.streaming.records.created.m15_rate | 資料集新記錄的吸收率。 | 資料集ID(必&#x200B;**要**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 為資料集建立請求的順序錯誤時間戳記記錄的比率。 | 資料集ID(必&#x200B;**要**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 資料集上次建立記錄要求的時間戳記。 | 資料集ID(必&#x200B;**要**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 資料集更新請求的順序錯誤時間戳記記錄比率。 | 資料集ID(必&#x200B;**要**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 資料集上次更新記錄要求的時間戳記。 | 資料集ID(必&#x200B;**要**) |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均記錄大小。 | IMS組織(必&#x200B;**要**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | 針對資料集所收錄記錄的更新請求率。 | 資料集ID(必&#x200B;**要**) |

### 錯誤訊息

端點的回 `/metrics` 應可能會在特定條件下傳回錯誤訊息。 這些錯誤訊息會以下列格式傳回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
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
| `title` | 包含錯誤訊息的字串，以及可能發生錯誤訊息的可能原因。 |
| `report` | 包含錯誤的相關內容資訊，包括觸發錯誤的作業中使用的沙盒和IMS組織。 |

下表列出API可傳回的不同錯誤碼：

| 錯誤代碼 | 標題 | 說明 |
| --- | --- | --- |
| `INSGHT-1000-400` | 請求裝載錯誤 | 請求裝載發生問題。 請確定您與上述的裝載格式完全 [相符](#v2)。 任何可能的原因都可能觸發此錯誤：<ul><li>遺失必要欄位，例如 `aggregator`</li><li>無效的量度</li><li>請求包含無效的匯整器</li><li>開始日期在結束日期之後發生</li></ul> |
| `INSGHT-1001-400` | 量度查詢失敗 | 嘗試查詢量度資料庫時發生錯誤，因為請求錯誤或查詢本身不可分。 請先確定您的請求已正確格式化，然後再再試一次。 |
| `INSGHT-1001-500` | 量度查詢失敗 | 由於伺服器錯誤，嘗試查詢量度資料庫時發生錯誤。 請再試一次請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1002-500` | 服務錯誤 | 由於內部錯誤，無法處理請求。 請再試一次請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1003-401` | 沙盒驗證錯誤 | 由於沙盒驗證錯誤，無法處理請求。 在再次嘗試請求之前，請確 `x-sandbox-name` 定您在標題中提供的沙盒名稱代表IMS組織的有效啟用沙盒。 |
