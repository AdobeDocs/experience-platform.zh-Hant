---
title: 警示測試參考
description: 瞭解Auditor功能如何在Adobe Experience Platform Debugger中測試警報。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 34%

---

# 警示測試參考

此參考檔案主要探討Adobe Experience Platform Debugger的Auditor功能如何執行警示測試，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

警報會顯示您應留意但不影響分數的問題。某些情況下，這些最佳實務建議可能不適用於您的實作。

| 測試 | 粗細 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 實作正確的轉換標記 | 0 | 檢查是否使用正確的轉換標記。<br><br>**警告**：使用過時的TubeMogul轉換標籤可能會導致資料遺失。 | 將您的轉換像素升級為新的 Advertising Cloud 僅限影像轉換標記。這項工作可以透過以下方式輕鬆完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 使用正確的 JS 標記 | 0 | Advertising Cloud應使用最新的JavaScript標籤。 | 將您的 Advertising Cloud JavaScript 升級至最新版本。使用過時的 JavaScript 版本可能會導致功能失效。若要輕鬆完成這項工作，請使用 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 僅限影像標記 | 0 | Advertising Cloud 影像像素格式應符合下列其中一個建議格式： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 將您的 Advertising Cloud 像素升級至新的 Advertising Cloud 僅限影像標記，以確保您使用的是完整的 Advertising Cloud 功能。這項工作可以透過以下方式輕鬆完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 啟用區段像素 DSP 同步 | 0 | 檢查 TubeMogul 區段像素是否包含「DSP 同步」設定，並建議您將該設定新增至像素。DSP同步處理設定取決於查詢字串引數的使用。 總結： <ul><li>如果觸發標籤至下列任一專案：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>而且標籤包含URL引數 `sid=`</li><li>然後檢視URL引數是否為 `cs=0` 或 `cs=1` 已存在，且若未推薦 `cs=1` 將新增至這些畫素，以便提高對象符合率。</li></ul> | 新增URL引數 `cs=1` 至您的Advertising Cloud畫素，以便進行DSP同步，進而提高對象匹配率。 這項工作最容易透過以下方式完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID 服務 - 僅使用一個 AdobeOrg | 0 | 在一般ECID實作中，應使用單一AdobeOrg。 | 驗證此實作有多個 AdobeOrg ID。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| 啟動 —  `pageBottom` 回呼位置 | 0 | 此 `_satellite.pageBottom()` 函式必須存在，標籤才能運作。 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤以確保DTM可正常運作。 注意：最佳實務是讓該標籤成為 `<body>`. 若其位於 `<body>` 標籤時，此變數可能會正常運作，但由於這並非最佳實務，因此可能會無法正確運作，或產生非預期或不適當的結果。 | 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤以確保DTM可正常運作。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 自行託管 | 0 | 標籤程式庫在Adobe的Akamai執行個體上受到託管： `assets.adobedtm.com`. 自行託管是載入標籤的建議方法，因為此方法可讓您透過快取控制進一步掌控網站效能、減少對第三方指令碼的依賴，且更能掌握發佈程式。 您可以透過自己的網站託管或CDN來託管及管理標籤程式庫。 | 切換至自行託管，即是在頁面上載入標籤的方法。 雖然透過 Akamai CDN 進行 託管在多數情況下都是可行的，但自行託管可以改善頁面效能。<br><br>其他資訊:<ul><li>[標籤快速入門手冊](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[非同步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 應以非同步方式部署 | 0 | 標籤應以非同步方式部署，以發揮最佳效能。 | 包含 `async` 內嵌指令碼中的引數，以確保標籤功能正確 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target — 中的內容 `mboxDefault` | 0 | 內容應存在於中 `mboxDefault` 使用時 `at.js`. | 確認有可用的內容。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
