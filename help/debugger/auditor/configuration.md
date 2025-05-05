---
title: 設定測試參考
description: 瞭解Auditor功能如何測試Adobe Experience Platform Debugger中的設定。
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 50%

---

# 設定測試參考

此參考檔案主要探討Adobe Experience Platform Debugger的Auditor功能如何執行設定測試，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Experience Platform Debugger中Auditor測試的詳細資訊，請參閱[Auditor功能概觀](./overview.md)。

設定測試會掃描您實作中的特定設定和值，找出潛在衝突。Experience Platform Auditor會根據其他規則和建議的最佳實務來評估標籤。

| 測試 | 粗細 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud — 轉換名稱僅使用英數字元 | 3 | 除了`ev_transid`引數可以包含文字或數值外，`ev_conversion_property_name`引數應該只包含數值和小數值。 尋找包含URL引數（以`ev_`開頭）的`everesttech.net`畫素。 | 確定您的交易屬性參數只包含數值和小數值。<br><br>警告：任何其他值型別都可能導致資料遺失。 |
| Advertising Cloud — 轉換名稱使用URL可用的字元 | 3 | 轉換屬性名稱不應包含 &amp; 符號或問號。 | 確定交易屬性參數未包含非編碼的 &amp; 符號或問號。這些符號會中斷 URL 格式。<br><br>警告：包含非編碼&amp;符號或問號的屬性引數（例如： `ev_formComplete?=1`或`ev_formComplete&Submit=1`）可能會導致資料遺失。 |
| Advertising Cloud — 正確實作交易ID | 1 | 屬性名稱`ev_transid=`不應為空白。 | 屬性名稱`ev_transid=`不應保留為空白。 若將其保留為空白，交易資料可能會遺失。將值指派給`ev_transid=`或從畫素移除引數。 |
| Analytics — 在DOM中具現化 | 5 | Adobe Analytics 程式碼未安裝或無法執行。在網頁上找不到Analytics程式碼時，會傳回0。 | 確認已在頁面上實作 Analytics 標記，且後續指令碼活動不會加以封鎖。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Analytics — 具現化一次 | 5 | 在頁面上偵測到 Adobe Analytics 程式碼多次。在網頁上找不到A-Analytics程式碼時，會傳回0。 | 確定頁面上只有一個 Analytics 標記。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Analytics — 最新版本 | 3 | 您的頁面未執行最新版 Analytics 程式碼庫。支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。在網頁上找不到Analytics程式碼時，會傳回0。 | 安裝最新版的 Analytics 程式庫。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant) |
| Launch - DOM準備就緒後，以非同步方式載入第三方標籤 | 3 | 為了在良好的使用者體驗與收集正確資料之間取得平衡，應在DOM準備就緒時觸發第三方標籤。 這樣可以確保這些追蹤指令碼能夠在不影響網站功能的情況下執行。 | 調整所有執行第三方畫素的規則，使其在DOM就緒時引發，以解決此問題。<br><br>[其他資訊](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID服務 — 最新版本 | 2 | 您的頁面未執行最新版的訪客ID服務程式碼庫visitorAPI.js。 支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 安裝最新版的訪客 ID 服務程式庫。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html?lang=zh-Hant) |
| Launch — 最新版本 | 2 | 這些頁面未執行最新版本的標籤程式碼庫(Turbine)。 支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 重建並發佈標籤程式庫。<br><br>[其他資訊](../../tags/quick-start/quick-start.md) |
| Target — 最新版本 | 2 | 您的頁面未執行最新版 Target 程式碼庫。支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 安裝最新版的 Target 程式庫。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault先於mboxCreate | 5 | mboxCreate的正確用法看起來類似這樣： <br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | 在叫用mboxCreate()之前，請務必先加上`<div class="mboxDefault"></div>`標籤。 at.js 不會為您加上此標記。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/) |
| Target — 有效的DOCTYPE | 5 | 偵測到無效的 DOCTYPE。在此情況下不會觸發mbox。  對 at.js 而言，DOCTYPE 必須處於「標準」模式，否則 Target 將無法運作。 | 更新頁面上的 DOCTYPE。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
