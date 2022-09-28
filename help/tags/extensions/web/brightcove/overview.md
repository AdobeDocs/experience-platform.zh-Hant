---
title: BrightCove影片追蹤擴充功能概述
description: 了解Adobe Experience Platform中的BrightCove影片追蹤標籤擴充功能。
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 37%

---

# BrightCove影片追蹤擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## 先決條件

Adobe Experience Platform中的每個標籤屬性都需要在「擴充功能」畫面中安裝並設定下列擴充功能：

* Adobe Analytics
* Experience Cloud 訪客 ID 服務
* 已安裝核心擴充功能

在影片播放器要呈現的每個網頁HTML中，使用「頁面內嵌程式碼（進階）」程式碼片段。 您可以在 [Brightcove檔案](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). 下列連結提供 [如何為預覽和已發佈的視訊播放器產生內嵌程式碼](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

此1.1.0版擴充功能可支援在單一網頁內嵌多個BrightCove影片。 如果有多個 `id` 屬性，請確定每個屬性都有不重複的值。 例如， `player1`, `player2`等。

>[!NOTE]
>
>在有多個影片的頁面上，每個影片皆使用該頁面上執行之標籤規則中設定的相同組態。 例如，若您建立的規則是要在影片播放到 50% 時觸發事件，頁面上的每個影片都會在 50% 的提示點觸發規則。

如果在相關指令碼完全載入前使用此擴充功能的網頁與影片互動，您可以採取兩個動作來修正問題。 首先，標籤庫可以同步載入，其次，將 `<script type="text/javascript">\_satellite.pageBottom();\</script\>` 元素。

請參閱 [BrightCove API檔案](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) 以取得此擴充功能中使用的元件方法和事件的詳細資訊。

## 資料元素

擴充功能中有 7 個可用的資料元素，且皆無需設定。

* **播放點位置：** 在標籤規則內呼叫此資料元素時，它會以秒為單位記錄視訊時間軸上的播放點位置。
* **影片帳戶 ID：**&#x200B;此資料元素會記錄所發佈影片的 Brightcove 帳戶 ID。
* **影片長度：**&#x200B;此資料元素會記錄影片內容長度 (以秒為單位)。此外，您可在 Analytics 中建立計算量度，將秒數換算成分鐘或小時。
* **視訊廣告支援：** 此資料元素會指定視訊中是否支援廣告。
* **影片 ID：**&#x200B;此資料元素會指定與影片相關聯的 BrightCove ID。
* **影片名稱：**&#x200B;此資料元素會指定描述影片的名稱或易懂名稱。
* **影片標籤：** 此資料元素會指定與視訊相關聯的特定指令碼。

## 事件

擴充功能提供 7 種事件，其中只有「自訂提示點追蹤」需要設定。

* **自訂提示點追蹤：**&#x200B;影片播放到指定的臨界值百分比時，就會觸發此事件。例如，如果影片長度為60秒，而指定的提示點為50%，則事件會在30秒標籤處觸發。

>[!NOTE]
>
>請注意，每次影片播放到提示點時，就會觸發此事件。例如，如果使用者達到 50% 標記處，在 50% 標記處前搜尋影片，之後再次來到 50% 標記處時，仍會再次觸發事件。

* **影片完成：** 影片播放完畢時會觸發此事件。
* **視訊載入中繼資料：** 當播放器收到初始持續時間和維度資訊時，就會觸發此事件。
* **影片暫停：**&#x200B;影片暫停播放時會觸發此事件。
* **影片繼續：**&#x200B;在暫停事件後繼續播放影片內容，就會觸發此事件。
* **視訊畫面變更：** 影片進入或退出全螢幕模式時，就會觸發此事件。
* **影片開始：**&#x200B;第一次播放影片內容時會觸發此事件。

## 使用方式

每個視訊事件（即上方列出的七個事件）皆可設定一個標籤規則。 為每個您要追蹤的事件建立特定的標籤規則。 如果您不想追蹤事件，只需略過以建立事件的規則即可。

規則包含三個動作：

1. 設定 Adobe Analytics 變數（為上述所有或部分資料元素建立資料元素。）
1. 傳送 Adobe Analytics 信標。
1. 清除 Adobe Analytics 變數。

## 「影片開始」的標籤規則範例

將包括下列視訊擴充功能物件：

* **事件**

   1. 影片開始：此事件會在訪客開始播放 BrightCove 影片時觸發規則。

* **條件**

   1. None

* **動作**

   1. 在 Analytics 的「設定變數」動作中，設定：

      * **影片開始**&#x200B;事件 (範例：event17)
      * 的prop/eVar **視訊名稱** 資料元素(範例：eVar10)
      * 的prop/eVar **影片長度** 資料元素(範例：eVar11)
      * 的prop/eVar **當前視頻位置** 資料元素(範例：eVar12)
   1. Analytics 的「傳送信標」動作 (`s.tl`)
   1. Analytics 的「清除變數」動作


>[!TIP]
>
>若不想針對每個影片元素布建多個eVar或prop，資料元素值會串連為替代方法。 接著，會使用Classification Rule Builder Tool剖析它們並製成分類報表。 請參閱 [分類規則產生器工具](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) 檔案以取得詳細資訊。 最後，這些區段會以區段形式套用至Analysis Workspace。
>
>若要這麼做，請建立「Video MetaData」之類的新資料元素，並將其設定為提取所有視訊資料元素（如上所列），然後串連這些資料元素。

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
