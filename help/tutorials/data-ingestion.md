---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料擷取教學課程
topic-legacy: tutorial
type: Tutorial
description: 資料擷取包括批次擷取、串流擷取，以及使用來源連接器擷取。
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 4%

---

# 將資料內嵌至[!DNL Experience Platform]

Adobe Experience Platform 將來自多個來源的資料彙集在一起，以協助行銷人員進一步瞭解客戶的行為。Adobe[!DNL Experience Platform Data Ingestion]表示[!DNL Platform]從這些來源擷取資料的多種方法，以及該資料如何保存在資料湖中以供下游[!DNL Platform services]使用。 [!DNL Data Ingestion] 包括批次擷取、串流擷取，以及使用來源連接器擷取。如需詳細資訊，請閱讀[資料擷取概觀](../ingestion/home.md)，或直接前往[Sources檔案](../sources/home.md)。

## 在UI和API中建立來源連線

來源連接器可讓您從多個來源擷取資料，然後在這些來源使用[!DNL Platform services]加以標籤、結構化和增強。 要開始建立源連接器，請參閱[源概述](../sources/home.md)。

## 收錄批次資料

Adobe Experience Platform可讓您輕鬆將資料匯入至[!DNL Platform]為批次檔案。 要提取的資料示例可以包括來自CRM系統中的平面檔案（如Parce檔案）或符合模式註冊表中已知[!DNL Experience Data Model](XDM)模式的資料的配置檔案資料。 若要開始，請造訪[擷取資料至平台教學課程](../ingestion/tutorials/ingest-batch-data.md)。

## 將CSV檔案對應至XDM架構

為了將CSV資料內嵌至Adobe Experience Platform，資料必須對應至[!DNL Experience Data Model](XDM)架構。 有關如何使用[!DNL Experience Platform]用戶介面將CSV檔案映射到XDM架構的步驟，請遵循[將CSV檔案映射到XDM架構教程](../ingestion/tutorials/map-a-csv-file.md)。

## 建立串流連線

若要開始將資料串流至[!DNL Experience Platform]，您必須先要求HTTP端點。 您可以選擇設定此端點，以強制執行已驗證的行為。 這可以使用[!DNL Platform]使用者介面或[!DNL Experience Platform] API來完成。 若要進一步瞭解，請依照[使用UI](../ingestion/tutorials/create-streaming-connection-ui.md)或[建立串流連線的教學課程，使用API](../ingestion/tutorials/create-streaming-connection.md)建立串流連線。

## 建立驗證的串流連線

「已驗證的資料收集」可讓[!DNL Real-time Customer Profile]和[!DNL Identity]等Adobe Experience Platform服務區隔來自受信任來源和不受信任來源的記錄。 若要開始，請依照[建立已驗證串流連線的教學課程進行。](../ingestion/tutorials/create-authenticated-streaming-connection.md)

## 串流記錄和時間序列資料

在建立資料集和串流連線後，您可以將記錄或時間系列資料串流至[!DNL Platform]。 若要開始串流記錄資料，請依照[串流記錄資料，將之放入平台教學課程](../ingestion/tutorials/streaming-record-data.md)。 若要開始串流時間系列資料，請依照[串流時間系列資料至Platform](../ingestion/tutorials/streaming-time-series-data.md)。

## 在單一HTTP請求中串流多個訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫可能會很昂貴。 例如，建立1KB負載的200個HTTP請求，而不是建立1KB負載的200個HTTP請求，建立200個每個1KB訊息的1HTTP請求，而且單一負載為200KB，效率更高。 正確使用時，將多個訊息分組在單一要求中是最佳化傳送至[!DNL Experience Platform]資料的絕佳方式。 若要瞭解如何使用串流擷取功能，在單一HTTP要求內傳送多則訊息至[!DNL Experience Platform]，請遵循[傳送多則訊息教學課程](../ingestion/tutorials/streaming-multiple-messages.md)。
