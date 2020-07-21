---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用量度
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# 可用度量清單

下表列出依服務劃分的可觀察前瞻分析所公開的所有量 [!DNL Platform] 度。 每個度量都包含說明和接受的ID查詢參數。

## [!DNL Data Ingestion]

下表概述Adobe Experience Platform的量度 [!DNL Data Ingestion]。 粗體量 **度是串流** 擷取量度。

| 前瞻分析度量  | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 建立的資料集總數。 | 不適用 |
| timeseries.ingestion.dataset.size | 針對一個資料集或所有資料集所擷取的所有資料累積大小。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.dailysize | 針對一個資料集或所有資料集，依每日使用量而擷取的資料大小。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集的批處理失敗數。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.batchsuccess.count | 針對一個資料集或所有資料集所吸收的批次數。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.recordsuccess.count | 一個資料集或所有資料集所吸收的記錄數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.total.messages.rate** | 一個資料集或所有資料集的消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.valid.messages.rate** | 一個資料集或所有資料集的有效消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一個資料集或所有資料集的無效消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.type.count** | 一個資料集或所有資料集的無效「類型」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.range.count** | 一個資料集或所有資料集的無效「範圍」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.format.count** | 一個資料集或所有資料集的無效「格式」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.pattern.count** | 一個資料集或所有資料集的無效「模式」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.enum.count** | 一個資料集或所有資料集的無效「列舉」訊息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.unclassified.count** | 一個資料集或所有資料集的無效「未分類」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.validation.category.unknown.count** | 一個資料集或所有資料集的無效「未知」消息總數。 | 資料集ID（選用） |
| **timeseries.data.collection.inlet.total.messages.received** | 為一個資料入口或所有資料入口接收的消息總數。 | 入口ID（可選） |
| **timeseries.data.collection.inlet.total.messages.size.received** | 為一個資料入口或所有資料入口接收的資料的總大小。 | 入口ID（可選） |
| **timeseries.data.collection.inlet.success** | 成功呼叫一個資料入口或所有資料入口的HTTP呼叫總數。 | 入口ID（可選） |
| **timeseries.data.collection.inlet.failure** | 對一個資料入口或所有資料入口的失敗HTTP呼叫總數。 | 入口ID（可選） |

## [!DNL Identity Service]

下表概述Adobe Experience Platform的量度 [!DNL Identity Service]。

| 前瞻分析度量  | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 一個資料集或所有資料集寫入 [!DNL Identity Service]到其資料源的記錄數。 | 資料集ID（選用） |
| timeseries.identity.dataset.recordfailed.count | 失敗的記錄數 [!DNL Identity Service]，對於一個資料集或所有資料集。 | 資料集ID（選用） |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 成功接收命名空間的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 名稱空間失敗的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空間跳過的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 儲存在IMS組織身分圖表中的獨特身分數。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 名稱空間的識別圖中儲存的獨特身份數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | 儲存在IMS組織之識別圖中的唯一圖形識別數。 | 不適用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS組織在識別圖中針對特定圖形強度（「未知」、「弱」或「強」）儲存的獨特身分數。 | 圖形強度(**必要**) |

## [!DNL Privacy Service]

下表概述Adobe Experience Platform的量度 [!DNL Privacy Service]。

| 前瞻分析度量  | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 從GDPR建立的工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.completedjobs.count | 來自GDPR的已完成工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.errorjobs.count | 來自GDPR的錯誤工作總數。 | ENV(必&#x200B;**要**) |

## [!DNL Query Service]

下表概述Adobe Experience Platform的量度 [!DNL Query Service]。

| 前瞻分析度量  | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非週期性排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.scheduledrecurring.count | 循環排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.batchquery.count | 執行的批次查詢總數。 | 不適用 |
| timeseries.queryservice.query.scheduledquery.count | 已執行的計畫查詢總數。 | 不適用 |
| timeseries.queryservice.query.interactivequery.count | 執行的互動式查詢總數。 | 不適用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 來自PSQL的已執行批次查詢總數。 | 不適用 |

## [!DNL Real-time Customer Profile]

下表概述的量度 [!DNL Real-time Customer Profile]。

| 前瞻分析度量  | 說明 | ID查詢參數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 從中讀取的記錄數 [!DNL Data Lake] 量，對於 [!DNL Profile]一個資料集或所有資料集。 | 資料集ID（選用） |
| timeseries.profiles.dataset.recordsuccess.count | 通過、對一個資料集或所有資料集 [!DNL Profile]寫入其資料源的記錄數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.recordfailed.count | 失敗的記錄數 [!DNL Profile]，對於一個資料集或所有資料集。 | 資料集ID（選用） |
| timeseries.profiles.dataset.batchsuccess.count | 資料集 [!DNL Profile] 或所有資料集所吸收的批次數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.batchfailed.count | 一個資料 [!DNL Profile] 集或所有資料集的批次數失敗。 | 資料集ID（選用） |
| platform.ups.ingest.streaming.request.m1_rate | 傳入請求率。 | IMS組織 |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 擷取成功率。 | IMS組織 |
| platform.ups.ingest.streaming.records.created.m15_rate | 資料集新記錄的吸收率。 | 資料集ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 為資料集建立請求的順序錯誤時間戳記記錄的比率。 | 資料集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 資料集上次建立記錄要求的時間戳記。 | 資料集ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 資料集更新請求的順序錯誤時間戳記記錄比率。 | 資料集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 資料集上次更新記錄要求的時間戳記。 | 資料集ID |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均記錄大小。 | IMS組織 |
| platform.ups.ingest.streaming.records.updated.m15_rate | 針對資料集所收錄記錄的更新請求率。 | 資料集ID |
