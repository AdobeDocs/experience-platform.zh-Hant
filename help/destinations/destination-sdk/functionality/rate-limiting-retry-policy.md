---
description: 瞭解Experience Platform如何處理串流目的地傳回的不同錯誤型別，以及如何重試將資料傳送至目的地平台。
title: 使用Destination SDK建立的串流目的地的速率限制和重試原則
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 使用Destination SDK建立的串流目的地的速率限制和重試原則

合作夥伴建立的目的地可能會傳回各種錯誤，並有不同的速率限制原則。 本頁說明Experience Platform如何處理串流目的地傳回的不同錯誤型別。

使用Destination SDK設定目的地時，您可以在兩種彙總型別之間選取 — [最大努力彙總](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation)和[可設定的彙總](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)。 根據您選取的彙總型別，請閱讀下文Experience Platform如何處理錯誤和費率限制。

## 最大努力彙總 {#best-effort-aggregation}

Experience Platform會重試傳回下列HTTP回應代碼的呼叫： **403、408、409、429、500、502、503、504**。 會依下列時間間隔執行兩次重試：

* 首次重試嘗試： 15秒後
* 第二次重試嘗試： 30秒後

Experience Platform會&#x200B;*不*&#x200B;重試傳回其他HTTP回應代碼(例如400 （錯誤請求）的呼叫。 如果呼叫在兩次重試嘗試後仍失敗，Experience Platform會捨棄啟用，而不會重新嘗試。

您可以連絡客戶支援，為特定資料流要求不同的重試政策。

## 可設定的彙總 {#configurable-aggregation}

在使用可設定的彙總設定目的地平台的情況下，Experience Platform會區分您的平台傳回的錯誤型別：

* Experience Platform重試將資料傳送至您的平台的錯誤：
   * HTTP回應代碼420和429
   * HTTP回應程式碼大於500
* Experience Platform *未*&#x200B;重試將資料傳送至您的平台的錯誤：您的平台傳回的所有其他資料

### 描述重試方法 {#retry-approach}

適用於可設定彙總的Experience Platform方法說明如下。 此範例假設Experience Platform會傳送資料至目的地平台，且會在每分鐘收到超過50,000個請求時開始傳回429個錯誤代碼：

* 分鐘1：Experience Platform會使用要傳送至目的地平台的設定檔來彙總40,000批次資料。 Experience Platform發出40,000個HTTP請求且全都成功。
* 分鐘2：Experience Platform會使用要傳送至目的地平台的設定檔來彙總70,000批次資料。 Experience Platform發出70,000個HTTP請求並成功50,000個。 其他20k收到來自您端點的速率限制錯誤，將在30分鐘後重新嘗試。
* 第3分鐘：Experience Platform會使用要傳送至目的地平台的設定檔來彙總30,000批次資料。 Experience Platform發出30,000個HTTP請求且全都成功。
* ...
* ...
* 分鐘32：Experience Platform會再次嘗試在分鐘2傳送失敗的20,000批次資料。 所有呼叫均成功。

## 後續步驟 {#next-steps}

您現在知道Experience Platform如何處理目的地平台的錯誤和速率限制，具體取決於您在設定串流目的地時選取的彙總原則。 接著，您可以檢閱下列檔案：

* [測試您的目的地設定](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交在Destination SDK中編寫的目的地，以供檢閱](../guides/submit-destination.md)
