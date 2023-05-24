---
title: 標籤存在Test引用
description: 瞭解審計者如何在Adobe Experience Platform調試器中為標籤存在test提供功能。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 33%

---

# 標籤存在test引用

此參考提供了有關審計者如何在Adobe Experience Platform調試器test中進行標籤存在功能的詳細資訊。

>[!NOTE]
>
>有關平台調試器中審計者test的詳細資訊，請參見 [審計器功能概述](./overview.md)。

標籤狀態test評估頁面上是否存在某些標籤，以及這些標籤是否位於頁面代碼的正確位置。

| 測試 | 重量 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 程式碼是否存在 | 5 | Advertising Cloud 標記無法在 DOM 中使用。 | 使用 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Advertising Cloud - 實作區段像素 | 5 | 將您的 Advertising Cloud 區段像素升級為新的 Advertising Cloud 僅限影像標記。使用過時的 AMO 區段標記可能會導致資料遺失。 | 使用 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Analytics - 在 DOM 中載入 | 5 | 未偵測到 Adobe Analytics 標記。 | 安裝最新版的 Analytics。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |
| Launch - 載入程式庫 | 5 | A `global _satellite` 在DOM中找不到對象，這意味著未安裝或無法執行標籤庫。 | 驗證標籤庫是否已在頁面上實現，且未被後續指令碼活動阻止。 |
| Launch - 沒有多個內嵌指令碼 | 5 | 生產站點每頁只應載入一個嵌入代碼。 | 確認頁面上僅載入所需的生產程式庫。 |
| 啟動 —  `pageBottom` 回調存在 `<body>` | 5 | 必需 `_satellite.pageBottom()` 在中未找到回調 `<body>` 的下界。 此test在 `pageBottom` 在頁面上找不到呼叫，或者 `<head>` 標籤（或其他意外位置）。 只有在 `pageBottom` 在 `<body>` 標籤。 | 在關閉前添加內聯指令碼 `</body>` 標籤以確保正確的標籤功能。<br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| 啟動 —  `pageBottom` 非同步部署時不存在回調 | 5 | 的 `_satellite.pageBottom()` 在頁上找到回調，在非同步部署標籤時不應出現這種情況。 | 刪除 `_satellite.pageBottom()` 指令碼以啟用正確的標籤功能。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID 服務 - 程式碼是否存在 | 5 | 找不到 Experience Cloud ID 服務程式碼。強烈建議使用Experience CloudID(ECID)，以確保您從Experience Cloud解決方案中獲得最大價值，並且對於跨Experience Cloud解決方案的ID管理至關重要。 | 安裝ECID的最新版本。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID 服務 - Cookie 是否存在 | 5 | 的 `AMCV_` 找不到cookie。 您必須從 `VisitorAPI.js` 程式碼將訪客物件具現化。 | 如果這是標籤實現，請驗證AdobeOrg ID是否正確輸入到ECID工具中。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID 服務 - 有 MID 值存在 | 5 | 在中未找到MID值 `AMCV_` 餅乾。 | 再次test以檢查任何ECID API延遲。 若持續發生此狀況，請連絡 Adobe 客戶服務。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - 程式碼是否存在 | 5 | Adobe Target應該在DOM中定義。 | 安裝最新版的 Target (at.js)。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| 目標 — 載入的庫 `<head>` | 4 | 應在 `<head>` 標籤。 | 檢查以確保在 `<head>` 標籤。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
