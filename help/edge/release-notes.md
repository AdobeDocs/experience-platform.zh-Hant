---
title: Adobe Experience Platform Web SDK發行說明
seo-title: Adobe Experience Platform Web SDK發行說明
description: Adobe Experience Platform Web SDK 發行說明。
seo-description: Adobe Experience Platform Web SDK 發行說明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 16%

---


# 發行說明

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
