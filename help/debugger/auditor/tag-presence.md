---
title: 標籤存在測試參考
description: 瞭解Auditor功能如何測試Adobe Experience Platform Debugger中的標籤是否存在。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 17%

---

# 標籤存在測試參考

此參考檔案主要探討Auditor功能在Adobe Experience Platform Debugger測試中如何偵測標籤是否存在的問題，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱[Auditor功能概觀](./overview.md)。

標籤是否存在測試會評估頁面上是否存在特定標籤，以及這些標籤在頁面程式碼中的位置是否正確。

| 測試 | 粗細 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud — 程式碼是否存在 | 5 | Advertising Cloud 標記無法在 DOM 中使用。 | 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)實作Advertising Cloud標籤。 |
| Advertising Cloud — 實作區段畫素 | 5 | 將您的 Advertising Cloud 區段像素升級為新的 Advertising Cloud 僅限影像標記。使用過時的 AMO 區段標記可能會導致資料遺失。 | 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)實作Advertising Cloud區段畫素。 |
| Analytics — 在DOM中載入 | 5 | 未偵測到 Adobe Analytics 標記。 | 安裝最新版的Analytics。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Launch — 載入程式庫 | 5 | 在DOM中找不到`global _satellite`物件，這表示未安裝標籤程式庫或無法執行。 | 確認已在頁面上實作標籤程式庫，且後續指令碼活動不會加以封鎖。 |
| Launch — 沒有多個內嵌指令碼 | 5 | 生產網站應在每頁僅載入一個內嵌程式碼。 | 確認頁面上僅載入所需的生產程式庫。 |
| 啟動 — `pageBottom`回呼存在於`<body>`中 | 5 | 在頁面的`<body>`內找不到必要的`_satellite.pageBottom()`回呼。 如果在頁面上完全找不到`pageBottom`呼叫，或該呼叫位於`<head>`標籤中（或其他非預期的位置），則此測試不會通過。 只有在`pageBottom`位於`<body>`標籤內的某處時，測試才會通過。 | 在結尾的`</body>`標籤前面加上緊鄰的內嵌指令碼，以確保標籤可正常運作。<br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch — 進行非同步部署時，`pageBottom`回呼不應存在 | 5 | 在頁面上找到`_satellite.pageBottom()`回呼，但以非同步方式部署標籤時不應有此回呼。 | 移除`_satellite.pageBottom()`指令碼以啟用適當的標籤功能。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience CloudID服務 — 程式碼是否存在 | 5 | 找不到 Experience Cloud ID 服務程式碼。強烈建議您使用Experience CloudID (ECID)，以確保充分發揮Experience Cloud解決方案的效益，這對於跨Experience Cloud解決方案的ID管理至關重要。 | 安裝最新版的ECID。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant) |
| Experience CloudID服務 — Cookie是否存在 | 5 | 找不到`AMCV_` Cookie。 您必須從`VisitorAPI.js`程式碼將訪客物件具現化。 | 如果這是標籤實施，請確認已在ECID工具中正確輸入AdobeOrg ID。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience CloudID服務 — 有MID值存在 | 5 | 在`AMCV_` Cookie中找不到MID值。 | 再次測試以檢查是否有任何ECID API延遲。 若持續發生此狀況，請連絡Adobe客戶服務。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target — 程式碼是否存在 | 5 | Adobe Target應在DOM中定義。 | 安裝最新版的Target (at.js)。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target — 在`<head>`中載入資料庫 | 4 | Target程式庫應載入`<head>`標籤中。 | 確認Target程式庫已載入`<head>`標籤中。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
