---
audience: user
user-guide-title: Adobe Experience Platform 資料擷取說明
breadcrumb-title: Data Ingestion 指南
user-guide-description: 透過批次或串流擷取，將您的資料匯入 Experience Platform。
feature: Data Ingestion
role: Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 21%

---


# Adobe Experience Platform資料擷取 {#ingestion}

- [資料擷取概觀](home.md)
- 串流擷取{#streaming}
   - [概觀](streaming-ingestion/overview.md)
   - [Kafka聯結器](streaming-ingestion/kafka.md)
   - [疑難排解](streaming-ingestion/troubleshooting.md)
- 批次內嵌{#batch}
   - [批次擷取API快速入門](batch-ingestion/getting-started.md)
   - [API總覽](batch-ingestion/overview.md)
   - [API開發人員指南](batch-ingestion/api-overview.md)
   - [部分批次擷取](batch-ingestion/partial.md)
   - [疑難排解](batch-ingestion/troubleshooting.md)
- 教學課程 {#tutorials}
   - 將CSV檔案對應至XDM {#map-csv}
      - [概觀](./tutorials/map-csv/overview.md)
      - [將CSV檔案對應到現有結構描述](./tutorials/map-csv/existing-schema.md)
      - [使用AI產生的建議對應CSV檔案](./tutorials/map-csv/recommendations.md)
   - [使用UI內嵌批次資料](tutorials/ingest-batch-data.md)
   - [建立已驗證的串流連線](tutorials/create-authenticated-streaming-connection.md)
   - [建立串流連線(API)](tutorials/create-streaming-connection.md)
   - [建立串流連線(UI)](tutorials/create-streaming-connection-ui.md)
   - [串流記錄資料](tutorials/streaming-record-data.md)
   - [串流時間序列資料](tutorials/streaming-time-series-data.md)
   - [串流多則訊息](tutorials/streaming-multiple-messages.md)
- 資料品質和監視{#quality}
   - [概觀](quality/overview.md)
   - [監視資料擷取](quality/monitor-data-ingestion.md)
   - [擷取錯誤診斷](quality/error-diagnostics.md)
   - [擷取失敗的批次](quality/retrieve-failed-batches.md)
   - [串流擷取驗證](quality/streaming-validation.md)
- [資料擷取的護欄](guardrails.md)
- [Source聯結器](source-connectors.md)
- [批次擷取API參考](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [串流擷取API參考](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience Platform 發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/release-notes/latest)
