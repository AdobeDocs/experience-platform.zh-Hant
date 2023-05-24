---
title: 配置Test參考
description: 瞭解審計員如何在Adobe Experience Platform調試器中為配置設定test。
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 67%

---

# 配置test引用

此參考提供了有關Adobe Experience Platform調試器中審計器功能如何運行配置test的詳細資訊。

>[!NOTE]
>
>有關平台調試器中審計者test的詳細資訊，請參見 [審計器功能概述](./overview.md)。

設定測試會掃描您實作中的特定設定和值，找出潛在衝突。Platform Auditor 會根據其他規則和建議的最佳實務來評估標記。

| 測試 | 重量 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 轉換名稱僅使用英數字元 | 3 | 的 `ev_conversion_property_name` 參數只應包含數字和小數值EXCEPT `ev_transid` 參數，它可以包含文本或數值。 尋找包含 URL 參數 (以 `everesttech.net` _ 開頭) 的 `ev_` 像素。 | 確定您的交易屬性參數只包含數值和小數值。<br><br>警告：任何其他值類型都可能導致資料遺失。 |
| Advertising Cloud - 轉換名稱使用 URL 可用的字元 | 3 | 轉換屬性名稱不應包含 &amp; 符號或問號。 | 確定交易屬性參數未包含非編碼的 &amp; 符號或問號。這些符號會中斷 URL 格式。<br><br>警告：包含非編碼和號或問號的屬性參數(例如：  `ev_formComplete?=1` 或  `ev_formComplete&Submit=1`)，可能導致資料丟失。 |
| Advertising Cloud - 正確實作交易 ID | 1 | 屬性名稱  `ev_transid=` 不應為空。 | 屬性名稱  `ev_transid=` 不應該沒有值。 若將其保留為空白，交易資料可能會遺失。將值分配給 `ev_transid=` 或從像素中刪除參數。 |
| Analytics - 在 DOM 中具現化 | 5 | Adobe Analytics 程式碼未安裝或無法執行。在網頁上找不到分析代碼時返回0。 | 確認已在頁面上實作 Analytics 標記，且後續指令碼活動不會加以封鎖。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Analytics - 具現化一次 | 5 | 在頁面上偵測到 Adobe Analytics 程式碼多次。在網頁上找不到A分析代碼時返回0。 | 確定頁面上只有一個 Analytics 標記。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Analytics - 最新版本 | 3 | 您的頁面未執行最新版 Analytics 程式碼庫。支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。在網頁上找不到分析代碼時返回0。 | 安裝最新版的 Analytics 程式庫。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hant) |
| 啟動 — 在DOM就緒後非同步載入第三方標籤 | 3 | 要在良好的用戶體驗和收集準確資料之間取得平衡，應在DOM就緒時觸發第三方標籤。 這樣可以確保這些追蹤指令碼能夠在不影響網站功能的情況下執行。 | 通過調整執行第三方像素的所有規則以在DOM Ready時激發來解決此問題。<br><br>[其他資訊](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID 服務 - 最新版本 | 2 | 您的頁面未執行最新版的訪客 ID 服務程式碼庫 visitorAPI.js。支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 安裝最新版的訪客 ID 服務程式庫。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch - 最新版本 | 2 | 這些頁面未運行標籤代碼庫（渦輪）的最新版本。 支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 重建並發佈標籤庫。<br><br>[其他資訊](../../tags/quick-start/quick-start.md) |
| Target - 最新版本 | 2 | 您的頁面未執行最新版 Target 程式碼庫。支援 Experience Cloud 技術的程式碼庫會持續更新及調整，以強化效能並提供最新功能。 | 安裝最新版的 Target 程式庫。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/) |
| Target - 在 mboxCreate 前面加上 mboxDefault | 5 | mboxCreate 的正確用法如下所示：<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | 確保包括  `<div class="mboxDefault"></div>` 調用mboxCreate()之前的標籤。 at.js 不會為您加上此標記。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/) |
| Target - 有效的 DOCTYPE | 5 | 偵測到無效的 DOCTYPE。在此情況下不會引發 mbox。對 at.js 而言，DOCTYPE 必須處於「標準」模式，否則 Target 將無法運作。 | 更新頁面上的 DOCTYPE。<br><br>[其他資訊](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
