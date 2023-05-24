---
audience: user
user-guide-title: Adobe Experience Platform 資料擷取說明
breadcrumb-title: Data Ingestion 指南
user-guide-description: 透過批次或串流擷取，將您的資料匯入 Experience Platform。
feature: Data Ingestion
source-git-commit: 6110bf51cbd0005428e7dab4552944c5c9b54d03
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 26%

---


# Adobe Experience Platform資料接收 {#ingestion}

- [資料接收概述](home.md)
- 串流擷取 {#streaming}
   - [總覽](streaming-ingestion/overview.md)
   - [卡夫卡連接器](streaming-ingestion/kafka.md)
   - [疑難排解](streaming-ingestion/troubleshooting.md)
- 批次擷取{#batch}
   - [批處理接收API入門](batch-ingestion/getting-started.md)
   - [API 概觀](batch-ingestion/overview.md)
   - [API開發人員指南](batch-ingestion/api-overview.md)
   - [部分批量攝取](batch-ingestion/partial.md)
   - [疑難排解](batch-ingestion/troubleshooting.md)
- 教學課程 {#tutorials}
   - 將CSV檔案映射到XDM {#map-csv}
      - [總覽](./tutorials/map-csv/overview.md)
      - [將CSV檔案映射到現有架構](./tutorials/map-csv/existing-schema.md)
      - [使用AI生成的建議來映射CSV檔案](./tutorials/map-csv/recommendations.md)
   - [使用UI接收批處理資料](tutorials/ingest-batch-data.md)
   - [建立經過驗證的流連接](tutorials/create-authenticated-streaming-connection.md)
   - [建立流連接(API)](tutorials/create-streaming-connection.md)
   - [建立流連接(UI)](tutorials/create-streaming-connection-ui.md)
   - [流記錄資料](tutorials/streaming-record-data.md)
   - [流式傳輸時間序列資料](tutorials/streaming-time-series-data.md)
   - [流式處理多個消息](tutorials/streaming-multiple-messages.md)
- 資料質量和監控{#quality}
   - [總覽](quality/overview.md)
   - [監視資料內嵌](quality/monitor-data-ingestion.md)
   - [檢索錯誤診斷](quality/error-diagnostics.md)
   - [檢索失敗的批](quality/retrieve-failed-batches.md)
   - [流式接收驗證](quality/streaming-validation.md)
   - [資料接收通知](quality/subscribe-events.md)
- [用於資料接收的護欄](guardrails.md)
- [來源連接器](source-connectors.md)
- [批處理接收API參考](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [流式接收API參考](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [平台發行說明](https://www.adobe.com/go/platform-release-notes_tw)
