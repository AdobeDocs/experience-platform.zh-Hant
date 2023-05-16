---
description: 了解Experience Platform如何處理串流目的地傳回的不同錯誤類型，以及如何重試將資料傳送至目的地平台。
title: 針對使用Destination SDK構建的流目的地的速率限制和重試策略
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 針對使用Destination SDK構建的流目的地的速率限制和重試策略

合作夥伴構建的目標可能返回各種錯誤，並且具有不同的限速策略。 本頁說明Experience Platform如何處理串流目的地傳回的不同錯誤類型。

使用Destination SDK配置目標時，您可以在兩種聚合類型之間進行選擇 —  [最佳成果匯總](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 [可配置聚合](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). 根據您選擇的聚合類型，請閱讀以下Experience Platform如何處理錯誤和速率限制的內容。

## 最佳成果匯總 {#best-effort-aggregation}

對於對您的目的地進行的任何HTTP呼叫失敗，Experience Platform會在第一次呼叫後再次嘗試進行呼叫。 如果第二次嘗試時呼叫仍然失敗，Experience Platform會中斷呼叫，而不會第三次重新嘗試。

## 可配置聚合 {#configurable-aggregation}

在以可配置聚合設定的目標平台情況下，Experience Platform會區分您的平台返回的錯誤類型：

* Experience Platform重試將資料傳送至您的平台時發生錯誤：
   * HTTP回應代碼420和429
   * 大於500的HTTP響應代碼
* 錯誤Experience Platform *不* 重試將資料發送到您的平台：平台返回的所有其他

### 說明的重試方法 {#retry-approach}

下面描述了可配置聚合的Experience Platform方法。 此範例假設Experience Platform每分鐘收到超過50,000個請求時，會傳送資料至開始傳回429錯誤碼的目的地平台：

* 第1分鐘：Experience Platform使用設定檔匯總40,000個批次，以傳送至您的目的地平台。 Experience Platform發出40k HTTP要求，且全部成功。
* 第2分鐘：Experience Platform使用設定檔匯總70,000個批次，以傳送至您的目的地平台。 Experience Platform發出70k HTTP要求，而50k成功。 其他20k會收到端點傳來的速率限制錯誤，並將在30分鐘內重新嘗試。
* 第3分鐘：Experience Platform使用設定檔匯總30,000個批次，以傳送至您的目的地平台。 Experience Platform發出30k HTTP要求，且全部成功。
* ...
* ...
* 第32分鐘：Experience Platform會重新嘗試傳送在第2分鐘失敗的20,000個批次。 所有呼叫都成功。

## 後續步驟 {#next-steps}

您現在可以了解Experience Platform如何處理來自目標平台的錯誤和速率限制，具體取決於您在配置流目標時選擇的聚合策略。 接下來，您可以檢閱下列檔案：

* [測試您的目標配置](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交以審核在Destination SDK中創作的目標](../guides/submit-destination.md)
