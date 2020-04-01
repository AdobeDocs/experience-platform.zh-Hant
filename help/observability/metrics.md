---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用量度
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# 可用度量清單

以下是「可觀性前瞻分析」所公開的量度清單，每個量度都包含其相關的平台服務、說明和接受的ID查詢參數。

| 前瞻分析度量 | 平台服務 | 說明 | ID查詢參數 |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 資料擷取 | 建立的資料集總數。 | 不適用 |
| timeseries.ingestion.dataset.size | 資料擷取 | 針對一個資料集或所有資料集所擷取的所有資料累積大小。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.dailysize | 資料擷取 | 針對一個資料集或所有資料集，依每日使用量而擷取的資料大小。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.batchfailed.count | 資料擷取 | 一個資料集或所有資料集的批處理失敗數。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.batchsuccess.count | 資料擷取 | 針對一個資料集或所有資料集所吸收的批次數。 | 資料集ID（選用） |
| timeseries.ingestion.dataset.recordsuccess.count | 資料擷取 | 一個資料集或所有資料集所吸收的記錄數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.total.messages.rate | 資料擷取（串流） | 一個資料集或所有資料集的消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.valid.messages.rate | 資料擷取（串流） | 一個資料集或所有資料集的有效消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.invalid.messages.rate | 資料擷取（串流） | 一個資料集或所有資料集的無效消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.type.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「類型」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.range.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「範圍」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.format.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「格式」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.pattern.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「模式」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.presence.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「存在」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.enum.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「列舉」訊息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.unclassified.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「未分類」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.validation.category.unknown.count | 資料擷取（串流） | 一個資料集或所有資料集的無效「未知」消息總數。 | 資料集ID（選用） |
| timeseries.data.collection.inlet.total.messages.received | 資料擷取（串流） | 為一個資料入口或所有資料入口接收的消息總數。 | 入口ID（可選） |
| timeseries.data.collection.inlet.total.messages.size.received | 資料擷取（串流） | 為一個資料入口或所有資料入口接收的資料的總大小。 | 入口ID（可選） |
| timeseries.data.collection.inlet.success | 資料擷取（串流） | 成功呼叫一個資料入口或所有資料入口的HTTP呼叫總數。 | 入口ID（可選） |
| timeseries.data.collection.inlet.failure | 資料擷取（串流） | 對一個資料入口或所有資料入口的失敗HTTP呼叫總數。 | 入口ID（可選） |
| timeseries.profiles.dataset.recorgar.count | 即時客戶個人檔案 | 依「設定檔」、一個資料集或所有資料集從資料湖讀取的記錄數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.recordsuccess.count | 即時客戶個人檔案 | 按配置檔案、一個資料集或所有資料集寫入其資料源的記錄數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.recordfailed.count | 即時客戶個人檔案 | 「配置檔案」、一個資料集或所有資料集失敗的記錄數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.batchsuccess.count | 即時客戶個人檔案 | 資料集或所有資料集所吸收的描述檔批次數。 | 資料集ID（選用） |
| timeseries.profiles.dataset.batchfailed.count | 即時客戶個人檔案 | 一個資料集或所有資料集的配置檔案批次數失敗。 | 資料集ID（選用） |
| timeseries.identity.dataset.recordsuccess.count | Identity 服務 | Identity Service針對一個資料集或所有資料集寫入其資料來源的記錄數。 | 資料集ID（選用） |
| timeseries.identity.dataset.recordfailed.count | Identity 服務 | Identity Service、一個資料集或所有資料集失敗的記錄數。 | 資料集ID（選用） |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Identity 服務 | 成功接收命名空間的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Identity 服務 | 名稱空間失敗的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.dataset.namespacecode.recordkipped.count | Identity 服務 | 命名空間跳過的身份記錄數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.uniqueidentity.count | Identity 服務 | 儲存在IMS組織身分圖表中的獨特身分數。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentity.count | Identity 服務 | 名稱空間的識別圖中儲存的獨特身份數。 | 命名空間ID(**必要**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Identity 服務 | 儲存在IMS組織之識別圖中的唯一圖形識別數。 | 不適用 |
| timeseries.identity.graph.imsorg.graphthent.uniqueidentity.count | Identity 服務 | IMS組織在識別圖中針對特定圖形強度（「未知」、「弱」或「強」）儲存的獨特身分數。 | 圖形強度(**必要**) |
| timeseries.gdpr.jobs.totaljobs.count | GDPR | 從GDPR建立的工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR | 來自GDPR的已完成工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR | 來自GDPR的錯誤工作總數。 | ENV(必&#x200B;**要**) |
| timeseries.queryservice.query.scheduleonce.count | 查詢服務 | 非週期性排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.scheduledring.count | 查詢服務 | 循環排程查詢的總數。 | 不適用 |
| timeseries.queryservice.query.batchquery.count | 查詢服務 | 執行的批次查詢總數。 | 不適用 |
| timeseries.queryservice.query.scheduledquery.count | 查詢服務 | 已執行的計畫查詢總數。 | 不適用 |
| timeseries.queryservice.query.interactivequery.count | 查詢服務 | 執行的互動式查詢總數。 | 不適用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 查詢服務 | 來自PSQL的已執行批次查詢總數。 | 不適用 |