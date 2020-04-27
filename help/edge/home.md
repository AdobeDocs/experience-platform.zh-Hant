---
title: Adobe Experience Platform Web SDK說明
seo-title: Adobe Experience Platform Web SDK說明
description: 瞭解Adobe Experience Platform Web SDK是什麼，以及如何使用它。
seo-description: 可讓Adobe Experience Cloud客戶與Experience Cloud中的各種服務互動
translation-type: tm+mt
source-git-commit: 68361835437026c86af2402cc8400a3b3f32cb81

---


# （測試版）什麼是Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與Experience Cloud中的各種服務互動。

## SDK已由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不只是現有程式庫的包裝函式。 這完全是重寫。 其目的在於以正確的順序觸發標籤、與程式庫版本修訂挑戰不一致，以及更好的相依性管理，以結束挑戰。 這是實作Experience Cloud的新方式。

除了新的程式庫外，還有新的端點，可簡化對Adobe解決方案的HTTP要求。 之前，Visitor.js會將封鎖呼叫傳送至訪客ID服務，然後AT.js會傳送呼叫至Adobe Target,DIL.js會傳送呼叫至Adobe Audience Manager，最後AppMeasurement.js會傳送呼叫至Adobe Analytics。 這個新的程式庫和端點可以在單一呼叫中擷取ID、擷取Target體驗、傳送資料至Audience Manager，並將資料傳入Adobe Experience Platform。