---
title: BrightCove影片追蹤擴充功能概觀
description: 瞭解Adobe Experience Platform中的BrightCove影片追蹤標籤擴充功能。
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 35%

---

# BrightCove影片追蹤擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

## 先決條件

Adobe Experience Platform中的每個標籤屬性都需要在「擴充功能」畫面中安裝並設定下列擴充功能：

* Adobe Analytics
* Experience Cloud 訪客 ID 服務
* 已安裝核心擴充功能

在影片播放器預計運行的每個網頁的HTML中，使用「頁面內嵌程式碼（進階）」程式碼片段。 您可以在[Brightcove檔案](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage)中找到「頁面內嵌程式碼（進階）」HTML片段。 下列連結提供有關[如何產生預覽和已發佈視訊播放器的內嵌程式碼的詳細資訊](https://studio.support.brightcove.com/players/generating-player-embed-code.html)。

此1.1.0版擴充功能支援在單一網頁內嵌多個BrightCove影片。 如果進階內嵌標籤中有多個`id`屬性，請確定每個屬性都有唯一值。 例如，`player1`、`player2`等。

>[!NOTE]
>
>在有多個影片的頁面上，每個影片皆需使用該頁面所執行標籤規則所設定的相同組態。 例如，若您建立的規則是要在影片播放到 50% 時觸發事件，頁面上的每個影片都會在 50% 的提示點觸發規則。

如果在相關指令碼完全載入之前，使用此擴充功能的網頁與視訊互動，您有兩個動作可加以修正。 首先，標籤程式庫可以同步載入，其次，請將`<script type="text/javascript">\_satellite.pageBottom();\</script\>`元素置於頁面所內嵌的視訊之前。

請參閱[BrightCove API檔案](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer)，以取得此擴充功能中使用的元件方法與事件的詳細資訊。

## 資料元素

擴充功能中有 7 個可用的資料元素，且皆無需設定。

* **播放點位置：**&#x200B;在標籤規則中呼叫此資料元素時，它會以秒為單位記錄播放點在視訊時間軸上的位置。
* **影片帳戶 ID：**&#x200B;此資料元素會記錄所發佈影片的 Brightcove 帳戶 ID。
* **影片長度：**&#x200B;此資料元素會記錄影片內容長度 (以秒為單位)。此外，您可在 Analytics 中建立計算量度，將秒數換算成分鐘或小時。
* **視訊廣告支援：**&#x200B;此資料元素會指定是否支援視訊內的廣告。
* **影片 ID：**&#x200B;此資料元素會指定與影片相關聯的 BrightCove ID。
* **影片名稱：**&#x200B;此資料元素會指定描述影片的名稱或易懂名稱。
* **視訊標籤：**&#x200B;此資料元素會指定與視訊相關的特定指令碼。

## 事件

擴充功能提供 7 種事件，其中只有「自訂提示點追蹤」需要設定。

* **自訂提示點追蹤：**&#x200B;影片播放到指定的臨界值百分比時，就會觸發此事件。例如，如果影片長度為60秒，而指定的提示點為50%，則事件會在30秒標籤處觸發。

>[!NOTE]
>
>請注意，每次影片播放到提示點時，就會觸發此事件。例如，如果使用者達到 50% 標記處，在 50% 標記處前搜尋影片，之後再次來到 50% 標記處時，仍會再次觸發事件。

* **影片完成播放：**&#x200B;影片播放完畢時會觸發此事件。
* **視訊載入中繼資料：**&#x200B;當播放器收到初始持續時間和維度資訊時，就會觸發此事件。
* **影片暫停：**&#x200B;影片暫停播放時會觸發此事件。
* **影片繼續：**&#x200B;在暫停事件後繼續播放影片內容，就會觸發此事件。
* **影片畫面變更：**&#x200B;影片進入或退出全熒幕模式時，就會觸發此事件。
* **影片開始：**&#x200B;第一次播放影片內容時會觸發此事件。

## 使用方式

您可以為每個視訊事件（即上方列出的七個事件）設定一個標籤規則。 為每個您要追蹤的事件建立特定的標籤規則。 如果您不想追蹤事件，只需省略以為其建立規則即可。

規則包含三個動作：

1. 設定 Adobe Analytics 變數（為上方列出的所有或部分資料元素建立資料元素。）
1. 傳送 Adobe Analytics 信標。
1. 清除 Adobe Analytics 變數。

## 「影片開始」的標籤規則範例

需包括以下影片擴充功能物件：

* **事件**

   1. 影片開始：此事件會在訪客開始播放 BrightCove 影片時觸發規則。

* **條件**

   1. None

* **動作**

   1. 在 Analytics 的「設定變數」動作中，設定：

      * **影片開始**&#x200B;事件 (範例：event17)
      * **影片名稱**&#x200B;資料元素的prop/eVar(範例：eVar10)
      * **視訊持續時間**&#x200B;資料元素的prop/eVar(範例：eVar11)
      * **目前影片位置**&#x200B;資料元素的prop/eVar(範例：eVar12)

   1. Analytics 的「傳送信標」動作 (`s.tl`)
   1. Analytics 的「清除變數」動作

>[!TIP]
>
>若您不想為每個視訊元素布建多個eVar或prop，資料元素值會串連為替代方法。 接著，系統會使用「分類規則產生器」工具，將其剖析為分類報表。 如需詳細資訊，請參閱[分類規則產生器工具](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=zh-Hant)檔案。 最後，這些區段可套用為Analysis Workspace中的區段。
>
>若要這麼做，請建立「視訊中繼資料」之類的新資料元素，並將其設定為提取所有視訊資料元素（如上所列），接著將其串連。

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
