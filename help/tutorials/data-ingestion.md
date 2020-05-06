---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料擷取教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 將資料內嵌至Experience Platform

Adobe Experience Platform將來自多個來源的資料匯集在一起，以協助行銷人員更好地瞭解客戶的行為。 Adobe Experience Platform資料擷取代表平台從這些來源擷取資料的多種方法，以及該資料如何保存在資料湖中，以供下游平台服務使用。 資料擷取包括批次擷取、串流擷取，以及使用來源連接器擷取。 若要進一步瞭解，請閱讀「資 [料擷取」概觀](../ingestion/home.md) ，或直接前往 [Sources檔案](../sources/home.md)。

## 在UI和API中建立來源連接器

來源連接器可讓您從多個來源擷取資料，然後在這些來源使用平台服務加以標籤、結構化和增強。 要開始建立源連接器，請參閱源 [概述](../sources/home.md)。

## 收錄批次資料

Adobe Experience Platform可讓您輕鬆將資料匯入Platform做為批次檔案。 要提取的資料示例可以包括來自CRM系統中的平面檔案（如鑲木地板檔案）的概要檔案資料或符合模式註冊表中已知的體驗資料模型(XDM)模式的資料。 若要開始，請造訪將擷取 [資料匯入Platform教學課程](../ingestion/tutorials/ingest-batch-data.md)。

## 將CSV檔案對應至XDM架構

若要將CSV資料內嵌至Adobe Experience Platform，資料必須對應至Experience Data Model(XDM)架構。 如需說明如何使用Experience Platform使用者介面將CSV檔案對應至XDM架構的步驟，請遵循將 [CSV檔案對應至XDM架構教學課程](../ingestion/tutorials/map-a-csv-file.md)。

## 建立串流連線

若要開始將資料串流至Experience Platform，您必須先要求HTTP端點。 您可以選擇設定此端點，以強制執行已驗證的行為。 這可以使用Platform使用者介面或Experience Platform API來完成。 若要進一步瞭解，請依照教學課 [程，使用UI建立串流連線](../ingestion/tutorials/create-streaming-connection-ui.md) ，或 [使用API建立串流連線](../ingestion/tutorials/create-streaming-connection.md)。

## 建立驗證的串流連線

「已驗證的資料收集」可讓Adobe Experience Platform服務（例如即時客戶個人檔案和身分識別）區隔來自受信任來源和不受信任來源的記錄。 若要開始，請依照教學課程來建 [立已驗證的串流連線](../ingestion/tutorials/create-authenticated-streaming-connection.md)。

## 串流記錄和時間序列資料

有了資料集和串流連線，您就可以將記錄或時間系列資料串流至平台。 若要開始串流記錄資料，請依照串 [流記錄資料進入平台教學課程](../ingestion/tutorials/streaming-record-data.md)。 若要開始串流時間系列資料，請依 [循串流時間系列資料進入Platform](../ingestion/tutorials/streaming-time-series-data.md)。

## 在單一HTTP請求中串流多個訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫的成本可能很高。 例如，建立1KB負載的200個HTTP請求，而不是建立1KB負載的200個HTTP請求，建立200個每個1KB訊息的1HTTP請求，而且單一負載為200KB，效率更高。 正確使用時，在單一要求內將多個訊息分組是最佳化傳送至Experience Platform之資料的絕佳方式。 若要瞭解如何使用串流擷取功能，在單一HTTP要求內傳送多則訊息至Experience Platform，請遵循傳送多 [則訊息教學課程](../ingestion/tutorials/streaming-multiple-messages.md)。



