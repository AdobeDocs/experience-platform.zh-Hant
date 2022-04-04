---
title: 服務級別協定和目標
description: 瞭解如何配置邊緣網路伺服器API的身份驗證
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: 資料收集；收集；邊緣網路；api;sla;slt;service levels;data collection;edge network;api;sla;slt;service levels
hide: true
hidefromtoc: true
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# 護欄

## 總覽 {#overview}

Adobe將利用商業上合理的努力 [!DNL Server API] 在每月計費週期中，每個區域的正常運行時間百分比至少為99.9%。

## 定義

* **可用性** 每五分鐘間隔計算一次，即體驗Adobe Experience Platform邊緣網路處理的不會因錯誤而失敗且僅與預配置的Adobe Experience Platform邊緣網路API相關的請求的百分比。 如果租戶在給定的五分鐘間隔內未發出任何請求，則該間隔被視為100%可用。
* **每月正常運行時間百分比** 對於給定區域，計算為一個月內所有五分鐘間隔的可用性平均值。
* 安 **上游** 是Adobe Edge網路後面的服務，可用於特定的資料流，如Adobe伺服器端轉發、Adobe Edge分段或Adobe Target。
* A **請求** 發送到伺服器API的請求被定義為一個或多個請求單元。
* A **請求單元** 對應於請求的8 KB片段和為資料流配置的上游。
* 安 **錯誤** 是因Adobe Experience Platform邊緣網路而失敗的任何請求 [內部服務錯誤](error-handling.md)。

## 內部目標

Adobe工程團隊部署接近即時遙測、監控和擴展程式，以確保實現以下目標：

* 返回的HTTP請求不到1% `5xx` 過去5分鐘中的錯誤
* 不到1%的上游連接在過去五分鐘內返回錯誤
* 任何租戶容量在達到限制後不到10分鐘內增加一倍。

## 服務級別協定排除

上述服務級別承諾不適用於以下事件導致的任何不可用或效能問題：

* 超出我們合理控制範圍的因素，包括網際網路接入或Adobe基礎設施之外的相關問題。
* 任何濫用 [!DNL Server API]，如下面列出的限制所定義。

## 服務限制

所有資料流都強制實施某些使用限制，這主要控制可併發發送的事件數、事件大小以及這些請求路由到的上游服務的數量。

### 請求單位

所有限值都在 **請求單元(RU)**，定義為 **8 KB片段** 請求到資料流中配置的一個上游服務。

#### 範例

| 按資料流配置的上流 | 平均請求大小 | 請求單位 |
| --- | --- | --- |
| 1(Adobe平台) | 8 KB（1段） | 1 |
| 2(《Adobe綱要》，Adobe Target) | 8 KB（1段） | 2 |
| 2(《Adobe綱要》，Adobe Target) | 16 KB（2個片段） | 4 |
| 2(《Adobe綱要》，Adobe Target) | 64 KB（8個碎片） | 16 |

### 請求單位限制

下表顯示了預設限制值。 如果您需要更高的請求單位限制，請聯繫您的客戶代表。

| 端點 | 每秒請求數 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### HTTP請求大小限制

| 負載格式 | 請求的最大大小 | 最大8 KB請求片段 |
| --- | --- | --- |
| JSON純文字檔案 | 64 KB | 8 |


>[!NOTE]
>
>根據負載本身，二進位格式通常比純文字檔案JSON中壓縮20-40%。 如果您需要更高的資料流容量，請聯繫您的客戶服務代表。

