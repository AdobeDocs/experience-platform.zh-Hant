---
keywords: Experience Platform；疑難排解；護欄；准則；
title: 資料擷取的護欄
description: 本檔案提供Adobe Experience Platform中資料擷取護欄的相關指引
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 96ab28f9f909cedd1148d6b27610aebb7cf61b29
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 資料擷取的護欄

護欄是提供資料和系統使用、效能最佳化以及避免錯誤或意外結果在Adobe Experience Platform中的指引的閾值。 護欄可以參照與您的授權權限相關的資料和處理的使用或耗用量。

本檔案提供Adobe Experience Platform中資料擷取護欄的相關指引。

## 批次內嵌的護欄

下表列出使用 [批次內嵌API](./batch-ingestion/overview.md) 或來源：

| 擷取類型 | 準則 | 附註 |
| --- | --- | --- |
| 使用批次內嵌API進行資料湖內嵌 | <ul><li>您可以使用批次內嵌API，每小時將最多20 GB的資料內嵌至Data Lake。</li><li>每批檔案的最大數量為1500。</li><li>最大批大小為100 GB。</li><li>每列的屬性或欄位數上限為10000。</li><li>每個用戶每分鐘的批次數上限為138。</li></ul> |
| 使用批次來源擷取資料湖 | <ul><li>您可以使用批次擷取來源(例如 [!DNL Azure Blob], [!DNL Amazon S3]，和 [!DNL SFTP].</li><li>批大小應介於256 MB和100 GB之間。</li><li>每批檔案的最大數量為1500。</li></ul> | 請參閱 [來源概觀](../sources/home.md) 用於資料擷取的來源目錄。 |
| 批次內嵌至設定檔 | <ul><li>記錄類的最大大小為100 KB（軟）。</li><li>ExperienceEvent類別的最大大小為10 KB（軟式）。</li><li>單個記錄的最大大小為1 MB。</li></ul> |
| 每日擷取的設定檔或ExperienceEvent批次數 | **每日擷取的Profile或ExperienceEvent批次數上限為90。** 這表示每天擷取的Profile和ExperienceEvent批次總計不得超過90個。 接收其他批次將影響系統效能。 | 這是軟限制。 但是，軟限制可以超出軟限制，為系統效能提供建議的准則。 |

## 串流擷取的護欄

下表列出使用 [串流獲取API](./streaming-ingestion/overview.md) 或串流來源：

| 擷取類型 | 準則 | 附註 |
| --- | --- | --- |
| 串流擷取 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>您可以在一分鐘內每秒20000次處理對設定檔的請求。</li><li>在15分鐘內，您每秒最多可以處理20000個資料湖請求。</li></ul> | 如果您需要較高的資料吞吐量，請使用批次內嵌API。 |
| 串流來源 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>建立新源連接時，每秒支援4000到5000個請求。 **附註**:最多可能需要30分鐘，才能將串流資料完全處理至data lake。</li><li>您每秒可以處理4000到5000個資料湖請求。 **附註**:最多可能需要30分鐘，才能將串流資料完全處理至data lake。</li></ul> | 串流來源，例如 [!DNL Kafka], [!DNL Azure Event Hubs]，和 [!DNL Amazon Kinesis] 不使用 [!DNL Data Collection Core Service] (DCCS)路由，可能有不同的吞吐量限制。 請參閱 [來源概觀](../sources/home.md) 用於資料擷取的來源目錄。 |

## 後續步驟

請參閱下列檔案，以取得Experience Platform中資料和處理護欄的詳細資訊：

* [即時客戶設定檔資料的護欄](../profile/guardrails.md)
* [Identity Service資料的護欄](../identity-service/guardrails.md)
