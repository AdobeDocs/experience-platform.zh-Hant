---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 量度API端點
description: 了解如何使用可觀察性前瞻分析API在Experience Platform中擷取可觀察性量度。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# 量度端點

可觀察性量度可提供Adobe Experience Platform中各種功能的使用量統計資料、歷史趨勢和效能指標的深入分析。 此 `/metrics` 端點 [!DNL Observability Insights API] 可讓您以程式設計方式擷取組織活動的量度資料，位於 [!DNL Platform].

>[!NOTE]
>
>舊版的量度端點(V1)已淘汰。 本檔案專注於目前版本(V2)。 如需舊版實作之V1端點的詳細資訊，請參閱 [API參考](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## 快速入門

本指南中使用的API端點屬於 [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 擷取可觀察性量度

您可以向 `/metrics` 端點，指定您要在裝載中擷取的量度。

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
| `start` | 要擷取量度資料的最早日期/時間。 |
| `end` | 要擷取量度資料的最新日期/時間。 |
| `granularity` | 選用欄位，指出依量度資料劃分的時間間隔。 例如，值為 `DAY` 傳回之間每天的量度 `start` 和 `end` 日期，但 `MONTH` 會改為依月份將量度結果分組。 使用此欄位時，對應的 `downsample` 還必須提供屬性，以指明資料的分組函式。 |
| `metrics` | 物件陣列，每個要擷取的量度各一個。 |
| `name` | 可觀察性前瞻分析所識別的量度名稱。 請參閱 [附錄](#available-metrics) 以取得已接受量度名稱的完整清單。 |
| `filters` | 選用欄位，可讓您依特定資料集篩選量度。 欄位是物件的陣列（每個篩選器各一個），每個物件包含下列屬性： <ul><li>`name`:要據以篩選量度的實體類型。 目前，僅 `dataSets` 支援。</li><li>`value`:一或多個資料集的ID。 多個資料集ID可設為單一字串，每個ID以垂直長條字元(`\|`)。</li><li>`groupBy`:設為true時，表示對應的 `value` 代表應個別傳回其量度結果的多個資料集。 如果設為false，系統會將這些資料集的量度結果分組。</li></ul> |
| `aggregator` | 指定應用於將多個時間序列記錄分組為單個結果的聚合函式。 有關可用聚合器的詳細資訊，請參閱 [OpenTSDB檔案](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | 選用欄位，可讓您指定匯總函式，透過將欄位排序為間隔（或「貯體」）來降低量度資料的取樣率。 縮減取樣的間隔由 `granularity` 屬性。 有關縮減取樣的詳細資訊，請參閱 [OpenTSDB檔案](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style="table-layout:auto"}

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
| `metricResponses` | 陣列，其物件代表請求中指定的每個量度。 每個物件都包含篩選器設定和傳回量度資料的相關資訊。 |
| `metric` | 請求中提供的其中一個量度的名稱。 |
| `filters` | 指定量度的篩選器設定。 |
| `datapoints` | 陣列，其物件代表指定量度和篩選器的結果。 陣列中的物件數目取決於請求中提供的篩選選項。 若未提供篩選器，陣列將只會包含代表所有資料集的單一物件。 |
| `groupBy` | 若在 `filter` 量度的屬性，以及 `groupBy` 選項設為true時，此物件將會包含對應之資料集的ID `dps` 屬性。<br><br>如果此物件在回應中顯示為空白，則對應的 `dps` 屬性會套用至中提供的所有資料集 `filters` 陣列（或所有資料集） [!DNL Platform] 若未提供篩選器)。 |
| `dps` | 指定量度、篩選器和時間範圍的傳回資料。 此物件中的每個索引鍵代表時間戳記，以及指定量度的對應值。 每個資料點之間的時段取決於 `granularity` 值。 |

{style="table-layout:auto"}

## 附錄

下節包含使用 `/metrics` 端點。

### 可用量度 {#available-metrics}

下表列出 [!DNL Observability Insights]，劃分依據 [!DNL Platform] 服務。 每個量度都包含說明和接受的ID查詢參數。

>[!NOTE]
>
>除非另有說明，否則所有列出的ID查詢參數均為選用。

#### [!DNL Data Ingestion] {#ingestion}

下表概述Adobe Experience Platform的量度 [!DNL Data Ingestion]. 中的量度 **粗體** 是串流獲取量度。

| 前瞻分析量度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 針對一個資料集或所有資料集擷取的所有資料累積大小。 | 資料集 ID |
| timeseries.ingestion.dataset.dailysize | 一個資料集或所有資料集每日擷取的資料大小。 | 資料集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集的批次失敗數。 | 資料集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 一個資料集或所有資料集的批次擷取數。 | 資料集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 為一個資料集或所有資料集擷取的記錄數。 | 資料集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」消息總數。 | 資料集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 為一個資料入口或所有資料入口接收的報文總數。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 為一個資料入口或所有資料入口接收的資料的總大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 對一個資料入口或所有資料入口成功的HTTP呼叫總數。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 對一個資料入口或所有資料入口的失敗HTTP調用總數。 | 入口ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述Adobe Experience Platform的量度 [!DNL Identity Service].

| 前瞻分析量度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 寫入其資料源的記錄數(按 [!DNL Identity Service]，適用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.identity.dataset.recordfailed.count | 失敗的記錄數 [!DNL Identity Service]，適用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 命名空間失敗的身份記錄數。 | 命名空間ID(**必填**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空間跳過的身份記錄數。 | 命名空間ID(**必填**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 您IMS組織的身分圖表中儲存的不重複身分數。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 命名空間的身分圖表中儲存的不重複身分數。 | 命名空間ID(**必填**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 針對特定圖表強度（「未知」、「弱」或「強」），儲存在您IMS組織之身分圖表中的不重複身分數。 | 圖表強度(**必填**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述 [!DNL Real-Time Customer Profile].

| 前瞻分析量度 | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 從 [!DNL Data Lake] by [!DNL Profile]，適用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 寫入其資料源的記錄數(按 [!DNL Profile]，適用於一個資料集或所有資料集。 | 資料集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 數量 [!DNL Profile] 為資料集或所有資料集批次匯入。 | 資料集 ID |

{style="table-layout:auto"}

### 錯誤訊息

來自 `/metrics` 端點可能會在特定條件下傳回錯誤訊息。 這些錯誤訊息會以下列格式傳回：

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
| `title` | 包含錯誤訊息的字串，以及可能發生的可能原因。 |
| `report` | 包含錯誤的相關內容資訊，包括觸發錯誤的操作所使用的沙箱和IMS組織。 |

{style="table-layout:auto"}

下表列出API可傳回的不同錯誤碼：

| 錯誤代碼 | 標題 | 說明 |
| --- | --- | --- |
| `INSGHT-1000-400` | 請求裝載錯誤 | 請求裝載有誤。 請確定您的有效負載格式符合如所示 [abos](#v2). 任何可能的原因都可能觸發此錯誤：<ul><li>缺少必填欄位，例如 `aggregator`</li><li>無效的量度</li><li>請求包含無效的聚合器</li><li>開始日期在結束日期之後</li></ul> |
| `INSGHT-1001-400` | 度量查詢失敗 | 由於請求錯誤或查詢本身不可剖析，因此嘗試查詢量度資料庫時發生錯誤。 請先確定請求的格式正確，然後再重試。 |
| `INSGHT-1001-500` | 度量查詢失敗 | 由於伺服器錯誤，嘗試查詢度量資料庫時出錯。 請再試一次請求，如果問題仍然存在，請聯繫Adobe支援。 |
| `INSGHT-1002-500` | 服務錯誤 | 由於內部錯誤，無法處理該請求。 請再試一次請求，如果問題仍然存在，請聯繫Adobe支援。 |
| `INSGHT-1003-401` | 沙箱驗證錯誤 | 由於沙箱驗證錯誤，無法處理請求。 確定您在 `x-sandbox-name` 標題代表IMS組織的有效且已啟用的沙箱，然後再次嘗試請求。 |

{style="table-layout:auto"}
