---
keywords: Experience Platform；故障排除；護欄；指導方針；
title: 用於資料接收的護欄
description: 本檔案就Adobe Experience Platform資料接收的護欄提供指導
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 582f6ffdea6fa1978f6af6f0f0f92e50a12f6200
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# 用於資料接收的護欄

護欄是指為資料和系統使用、效能優化和避免錯誤或意外結果在Adobe Experience Platform提供指導的閾值。 護欄可以參考您對許可權利的使用或資料的使用和處理。

本檔案就Adobe Experience Platform資料接收的護欄提供指導。

## 批量攝取護欄

下表概述了使用 [批處理接收API](./batch-ingestion/overview.md) 或源：

| 攝取類型 | 準則 | 附註 |
| --- | --- | --- |
| 使用批量攝取API的資料湖攝取 | <ul><li>使用批處理接收API，您每小時可向資料湖接收多達20 GB的資料。</li><li>每批的最大檔案數為1500。</li><li>最大批大小為100 GB。</li><li>每行的最大屬性或欄位數為10000。</li><li>每個用戶每分鐘的最大批次數為138。</li></ul> |
| 使用批源的資料湖攝取 | <ul><li>您每小時可使用批處理接收源(如 [!DNL Azure Blob]。 [!DNL Amazon S3], [!DNL SFTP]。</li><li>批大小應介於256 MB和100 GB之間。</li><li>每批的最大檔案數為1500。</li></ul> | 查看 [源概述](../sources/home.md) 用於資料接收的源目錄。 |
| 批接收到配置檔案 | <ul><li>記錄類的最大大小為100 KB（軟）。</li><li>ExperienceEvent類的最大大小為10 KB（軟）。</li><li>單個記錄的最大大小為1 MB。</li></ul> |
| 每天接收的Profile或ExperienceEvent批數 | **每天接收的Profile或ExperienceEvent批的最大數量為90。** 這意味著每天接收的Profile和ExperienceEvent批的合計不能超過90。 接收附加批將影響系統效能。 | 這是軟極限。 可以超出軟限制，但是軟限制為系統效能提供了建議的准則。 |

## 用於流式攝取的護欄

下表概述了使用 [流式接收API](./streaming-ingestion/overview.md) 或流源：

| 攝取類型 | 準則 | 附註 |
| --- | --- | --- |
| 串流擷取 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>您每秒最多可處理2500個對Profile的請求。</li><li>在15分鐘內，您每秒最多可處理20000個資料湖請求。</li></ul> | 如果需要更高的資料吞吐量，請使用批接收API。 |
| 流源 | <ul><li>最大記錄大小為1 MB，建議大小為10 KB。</li><li>在建立新源連接時，流源每秒支援4000到5000個請求。 **注釋**:流式資料要完全處理到資料湖，最多需要30分鐘。</li><li>您每秒可以處理4000到5000個資料湖請求。 **注釋**:流式資料要完全處理到資料湖，最多需要30分鐘。</li></ul> | 流源，如 [!DNL Kafka]。 [!DNL Azure Event Hubs], [!DNL Amazon Kinesis] 不使用 [!DNL Data Collection Core Service] (DCCS)路由，可以有不同的吞吐量限制。 查看 [源概述](../sources/home.md) 用於資料接收的源目錄。 |

## 後續步驟

有關Experience Platform中的資料和處理護欄的詳細資訊，請參閱以下文檔：

* [即時客戶配置檔案資料的護欄](../profile/guardrails.md)
* [Identity Service資料的護欄](../identity-service/guardrails.md)
