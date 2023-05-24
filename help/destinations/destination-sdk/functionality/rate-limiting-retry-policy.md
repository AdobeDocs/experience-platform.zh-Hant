---
description: 瞭解Experience Platform如何處理流目標返回的不同類型的錯誤，以及如何重試將資料發送到目標平台。
title: 用於使用Destination SDK構建的流目標的速率限制和重試策略
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 用於使用Destination SDK構建的流目標的速率限制和重試策略

合作夥伴構建的目標可能返回各種錯誤，並且有不同的速率限制策略。 本頁說明Experience Platform如何處理流目標返回的不同類型的錯誤。

使用Destination SDK配置目標時，可以在兩種聚合類型之間進行選擇 —  [最佳工作聚合](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 [可配置聚合](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)。 根據您選擇的聚合類型，請閱讀下面的Experience Platform處理錯誤和速率限制的方式。

## 盡力聚合 {#best-effort-aggregation}

對於向目標發出的任何HTTP調用失敗，Experience Platform會嘗試在第一次調用後立即再次進行調用。 如果第二次嘗試時呼叫仍然失敗，Experience Platform將放棄呼叫，並且不再再次嘗試。

## 可配置聚合 {#configurable-aggregation}

在使用可配置聚合設定目標平台的情況下，Experience Platform可區分平台返回的錯誤類型：

* Experience Platform重試將資料發送到您的平台時出錯：
   * HTTP響應代碼420和429
   * 大於500的HTTP響應代碼
* Experience Platform *不* 請重試將資料發送到您的平台：平台返回的所有其他

### 描述的重試方法 {#retry-approach}

下面介紹了用於可配置聚合的Experience Platform方法。 此示例假定Experience Platform將資料發送到目標平台，該平台在每分鐘接收超過50k請求時開始返回429個錯誤代碼：

* 第1分鐘：Experience Platform將40k批與配置檔案聚合，以發送到目標平台。 Experience Platform發出40k HTTP請求，所有請求都成功。
* 第2分鐘：Experience Platform將70k批與配置檔案聚合，以發送到目標平台。 Experience Platform使70k HTTP請求和50k請求成功。 另外20k從您的終結點接收速率限制錯誤，將在30分鐘內重試。
* 第3分鐘：Experience Platform將30k批與配置檔案聚合，以發送到目標平台。 Experience Platform發出30k HTTP請求，所有請求都成功。
* ...
* ...
* 第32分鐘：Experience Platform重新嘗試發送在第2分鐘失敗的20k批。 所有呼叫都成功。

## 後續步驟 {#next-steps}

您現在知道Experience Platform如何處理目標平台中的錯誤和速率限制，具體取決於配置流目標時選擇的聚合策略。 接下來，您可以查看以下文檔：

* [Test目標配置](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交以審閱在Destination SDK中創作的目標](../guides/submit-destination.md)
