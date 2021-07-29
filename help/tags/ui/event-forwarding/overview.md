---
title: 事件轉送概述
description: 了解Adobe Experience Platform中的事件轉送功能，讓您不須變更標籤實作，即可使用Platform Edge Network執行工作。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 37%

---

# 事件轉送概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

Adobe Experience Platform中的事件轉送功能可讓Adobe Experience Platform邊緣網路執行用戶端上正常執行的工作，減少網頁和應用程式的重量。 事件轉送規則可以轉換資料，並將資料傳送至新目的地，而不會變更用戶端實作。

事件轉送結合Adobe Experience Platform Web和行動SDK，便能：

* 從包含資料裝載的頁面發出單一呼叫。 然後，資料會聯合伺服器端，以減少用戶端網路流量，並為客戶提供更快速的體驗。
* 減少載入網頁所需時間，讓您的網站符合業界最佳實務，發揮優異效能。
* 提高透明度並控制要在所有標籤屬性間傳送哪些資料類型。
* 建立事件轉送規則，將先前追蹤的資料傳送至新目的地。

## 提升效能

大環境的競爭日益激烈，企業勢必得以效能至上，設法維持及擴大市占率。事件轉送可改善行動、IoT和OTT裝置間的網站和應用程式效能。 網站轉換率能因載入時間加快而有所提升、行動應用程式的耗電量減少，而且 OTT 應用程式的回應速度和在行動裝置上執行一樣快。隨著效能提升，轉換率通常也會增加。

## 資料控管更理想

隨著採用的技術越來越多，且資料傳送至更多目的地，想控管哪些資料傳送至何處，簡直難上加難。GDPR和CCPA等法規的規範化，迫使公司對日益困難的資料問題施加更多控制。

事件轉送有助於行銷團隊在控制資料的同時，發展其業務。 這可減少行銷人員需要使用的用戶端技術數量，使其能更輕鬆地進入目標市場，並將資料傳送至 Adobe 以外的目的地。實作團隊也能更輕鬆地管理從用戶端到多個目的地的資料流。

## 事件轉送與標籤之間的差異

請務必注意事件轉送與標籤之間的下列差異：

* 資料元素代碼化

   * 標籤：在規則中，資料元素會以`%`標籤，位於資料元素名稱的開頭和結尾。 例如 `%viewportHeight%`。

   * 事件轉送：在規則中，資料元素會以`{{`在開頭、`}}`在資料元素名稱的結尾標籤。 例如 `{{viewportHeight}}`。

* 資料參照方式

   若要參照 Edge Network 的資料，資料元素路徑必須為 `arc.event._<element>_`，

   其中 `arc` 代表 Adobe Response Context。

   例如︰`arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >如果此路徑指定不正確，則不會收集資料。


* 規則動作順序

   在規則的「動作」區段中，事件轉送規則一律會依序執行。 儲存規則時，請確認動作順序正確。無法像使用標籤一樣選擇此執行序列。

* 自訂程式碼 JavaScript 版本

   標籤使用JavaScript es5版。 事件轉送使用es6版。

<!--doc Adobe Cloud Connector extension, get from Jon-->
