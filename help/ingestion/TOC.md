---
audience: user
user-guide-title: Adobe Experience Platform 資料擷取說明
breadcrumb-title: Data Ingestion 指南
user-guide-description: 透過批次或串流擷取，將您的資料匯入 Experience Platform。
feature: Data Ingestion
source-git-commit: f77bbc60f2bc1f12970e8050ec6a924b9713f303
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 29%

---


# Adobe Experience Platform資料擷取 {#ingestion}

- [資料擷取概觀](home.md)
- 串流擷取 {#streaming}
   - [總覽](streaming-ingestion/overview.md)
   - [Kafka連接器](streaming-ingestion/kafka.md)
   - [疑難排解](streaming-ingestion/troubleshooting.md)
- 批次擷取{#batch}
   - [批次內嵌API快速入門](batch-ingestion/getting-started.md)
   - [API 概觀](batch-ingestion/overview.md)
   - [API開發人員指南](batch-ingestion/api-overview.md)
   - [部分批次內嵌](batch-ingestion/partial.md)
   - [疑難排解](batch-ingestion/troubleshooting.md)
- 教學課程 {#tutorials}
   - 將CSV檔案對應至XDM {#map-csv}
      - [總覽](./tutorials/map-csv/overview.md)
      - [將CSV檔案對應至現有結構](./tutorials/map-csv/existing-schema.md)
      - [使用AI產生的建議對應CSV檔案](./tutorials/map-csv/recommendations.md)
   - [使用UI內嵌批次資料](tutorials/ingest-batch-data.md)
   - [建立已驗證的串流連線](tutorials/create-authenticated-streaming-connection.md)
   - [建立串流連線(API)](tutorials/create-streaming-connection.md)
   - [建立串流連線(UI)](tutorials/create-streaming-connection-ui.md)
   - [流記錄資料](tutorials/streaming-record-data.md)
   - [串流時間序列資料](tutorials/streaming-time-series-data.md)
   - [串流多則訊息](tutorials/streaming-multiple-messages.md)
- 資料品質與監控{#quality}
   - [總覽](quality/overview.md)
   - [監視資料內嵌](quality/monitor-data-ingestion.md)
   - [檢索錯誤診斷](quality/error-diagnostics.md)
   - [檢索失敗的批](quality/retrieve-failed-batches.md)
   - [串流內嵌驗證](quality/streaming-validation.md)
   - [資料擷取通知](quality/subscribe-events.md)
- [資料擷取的護欄](guardrails.md)
- [來源連接器](source-connectors.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [平台發行說明](https://www.adobe.com/go/platform-release-notes_tw)
