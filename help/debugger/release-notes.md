---
title: Adobe Experience Platform Debugger 發行說明
description: Adobe Experience Platform Debugger 的最新發行說明。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；發行說明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: a5af5c194bc6b3bf9a6e119a2f147efa85f263f0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 92%

---

# Adobe Experience Platform Debugger 發行說明

## 1.6.3版 — 2025年4月30日

### 修正和改良

* 修正Debugger無法運作DTM和Tags功能的問題。
* 修正Analytics處理後點選未出現在記錄中的問題。
* 修正日文等非ASCII語言資料在記錄中無法正確顯示的問題。

## 1.6.2版 — 2024年10月1日

### 修正和改良

* 修正Debugger對所有CSP錯誤過於敏感的問題

## 版本 1.6.1 - 2024 年 7 月 25 日

### 修正和改良

* 已修正讓使用者無法將新標記內嵌程式碼新增至沒有程式碼頁面的問題。

## 版本 1.6.0 - 2024 年 7 月 11 日

### 新功能

* 允許使用者選擇加入/退出技術和個人資料彙集。

### 修正和改良

* 修正 Firefox 指令碼插入和隱私權政策連結。
* 擷取遺失的 Analytics 請求。
* 修正含大量複雜主控台訊息的頁面損壞問題。
* 將 Adobe Experience Platform Debugger 更新為 Manifest v3 擴充功能。

## 版本 1.5.4 - 2023 年 12 月 19 日

### 修正和改良

* 修正設定未保留的問題。
* 修正查看 Analytics 處理後點閱時導致 Debugger 損壞的問題。

## 版本 1.5.3 - 2023 年 12 月 6 日

### 新功能

* 新增「開啟 Debugger 時鎖定活動標記」的設定。

### 修正和改良

* 修正私人網域上遺失 Analytics 請求的問題。
* 修正 Analytics 請求表中 Activity Map 資料遺失的問題。
* 修正查看 Target 追踨會導致當機的問題。
* 新增當 Debugger 無法在 Firefox 中設定頁面基礎結構時發出的警告。

## 版本 1.5.2 - 2023 年 11 月 10 日

(僅限 Firefox)

### 修正和改良

* 更新檔案所屬的組織。

## 版本 1.5.1 - 2023 年 11 月 2 日

### 修正和改良

* 修正 Analytics 事件被忽略或重複的問題。
* 修正超出最大狀態儲存大小的問題。
* 修正 Edge 記錄搜尋無法篩選事件的問題。

## 版本 1.5.0 - 2023 年 10 月 19 日

### 新功能

* 在標記摘要和記錄中顯示至屬性、環境和規則的連結。

### 修正和改良

* 修正標記摘要資料未發送的問題。
* 修正 Assurance 工作階段會出現 CORS 錯誤的問題
* 修正導致 Target 追踨無法出現的問題。
* 修正「送回意見回饋」按鈕。
* 修正版本 ≥2.18.0 的 Web SDK 摘要缺少「資料流 ID」。
* 修正 Edge 記錄不可搜尋的問題。
* 新增有關某些帳戶類型其他輪廓的註解。

## 版本 1.4.1 - 2022 年 11 月 1 日

* 改善含有許多 Adob&#x200B;&#x200B;e Experience Platform Assurance 事件的頁面效能。

## 版本 1.4.0 - 2022 年 10 月 3 日

* 新增對 Web SDK 混合實施的 AEP Assurance 偵錯支援。
* 新增在同一個 AEP Assurance 工作階段中對多個標籤的支援。
* 修正使用者登入後無法切換輪廓/組織的問題。
   * 對於某些帳戶，需要登出並重新登入才能切換組織。
* 新增啟用 Target 追踨失敗時的錯誤訊息。
* 更新相依性。

## 版本 1.3.3 - 2022 年 6 月 20 日

* 修正阻止從網路事件表開啟快顯視窗的問題。
* 修正頁面 Alloy 資訊無法載入的問題。

## 版本 1.3.2 - 2022 年 6 月 9 日

* 新增使用者登入時的預設顯示圖片。
* 新增語法醒目提示至記錄中的 JSON 物件。

## 版本 1.3.1 - 2022 年 5 月 24 日

* 更新相依性。
* 修正無法啟用處理後點擊的 Analytics 問題。
* 修正偵錯工具附加到 Adob&#x200B;&#x200B;e 登入視窗的問題。
* 修正記錄訊息不會顯示在偵錯工具中的 AT.js 問題。

## 版本 1.3.0 - 2022 年 1 月 28 日

* 新增「關於」連結以顯示目前發行版本和註解。
* 新增切換功能，以查看 Analytics 請求的處理後點擊情形。此切換功能位於 Analytics 部份中。
* 修正在偵錯工具外部關閉工作階段時遠端偵錯工作階段的問題。
* 修正 Web SDK Edge Transactions 標籤中可見的錯誤通知。
* 修正偵錯工具存取 _satellite 物件時頁面不再使用警告的 Adob&#x200B;&#x200B;e 標記。
* 修正頁面上找不到 AppMeasurement 執行個體的某些情&#x200B;&#x200B;況。
* 修正首次開啟偵錯工具視窗時發生的頁面連線問題。

## 版本 1.2.0 - 2021 年 10 月 26 日

* 在網路檢視中顯示所有瀏覽器標籤的事件。若要限查看目前標籤的事件，請選取偵錯工具右下角的鎖定圖示。
* 更新品牌化。

## 版本 1.1.0 - 2021 年 10 月 5 日

* 遠端偵錯視覺化 - 將遠端偵錯事件整理排在視覺化流程圖中 (位在 Adob&#x200B;&#x200B;e Experience Platform Web SDK > Edge Transactions 部份中)。
* 規定頁面上使用的 Adob&#x200B;&#x200B;e Experience Platform Web SDK 組織，必須與啟動新的遠端偵錯工作階段時登入的組織相符。
* 僅顯示已連線標籤的 Edge Transactions。Target 追蹤記錄仍在「記錄 > Edge」部份中提供。
* 允許頁面上 Adob&#x200B;&#x200B;e Experience Platform Web SDK 的每個執行個體進行個別資料流 ID 設定覆蓋。新增偵錯已啟用的切換功能。
* 修正 Adob&#x200B;&#x200B;e Target 追蹤權杖不一定會隨 Adob&#x200B;&#x200B;e Experience Platform Web SDK 的遠端偵錯工作階段一起發送的問題。

## 版本 1.0.0，2021 年 5 月 5 日

* Experience Platform Debugger 第一個主要版本。旨在替換 Experience Cloud Debugger。
