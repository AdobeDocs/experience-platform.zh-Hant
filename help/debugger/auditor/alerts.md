---
title: 警示測試參考
description: 瞭解Auditor功能如何在Adobe Experience Platform Debugger中測試警報。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 12%

---

# 警示測試參考

此參考檔案主要探討Adobe Experience Platform Debugger中Auditor功能如何執行警示測試，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱[Auditor功能概觀](./overview.md)。

警報會顯示您應留意但不影響分數的問題。某些情況下，這些最佳實務建議可能不適用於您的實作。

| 測試 | 粗細 | 標準 | 建議 |
| --- | --- | --- | --- |
| Advertising Cloud — 實作正確的轉換標籤 | 0 | 檢查是否使用正確的轉換標記。<br><br>**警告**：使用過時的TubeMogul轉換標籤可能會導致資料遺失。 | 將您的轉換畫素升級為新的Advertising Cloud僅限影像轉換標籤。 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可輕鬆完成這項作業。 |
| Advertising Cloud — 使用正確的JS標籤 | 0 | Advertising Cloud應使用最新的JavaScript標籤。 | 將您的 Advertising Cloud JavaScript 升級至最新版本。使用過時的JavaScript版本可能會導致功能喪失。 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可輕鬆完成這項作業。 |
| Advertising Cloud — 僅限影像標籤 | 0 | Advertising Cloud 影像像素格式應符合下列其中一個建議格式： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 將您的Advertising Cloud畫素升級為新的Advertising Cloud僅限影像標籤，以確保您使用的是完整的Advertising Cloud功能。 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可輕鬆完成這項作業。 |
| Advertising Cloud — 啟用區段畫素DSP同步 | 0 | 檢查TubeMogul區段畫素是否包含DSP同步設定，並建議您將該設定新增至畫素。 「DSP同步」設定取決於查詢字串引數的使用。 總結： <ul><li>如果觸發標籤至下列任一專案：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>標籤包含URL引數`sid=`</li><li>然後檢查URL引數`cs=0`或`cs=1`是否存在，如果不存在，則建議將`cs=1`新增到這些畫素，以便提高對象符合率。</li></ul> | 將URL引數`cs=1`新增至您的Advertising Cloud畫素，以便進行DSP同步，進而提高投放對象準確率。 使用[Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可輕鬆完成這項作業。 |
| Experience CloudID服務 — 僅使用一個AdobeOrg | 0 | 在一般ECID實作中，應使用單一AdobeOrg。 | 驗證此實作有多個AdobeOrg ID。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| 啟動 — `pageBottom`回呼位置 | 0 | 必須有`_satellite.pageBottom()`函式才能讓標籤運作。 在結尾的`</body>`標籤前面加上緊鄰的內嵌指令碼，以確保DTM可正常運作。 注意：最佳實務是讓該標籤成為`<body>`中的最後一個標籤。 若將其置於`<body>`標籤內，雖然或許能運作，但由於這並非最佳實務，因此其運作可能會不正確，或產生非預期或不適當的結果。 | 在結尾的`</body>`標籤前面加上緊鄰的內嵌指令碼，以確保DTM可正常運作。 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch — 自行託管 | 0 | 標籤程式庫在Adobe的Akamai執行個體上受到託管（位於`assets.adobedtm.com`）。 自行託管是載入標籤的建議方法，因為此方法可讓您透過快取控制進一步掌控網站效能、減少對第三方指令碼的依賴，且更能掌握發佈程式。 您可以透過自己的網站託管或CDN來託管及管理標籤程式庫。 | 切換為自行託管是在頁面上載入標籤的方法。 雖然透過Akamai CDN託管在多數情況下都是可行的，但自行託管可以改善頁面效能。 <br><br>其他資訊：<ul><li>[標籤快速入門手冊](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[非同步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch — 應以非同步方式部署 | 0 | 標籤應以非同步方式部署，以發揮最佳效能。 | 將`async`引數納入內嵌指令碼，以確保標籤功能正確<br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| 目標 — `mboxDefault`中的內容 | 0 | 使用`at.js`時，內容應存在於`mboxDefault`中。 | 確認有可用的內容。 <br><br>[其他資訊](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
