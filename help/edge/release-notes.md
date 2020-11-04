---
title: Adobe Experience Platform Web SDK發行說明
seo-title: Adobe Experience Platform Web SDK發行說明
description: Adobe Experience Platform Web SDK 發行說明。
seo-description: Adobe Experience Platform Web SDK 發行說明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 8%

---


# 發行說明

## 2.3.0 版

* 新增nonce支援，以允許更嚴格的內容安全性政策。
* 新增單頁應用程式的個人化支援。
* 已改善與其他可能覆寫API之頁面上JavaScript程式碼的相 `window.console` 容性。
* 錯誤修正： `sendBeacon` 設為或自動追蹤 `documentUnloading` 連結點按 `true` 時，未使用。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：某些包含唯讀屬性的瀏覽器錯 `message` 誤未得到適當處理，導致不同的錯誤暴露給客戶。
* 錯誤修正：如果在iframe中執行SDK，若iframe的HTML頁面來自父視窗的HTML頁面以外的子網域，則會產生錯誤。

## 2.2.0 版

* 錯誤修正：Opt-in物件會阻止Alloy在有時進行呼 `idMigrationEnabled` 叫 `true`。
* 錯誤修正：讓Alloy知道應該傳回個人化優惠的要求，以避免閃爍的問題。

## 2.1.0 版

* 移除命 `syncIdentity` 令並支援在命令中傳遞這些 `sendEvent` ID。
* 支援IAB 2.0同意標準。
* 支援在命令中傳遞其他 `setConsent` ID。
* 支援覆蓋 `datasetId` 命令中 `sendEvent` 的。
* 支援合金顯示器([詳細內容](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 傳遞 `environment: browser` 實作詳細內容資料。
