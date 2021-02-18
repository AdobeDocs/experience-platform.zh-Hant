---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK的最新發行說明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK；發行說明；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---


# 發行說明

## 2.3.0 版

* 新增nonce支援，以允許更嚴格的內容安全性政策。
* 新增單頁應用程式的個人化支援。
* 已改善與其他可能覆寫`window.console` API之頁面上JavaScript程式碼的相容性。
* 錯誤修正：`sendBeacon`未在`documentUnloading`設為`true`或自動追蹤連結點按時使用。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：某些包含唯讀`message`屬性的瀏覽器錯誤處理不當，導致不同的錯誤暴露給客戶。
* 錯誤修正：如果在iframe中執行SDK，若iframe的HTML頁面來自父視窗的HTML頁面以外的子網域，則會產生錯誤。

## 2.2.0 版

* 錯誤修正：當`idMigrationEnabled`為`true`時，Opt-in對象會阻止Alloy發出呼叫。
* 錯誤修正：讓Alloy知道應該傳回個人化優惠的要求，以避免閃爍的問題。

## 2.1.0 版

* 刪除`syncIdentity`命令，並支援在`sendEvent`命令中傳遞這些ID。
* 支援IAB 2.0同意標準。
* 支援在`setConsent`命令中傳遞其他ID。
* 支援覆蓋`sendEvent`命令中的`datasetId`。
* 支援合金顯示器（[閱讀更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在實作詳細內容資料中傳遞`environment: browser`。
