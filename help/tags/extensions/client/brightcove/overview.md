---
title: BrightCove視頻跟蹤擴展概述
description: 瞭解Adobe Experience Platform的BrightCove視頻跟蹤標籤擴展。
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 37%

---

# BrightCove視頻跟蹤擴展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## 先決條件

Adobe Experience Platform的每個標籤屬性都需要在擴展螢幕中安裝和配置以下擴展：

* Adobe Analytics
* Experience Cloud 訪客 ID 服務
* 已安裝核心擴充功能

使用每個要呈現視頻播放器的網頁HTML中的「In-Page embed code(Advanced)」代碼段。 「In-Page Embed Code(Advanced)」HTML代碼段位於 [Brightcove文檔](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage)。 以下連結提供了有關 [如何為預覽和已發佈視頻播放器生成嵌入代碼](https://studio.support.brightcove.com/players/generating-player-embed-code.html)。

此擴展版1.1.0支援在單個網頁上嵌入多個BrightCove視頻。 如果有多個 `id` 高級嵌入標籤中的屬性，確保它們各具有唯一值。 比如說， `player1`。 `player2`等等。

>[!NOTE]
>
>在具有多個視頻的頁面上，每個視頻在該頁面上執行的標籤規則中使用相同的配置集。 例如，若您建立的規則是要在影片播放到 50% 時觸發事件，頁面上的每個影片都會在 50% 的提示點觸發規則。

如果使用此副檔名的網頁在相關指令碼完全載入之前與視頻交互，則可以採取兩個操作來解決此問題。 首先可以同步載入標籤庫，然後放置 `<script type="text/javascript">\_satellite.pageBottom();\</script\>` 在頁面上嵌入視頻之前的元素。

查看 [BrightCove API文檔](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) 的子菜單。

## 資料元素

擴充功能中有 7 個可用的資料元素，且皆無需設定。

* **播放頭位置：** 當在標籤規則內調用此資料元素時，它以秒為單位記錄播放頭位置在視頻時間線上的位置。
* **影片帳戶 ID：**&#x200B;此資料元素會記錄所發佈影片的 Brightcove 帳戶 ID。
* **影片長度：**&#x200B;此資料元素會記錄影片內容長度 (以秒為單位)。此外，您可在 Analytics 中建立計算量度，將秒數換算成分鐘或小時。
* **視頻廣告支援：** 此資料元素指定視頻中是否支援廣告。
* **影片 ID：**&#x200B;此資料元素會指定與影片相關聯的 BrightCove ID。
* **影片名稱：**&#x200B;此資料元素會指定描述影片的名稱或易懂名稱。
* **視頻標籤：** 此資料元素指定與視頻關聯的特定指令碼。

## 事件

擴充功能提供 7 種事件，其中只有「自訂提示點追蹤」需要設定。

* **自訂提示點追蹤：**&#x200B;影片播放到指定的臨界值百分比時，就會觸發此事件。例如，如果視頻長度為60秒，而指定的提示點為50%，則事件將在30秒標籤處觸發。

>[!NOTE]
>
>請注意，每次影片播放到提示點時，就會觸發此事件。例如，如果使用者達到 50% 標記處，在 50% 標記處前搜尋影片，之後再次來到 50% 標記處時，仍會再次觸發事件。

* **視頻已完成：** 視頻完全完成時，此事件將觸發。
* **視頻載入的元資料：** 當播放器收到初始持續時間和維度資訊時，將觸發此事件。
* **影片暫停：**&#x200B;影片暫停播放時會觸發此事件。
* **影片繼續：**&#x200B;在暫停事件後繼續播放影片內容，就會觸發此事件。
* **視頻螢幕更改：** 當視頻進入或退出全屏模式時，事件將觸發。
* **影片開始：**&#x200B;第一次播放影片內容時會觸發此事件。

## 使用方式

可以為每個視頻事件（上面列出的七個事件）設定一個標籤規則。 為要跟蹤的每個事件建立特定標籤規則。 如果不想跟蹤事件，只需省略以建立事件規則。

規則包含三個動作：

1. 設定 Adobe Analytics 變數（為上面列出的所有或某些資料元素建立資料元素。）
1. 傳送 Adobe Analytics 信標。
1. 清除 Adobe Analytics 變數。

## 「視頻開始」的標籤規則示例

將包括以下視頻擴展對象：

* **事件**

   1. 影片開始：此事件會在訪客開始播放 BrightCove 影片時觸發規則。

* **條件**

   1. None

* **動作**

   1. 在 Analytics 的「設定變數」動作中，設定：

      * **影片開始**&#x200B;事件 (範例：event17)
      * 用於 **視頻名稱** 資料元素(示例：eVar10)
      * 用於 **視頻持續時間** 資料元素(示例：eVar11)
      * 用於 **當前視頻位置** 資料元素(示例：eVar12)
   1. Analytics 的「傳送信標」動作 (`s.tl`)
   1. Analytics 的「清除變數」動作


>[!TIP]
>
>對於可能不想為每個視頻元素設定多個eVar或道具的用戶，資料元素值被連接為替代方法。 然後，使用分類規則生成器工具將它們分析為分類報告。 查看 [分類規則生成器工具](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) 的子菜單。 最後，將它們作為一段在Analysis Workspace應用。
>
>為此，請建立一個稱為「視頻元資料」之類的新資料元素，並對其進行寫程式，以將所有視頻資料元素（上面列出）拉入並連接在一起。

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
