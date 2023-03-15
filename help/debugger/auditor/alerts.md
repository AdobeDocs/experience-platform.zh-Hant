---
title: 警報測試參考
description: 了解Auditor如何在Adobe Experience Platform Debugger中測試警報。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 34%

---

# 警報測試參考

此參考檔案主要探討Adobe Experience Platform Debugger中的auditor功能如何執行警報測試。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

警報會顯示您應留意但不影響分數的問題。某些情況下，這些最佳實務建議可能不適用於您的實作。

| 測試 | 寬度 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud - 實作正確的轉換標記 | 0 | 檢查是否使用正確的轉換標記。<br><br>**警告**:使用過時的TubeMogul轉換標籤可能會導致資料遺失。 | 將您的轉換像素升級為新的 Advertising Cloud 僅限影像轉換標記。這可以用 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 使用正確的 JS 標記 | 0 | Advertising Cloud應使用最新的JavaScript標籤。 | 將您的 Advertising Cloud JavaScript 升級至最新版本。使用過時的 JavaScript 版本可能會導致功能失效。這可以通過使用 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 僅限影像標記 | 0 | Advertising Cloud 影像像素格式應符合下列其中一個建議格式： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 將您的 Advertising Cloud 像素升級至新的 Advertising Cloud 僅限影像標記，以確保您使用的是完整的 Advertising Cloud 功能。這可以用 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 啟用區段像素 DSP 同步 | 0 | 檢查 TubeMogul 區段像素是否包含「DSP 同步」設定，並建議您將該設定新增至像素。「DSP同步」設定是由使用查詢字串參數所決定。 總結： <ul><li>如果標籤是針對下列任一項目觸發：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>標籤中包含URL參數 `sid=`</li><li>然後檢查URL參數 `cs=0` 或 `cs=1` 存在，若不建議 `cs=1` 會新增至這些像素，以提高對象匹配率。</li></ul> | 新增URL參數 `cs=1` 至您的Advertising Cloud像素，以便進行DSP同步，進而提高對象匹配率。 這最容易完成的是 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID 服務 - 僅使用一個 AdobeOrg | 0 | 在一般ECID實作中，應使用單一AdobeOrg。 | 驗證此實作有多個 AdobeOrg ID。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` 回撥位置 | 0 | 此 `_satellite.pageBottom()` 函式必須存在，標籤才能運作。 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤來確保DTM可正常運作。 注意：最佳實務是讓該標籤成為 `<body>`. 若在 `<body>` 標籤，雖然它有可能運作，但由於這並非最佳實務，因此其運作可能會不正確，或產生非預期或不適當的結果。 | 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤來確保DTM可正常運作。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 自行託管 | 0 | 標籤程式庫托管於Adobe的Akamai執行個體(位於 `assets.adobedtm.com`. 自行托管是載入標籤的建議方法，因為此方法可讓您透過快取控制進一步掌控網站效能、減少對第三方指令碼的相依性，並更能掌握發佈程式。 您可以透過自己的Web托管或CDN來托管及管理標籤程式庫。 | 切換為自行托管是在頁面上載入標籤的方法。 雖然透過 Akamai CDN 進行 託管在多數情況下都是可行的，但自行託管可以改善頁面效能。<br><br>其他資訊:<ul><li>[標籤快速入門手冊](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[非同步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 應以非同步方式部署 | 0 | 標籤應以非同步方式部署，以獲得最佳效能。 | 納入 `async` 參數，以確保標籤可正常運作 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target — 中的內容 `mboxDefault` | 0 | 內容應存在於 `mboxDefault` 使用 `at.js`. | 確認有可用的內容。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
