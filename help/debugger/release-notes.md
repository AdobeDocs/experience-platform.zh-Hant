---
title: Adobe Experience Platform Debugger發行說明
description: Adobe Experience Platform Debugger 的最新發行說明。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；發行說明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 28e54656fcd85fc56e72d4fdd3d079cf8590302f
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 4%

---

# Adobe Experience Platform Debugger發行說明

<!-- ## Version 1.4.0 - August 24, 2022

* Added support for Web SDK hybrid implementation.
* Added error message when enabling Target Trace fails.
* Updated dependencies. -->

## 版本1.3.3 - 2022年6月20日

* 修正無法從網路事件表開啟快顯視窗的問題。
* 修正無法載入頁面上Alloy資訊的問題。

## 版本1.3.2 - 2022年6月9日

* 新增使用者登入時的預設頭像。
* 新增語法醒目提示至記錄檔中的JSON物件。

## 版本1.3.1 - 2022年5月24日

* 更新相依性。
* 修正無法啟用處理後點擊的Analytics問題。
* 修正除錯程式會附加至Adobe登入視窗的問題。
* 修正AT.js問題，此問題導致記錄訊息無法顯示於Debugger中。

## 1.3.0版 — 2022年1月28日

* 新增關於連結以顯示最新版本和附註。
* 新增切換功能，可檢視Analytics請求的貼文處理點擊。 切換按鈕可在Analytics區段中使用。
* 修正在偵錯工具外部關閉工作階段時，發生遠端偵錯工作階段的問題。
* 修正Web SDK邊緣交易標籤中可見的錯誤通知。
* 修正除錯程式存取_satellite物件時，頁面取代Adobe標籤的警告。
* 修正在頁面上找不到AppMeasurement例項的部分案例。
* 修正首次開啟偵錯工具視窗時發生的頁面連線問題。

## 版本1.2.0 - 2021年10月26日

* 在網路檢視中顯示來自所有瀏覽器標籤的事件。 若只要從目前索引標籤查看事件，請選取除錯工具右下角的鎖定圖示。
* 更新品牌。

## 版本1.1.0 - 2021年10月5日

* 遠端除錯視覺效果 — 將遠端除錯事件整理至Adobe Experience Platform Web SDK >邊緣交易區段中的視覺化流程圖。
* 啟動新的遠端除錯工作階段時，需要頁面上使用的Adobe Experience Platform Web SDK IMS組織符合登入的組織。
* 僅顯示所連接頁簽的邊緣事務。 Target追蹤記錄仍可在「記錄> Edge」區段中使用。
* 為頁面上的Adobe Experience Platform Web SDK每個例項允許個別的資料流ID設定覆寫。 新增已啟用除錯的切換按鈕。
* 修正Adobe Target追蹤Token未一律與Adobe Experience Platform Web SDK的遠端除錯工作階段一起傳送的問題。

## 1.0.0版（2021年5月5日）

* Experience Platform偵錯工具的第一個主要版本。 意在取代Experience Cloud Debugger。
