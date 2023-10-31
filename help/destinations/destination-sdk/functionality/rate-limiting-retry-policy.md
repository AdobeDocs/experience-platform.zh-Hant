---
description: 瞭解Experience Platform如何處理串流目的地傳回的不同錯誤型別，以及如何重試將資料傳送至目的地平台。
title: 使用Destination SDK建立的串流目的地的速率限制和重試原則
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 使用Destination SDK建立的串流目的地的速率限制和重試原則

合作夥伴建立的目的地可能會傳回各種錯誤，並有不同的速率限制原則。 此頁面說明Experience Platform如何處理串流目的地傳回的不同錯誤型別。

使用Destination SDK設定目的地時，您可以在兩種彙總型別之間選取 —  [最大努力彙總](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 [可設定的彙總](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). 根據您選取的聚總型態，請閱讀下方Experience Platform處理錯誤與比率限制的方式。

## 最大努力彙總 {#best-effort-aggregation}

對於傳送至您目的地的任何HTTP呼叫失敗，Experience Platform會嘗試在第一次呼叫後立即再次進行呼叫。 如果呼叫在第二次嘗試時仍失敗，Experience Platform會捨棄呼叫，且不會第三次重新嘗試。

## 可設定的彙總 {#configurable-aggregation}

在使用可設定的彙總設定目的地平台的情況下，Experience Platform會區分您的平台傳回的錯誤型別：

* Experience Platform重試將資料傳送至您的平台的錯誤：
   * HTTP回應代碼420和429
   * HTTP回應程式碼大於500
* Experience Platform的錯誤 *不會* 重試將資料傳送至您的平台：您的平台傳回的所有其他資料

### 描述重試方法 {#retry-approach}

可設定彙總的Experience Platform方法說明如下。 此範例假設Experience Platform傳送資料至目的地平台，且會在每分鐘收到超過50,000個請求時開始傳回429個錯誤代碼：

* 分鐘1：Experience Platform以設定檔彙總40,000批次以傳送至您的目標平台。 Experience Platform發出40,000個HTTP請求且全都成功。
* 分鐘2：Experience Platform以設定檔彙總70,000批次以傳送至您的目標平台。 Experience Platform發出70k HTTP請求並成功50k。 其他20k收到來自您端點的速率限制錯誤，將在30分鐘後重新嘗試。
* 第3分鐘：Experience Platform以設定檔彙總30,000批次以傳送至您的目標平台。 Experience Platform發出30,000個HTTP請求且全都成功。
* ...
* ...
* 第32分鐘：Experience Platform會再次嘗試傳送在第2分鐘失敗的20,000批次資料。 所有呼叫均成功。

## 後續步驟 {#next-steps}

您現在知道Experience Platform如何處理目的地平台的錯誤和速率限制，具體取決於您在設定串流目的地時選取的彙總原則。 接著，您可以檢閱下列檔案：

* [測試您的目的地設定](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交以Destination SDK撰寫的目的地，以供複查](../guides/submit-destination.md)
