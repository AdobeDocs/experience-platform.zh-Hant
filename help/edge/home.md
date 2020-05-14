---
title: Adobe Experience Platform Web SDK說明
seo-title: Adobe Experience Platform Web SDK說明
description: 瞭解Adobe Experience Platform Web SDK是什麼，以及如何使用它。
seo-description: 可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 什麼是Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與Experience Cloud中的各種服務互動。

## SDK已由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不只是現有程式庫的包裝函式。 這完全是重寫。 其目的在於以正確的順序觸發標籤、與程式庫版本修訂挑戰不一致，以及更好的相依性管理，以結束挑戰。 這是實作Experience Cloud的新方式，也是開放原 [始碼](https://github.com/adobe/alloy)

除了新的程式庫外，還有新的端點，可簡化對Adobe解決方案的HTTP要求。 之前，Visitor.js會將封鎖呼叫傳送至訪客ID服務，然後AT.js會傳送呼叫至Adobe Target,DIL.js會傳送呼叫至Adobe Audience Manager，最後AppMeasurement.js會傳送呼叫至Adobe Analytics。 這個新的程式庫和端點可以在單一呼叫中擷取ID、擷取Target體驗、傳送資料至Audience Manager，以及將資料傳送至Adobe Experience Platform。

## 快速入門

我們強烈建議您結 [帳我們的快速入門手冊](getting-started/quick-start-with-launch.md) ，以取得如何開始使用啟動的快速教學課程。

本產品不斷發展，不斷成長，以支援越來越多的使用案例。 為跟上最新的腳步，我們結帳瞭解我們 [支援的使用案例展示板](https://github.com/adobe/alloy/projects/5)。 我們會隨時更新目前支援的使用案例，以及我們正在研究的使用案例，讓您做出最佳決策。

* __尚未支援的使用案例__ -我們規劃中未來將要完成的使用案例。
* __使用案例進行中__ -這些是團隊目前正在完成的發行使用案例。
* __支援的使用案例__ -這些是目前支援和適用的使用案例。
* __我們不支援的使用案例__ -這些是我們決定不支援的使用案例。
