---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用量度
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# 量度端點

可觀測度量可針對Adobe Experience Platform中的各種功能，提供使用統計資料、歷史趨勢和績效指標的深入資訊。 中 `/metrics` 的端點 [!DNL Observability Insights API] 可讓您以程式設計方式擷取組織活動的量度資料 [!DNL Platform]。

## 快速入門

本指南中使用的API端點是 [[!DNL Observability Insights] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。 在繼續之前，請先閱讀快速入門 [指南](./getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 擷取可觀測度量

您可以透過對API中的端點提出GET請求，來擷 `/metrics` 取可觀測度 [!DNL Observability Insights] 量。

**API格式**

使用端點 `/metrics` 時，必須至少提供一個量度請求參數。 其他查詢參數是篩選結果的可選參數。

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
| `{ID}` | 您要公開其度 [!DNL Platform] 量的特定資源的識別碼。 此ID可能是選用、必要或不適用，視使用的量度而定。 請參 [閱附錄](#available-metrics) ，以取得可用度量的清單，以及每個度量的支援ID（必要和選用）。 |
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