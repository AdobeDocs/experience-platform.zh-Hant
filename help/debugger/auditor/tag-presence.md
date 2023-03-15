---
title: 標籤是否存在測試參考
description: 了解Auditor如何在Adobe Experience Platform Debugger中測試標籤是否存在。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 33%

---

# 標籤是否存在測試參考

此參考檔案主要探討Adobe Experience Platform Debugger中的auditor功能如何測試標籤是否存在所需，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

標籤是否存在測試會評估特定標籤是否存在於頁面上，以及它們是否位於頁面程式碼中的正確位置。

| 測試 | 寬度 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 程式碼是否存在 | 5 | Advertising Cloud 標記無法在 DOM 中使用。 | 使用實作Advertising Cloud標籤 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 實作區段像素 | 5 | 將您的 Advertising Cloud 區段像素升級為新的 Advertising Cloud 僅限影像標記。使用過時的 AMO 區段標記可能會導致資料遺失。 | 使用實作Advertising Cloud區段像素 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - 在 DOM 中載入 | 5 | 未偵測到 Adobe Analytics 標記。 | 安裝最新版的 Analytics。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Launch - 載入程式庫 | 5 | A `global _satellite` 在DOM中找不到物件，表示未安裝或無法執行標籤程式庫。 | 確認已在頁面上實作標籤程式庫，且後續指令碼活動不會加以封鎖。 |
| Launch - 沒有多個內嵌指令碼 | 5 | 生產網站每頁只應載入一個內嵌程式碼。 | 確認頁面上僅載入所需的生產程式庫。 |
| Launch - `pageBottom` 回呼存在 `<body>` | 5 | 必要 `_satellite.pageBottom()` 在中找不到回呼 `<body>` 頁面的下一個頁面。 若 `pageBottom` 在頁面上完全找不到呼叫，或呼叫位於 `<head>` 標籤（或其他非預期的位置）。 只有在 `pageBottom` 在內 `<body>` 標籤。 | 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤，以確保標籤可正常運作。<br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` 非同步部署時，回呼不應存在 | 5 | 此 `_satellite.pageBottom()` 在頁面上找到回呼，但以非同步方式部署標籤時，則不應有此回呼。 | 移除 `_satellite.pageBottom()` 指令碼來啟用正確的標籤功能。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID 服務 - 程式碼是否存在 | 5 | 找不到 Experience Cloud ID 服務程式碼。強烈建議您使用Experience CloudID(ECID)，以確保能充分發揮Experience Cloud解決方案的效益，且這對於Experience Cloud解決方案的ID管理至關重要。 | 安裝最新版ECID。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID 服務 - Cookie 是否存在 | 5 | 此 `AMCV_` 找不到cookie。 您必須從 `VisitorAPI.js` 程式碼將訪客物件具現化。 | 如果這是標籤實作，請確認在ECID工具中已正確輸入AdobeOrg ID。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID 服務 - 有 MID 值存在 | 5 | 在 `AMCV_` cookie。 | 再次測試以檢查是否有任何ECID API延遲。 若持續發生此狀況，請連絡 Adobe 客戶服務。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - 程式碼是否存在 | 5 | Adobe Target應在DOM中定義。 | 安裝最新版的 Target (at.js)。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target — 在中載入程式庫 `<head>` | 4 | Target程式庫應載入 `<head>` 標籤。 | 確認Target程式庫已載入 `<head>` 標籤。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
