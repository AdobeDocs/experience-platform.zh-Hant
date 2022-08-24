---
title: Adobe Experience Platform調試器發行說明
description: Adobe Experience Platform Debugger 的最新發行說明。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；發行說明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: f2733cca00f98e85cd1b3944c5127f5c1c89594e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 4%

---

# Adobe Experience Platform調試器發行說明

## 版本1.4.0 - 2022年8月24日

* 增加了對Web SDK混合實現的支援。
* 啟用目標跟蹤失敗時添加了錯誤消息。
* 已更新依賴項。

## 版本1.3.3 - 2022年6月20日

* 已修復阻止從網路事件表開啟彈出窗口的問題。
* 已修復問題，阻止載入頁上的合金資訊。

## 版本1.3.2 - 2022年6月9日

* 已在用戶登錄時添加預設虛擬形象。
* 已向日誌中的JSON對象添加語法突出顯示。

## 版本1.3.1 - 2022年5月24日

* 已更新依賴項。
* 無法啟用後處理命中的已修復分析問題。
* 已解決調試器將附加到Adobe登錄窗口的問題。
* 已修復AT.js問題，其中日誌消息不會在調試器中顯示。

## 版本1.3.0 - 2022年1月28日

* 已添加關於連結，以顯示當前版本和說明。
* 添加切換以查看分析請求的後處理命中。 該切換在「分析」部分可用。
* 修復了在調試器外部關閉會話時的遠程調試會話問題。
* 在Web SDK邊緣事務頁籤中可見的修復錯誤通知。
* 修復器訪問_sattellite對象時，頁面上的固定Adobe標籤出現棄用警告。
* 修復了在頁面上找不到AppMeasurement實例的某些情況。
* 第一次開啟調試器窗口時發生的已修復頁面連接問題。

## 版本1.2.0 - 2021年10月26日

* 顯示網路視圖中所有瀏覽器頁籤中的事件。 要僅從當前頁籤中查看事件，請選擇調試器右下角的鎖定表徵圖。
* 已更新品牌。

## 1.1.0版 — 2021年10月5日

* 遠程調試可視化 — 將遠程調試事件組織到Adobe Experience PlatformWeb SDK >邊緣事務部分的可視流程圖中。
* 啟動新的遠程調試會話時，需要頁面上使用的Adobe Experience PlatformWeb SDK IMS組織與登錄的組織匹配。
* 僅顯示已連接頁籤的邊緣事務。 「日誌」>「邊緣」部分中仍提供目標跟蹤日誌。
* 允許對頁面上的Adobe Experience PlatformWeb SDK的每個實例分別進行資料流ID配置覆蓋。 添加啟用調試的切換。
* 已修復Adobe Target跟蹤令牌未隨Adobe Experience PlatformWeb SDK的遠程調試會話一起發送的問題。

## 1.0.0版2021年5月5日

* Experience Platform調試器的第一個主版本。 意在替換Experience Cloud Debugger。
