---
keywords: Experience Platform；疑難排解；護欄；指南；
title: 資料擷取的護欄
description: 本文提供Adobe Experience Platform中資料擷取護欄的相關指示
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4debc301b930643565b25218f4822a67e88063bb
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# 資料擷取的護欄

護欄是臨界值，可為Adobe Experience Platform中的資料和系統使用、效能最佳化，以及避免錯誤或意外結果提供指引。 護欄可指您與授權權益相關的資料使用或消費與處理。

本文提供Adobe Experience Platform中資料擷取護欄的相關指示。

## 批次擷取的護欄

下表概述使用時需考慮的護欄 [批次擷取API](./batch-ingestion/overview.md) 或來源：

| 擷取型別 | 準則 | 附註 |
| --- | --- | --- |
| 使用批次擷取API擷取資料湖 | <ul><li>您可以使用批次擷取API，每小時可擷取最多20 GB的資料至Data Lake。</li><li>每個批次的最大檔案數為1500。</li><li>最大批次大小為100 GB。</li><li>每列的屬性或欄位數上限為10000。</li><li>每分鐘每個使用者的批次數量上限為138。</li></ul> |
| 使用批次來源擷取資料湖 | <ul><li>您可以使用批次擷取來源（例如），每小時將高達200 GB的資料擷取至資料湖 [!DNL Azure Blob]， [!DNL Amazon S3]、和 [!DNL SFTP].</li><li>批次大小應介於256 MB和100 GB之間。 這同時適用於未壓縮和壓縮的資料。 若在資料湖中解壓縮壓縮壓縮的資料，將套用這些限制。</li><li>每個批次的最大檔案數為1500。</li></ul> | 請參閱 [來源概觀](../sources/home.md) 如需可用於資料內嵌的來源目錄。 |
| 批次內嵌至設定檔 | <ul><li>記錄類別的大小上限為100 KB （可變）。</li><li>ExperienceEvent類別的大小上限為10 KB （可變）。</li><li>單一記錄的大小上限為1 MB。</li></ul> |
| 每天擷取的設定檔或ExperienceEvent批次數量 | **每天最多可擷取90個Profile或ExperienceEvent批次。** 這表示每天擷取的Profile和ExperienceEvent批次總數不能超過90。 擷取其他批次將會影響系統效能。 | 這是軟性限制。 雖然可能會超過軟性限制，但軟性限制提供系統效能的建議指引。 |

## 串流擷取的護欄

閱讀 [串流擷取概觀](./streaming-ingestion/overview.md) 以取得串流擷取的護欄相關資訊。

## 串流來源的護欄

下表概述使用串流來源時應考慮的護欄：

| 擷取型別 | 準則 | 附註 |
| --- | --- | --- |
| 串流來源 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>串流來源在建立新的來源連線時，支援的請求量為每秒4000到5000個。 **注意**：串流資料可能需要30分鐘的時間才能完全處理至Data Lake。</li><li>您可以每秒處理4000到5000個對Data Lake的請求。 **注意**：串流資料可能需要30分鐘的時間才能完全處理至Data Lake。</li></ul> | 串流來源，例如 [!DNL Kafka]， [!DNL Azure Event Hubs]、和 [!DNL Amazon Kinesis] 請勿使用 [!DNL Data Collection Core Service] (DCCS)路由，而且可以有不同的輸送量限制。 請參閱 [來源概觀](../sources/home.md) 如需可用於資料內嵌的來源目錄。 |

## 後續步驟

請參閱下列檔案，深入瞭解其他Experience Platform服務護欄、端對端延遲資訊，以及Real-Time CDP產品說明檔案的授權資訊：

* [Real-Time CDP護欄](/help/rtcdp/guardrails/overview.md)
* [端對端延遲圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用於各種Experience Platform服務。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate套件）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
