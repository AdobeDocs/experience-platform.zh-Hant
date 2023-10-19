---
title: Adobe Experience Platform Debugger發行說明
description: Adobe Experience Platform Debugger 的最新發行說明。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；發行說明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 70abe974aa7f94ea172d7ab90aacaf765b88de0e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 4%

---

# Adobe Experience Platform Debugger發行說明

## 1.5.0版 — 2023年10月19日

### 新功能

* 在標籤摘要和記錄中顯示屬性、環境和規則的連結。

### 修正和改良

* 修正未傳送標籤摘要資料的問題。
* 修正保證工作階段會產生CORS錯誤的問題
* 修正無法顯示Target追蹤的問題。
* 修正「傳送意見回饋」按鈕。
* 修正≥2.18.0版Web SDK摘要中缺少「資料串流ID」的問題。
* 修正無法搜尋Edge記錄檔的問題。
* 新增特定帳戶型別其他設定檔的相關備註。

## 1.4.1版 — 2022年11月1日

* 已改進具有許多Adobe Experience Platform保證事件的頁面效能。

## 1.4.0版 — 2022年10月3日

* 新增Web SDK混合實作的AEP保證偵錯支援。
* 在同一AEP保證工作階段中新增支援多個標籤。
* 修正使用者在登入後無法切換設定檔/組織的問題。
   * 對於某些帳戶，需要登出並重新登入才能切換組織。
* 新增啟用Target追蹤失敗時的錯誤訊息。
* 更新相依性。

## 1.3.3版 — 2022年6月20日

* 修正無法從網路事件表格開啟快顯視窗的問題。
* 修正無法載入頁面上Alloy資訊的問題。

## 1.3.2版 — 2022年6月9日

* 新增使用者登入時的預設頭像。
* 為記錄中的JSON物件新增語法醒目提示。

## 1.3.1版 — 2022年5月24日

* 更新相依性。
* 修正無法啟用處理後點選的Analytics問題。
* 修正除錯工具附加至Adobe登入視窗的問題。
* 修正AT.js中記錄訊息無法在Debugger中顯示的問題。

## 1.3.0版 — 2022年1月28日

* 新增「關於」連結以顯示最新發行版本和說明。
* 新增切換功能，可檢視Analytics請求的處理後點選。 Analytics區段提供此切換選項。
* 修正在偵錯工具外部關閉工作階段時的遠端偵錯工作階段問題。
* 修正Web SDK Edge Transactions索引標籤中顯示的錯誤通知。
* 修正偵錯工具存取_satellite物件時，頁面出現棄用警告的Adobe標籤。
* 修正在頁面上找不到AppMeasurement執行個體的某些情況。
* 修正第一次開啟偵錯工具視窗時發生的頁面連線問題。

## 1.2.0版 — 2021年10月26日

* 顯示網路檢視中所有瀏覽器標籤的事件。 若只要檢視目前標籤中的事件，請選取Debugger右下角的鎖定圖示。
* 更新品牌。

## 1.1.0版 — 2021年10月5日

* 遠端偵錯視覺效果 — 將遠端偵錯事件組織成Adobe Experience Platform Web SDK > Edge Transactions區段中的視覺流程圖。
* 啟動新的遠端偵錯工作階段時，需要頁面上使用的Adobe Experience Platform Web SDK組織與登入的組織相符。
* 僅顯示已連線標籤的邊緣交易。 仍可在「記錄> Edge」區段中取得Target追蹤記錄。
* 允許頁面上每個Adobe Experience Platform Web SDK執行個體的個別資料流ID設定覆寫。 新增偵錯功能切換。
* 修正Adobe Target追蹤權杖不一定會與Adobe Experience Platform Web SDK的遠端偵錯工作階段一併傳送的問題。

## 1.0.0版（2021年5月5日）

* Experience Platform Debugger的第一個主要版本。 旨在取代Experience Cloud Debugger。
