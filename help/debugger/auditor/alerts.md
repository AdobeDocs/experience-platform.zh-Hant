---
title: 警報Test引用
description: 瞭解審計員如何在Adobe Experience Platform調試器中為警報提供test。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 34%

---

# 警報test引用

此參考提供了有關Adobe Experience Platform調試器中審計器功能如何運行警報test的詳細資訊。

>[!NOTE]
>
>有關平台調試器中審計者test的詳細資訊，請參見 [審計器功能概述](./overview.md)。

警報會顯示您應留意但不影響分數的問題。某些情況下，這些最佳實務建議可能不適用於您的實作。

| 測試 | 重量 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 實作正確的轉換標記 | 0 | 檢查是否使用正確的轉換標記。<br><br>**警告**:使用過時的TubeMogul轉換標籤可能會導致資料丟失。 | 將您的轉換像素升級為新的 Advertising Cloud 僅限影像轉換標記。這可以通過 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Advertising Cloud - 使用正確的 JS 標記 | 0 | Advertising Cloud應使用最新的JavaScript標籤。 | 將您的 Advertising Cloud JavaScript 升級至最新版本。使用過時的 JavaScript 版本可能會導致功能失效。通過使用 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Advertising Cloud - 僅限影像標記 | 0 | Advertising Cloud 影像像素格式應符合下列其中一個建議格式： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 將您的 Advertising Cloud 像素升級至新的 Advertising Cloud 僅限影像標記，以確保您使用的是完整的 Advertising Cloud 功能。這可以通過 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Advertising Cloud - 啟用區段像素 DSP 同步 | 0 | 檢查 TubeMogul 區段像素是否包含「DSP 同步」設定，並建議您將該設定新增至像素。同步DSP設定由使用查詢字串參數確定。 總結： <ul><li>如果標籤正被激發到以下任一項：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>標籤包含URL參數 `sid=`</li><li>然後檢查URL參數 `cs=0` 或 `cs=1` 存在，如果不建議 `cs=1` 添加到這些像素中，以便提高觀眾匹配率。</li></ul> | 添加URL參數 `cs=1` 到您的Advertising Cloud像素，DSP以便可以進行同步，從而提高受眾匹配率。 這可以通過 [Advertising Cloud標籤擴展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)。 |
| Experience Cloud ID 服務 - 僅使用一個 AdobeOrg | 0 | 在普通ECID實現中，應使用單個AdobeOrg。 | 驗證此實作有多個 AdobeOrg ID。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| 啟動 —  `pageBottom` 回調放置 | 0 | 的 `_satellite.pageBottom()` 函式必須存在，才能使標籤工作。 在關閉前添加內聯指令碼 `</body>` 標籤以確保DTM功能正確。 注：最佳做法是，標籤是 `<body>`。 如果在 `<body>` tag ，它有運行的可能，但由於它不是最佳做法，它可能運行不正確或出現意外或不希望的結果。 | 在關閉前添加內聯指令碼 `</body>` 標籤以確保DTM功能正確。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 自行託管 | 0 | 標籤庫托管在Adobe的Akamai實例上 `assets.adobedtm.com`。 自我托管是載入標籤的推薦方法，因為它通過快取控制、減少第三方指令碼依賴關係和更好地控制發佈過程提供了對網站效能的更大控制。 標籤庫可以通過您自己的Web托管或CDN托管和管理。 | 切換到自主承載是在頁面上載入標籤的方法。 雖然透過 Akamai CDN 進行 託管在多數情況下都是可行的，但自行託管可以改善頁面效能。<br><br>其他資訊:<ul><li>[標籤快速入門手冊](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[非同步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 應以非同步方式部署 | 0 | 應非同步部署標籤以獲得最佳效能。 | 包括 `async` 內聯指令碼中的參數，以確保正確的標籤功能 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| 目標 — 中的內容 `mboxDefault` | 0 | 內容應存在於 `mboxDefault` 使用 `at.js`。 | 確認有可用的內容。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
