---
title: YouTube影片追蹤擴充功能概觀
description: 瞭解Adobe Experience Platform中的YouTube影片追蹤標籤擴充功能。
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 627835011784ffca8487d446c04c6948dfff059d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 30%

---

# YouTube影片追蹤擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

**先決條件**

Adobe Experience Platform中的每個標籤屬性都需要從「擴充功能」畫面安裝及設定下列擴充功能：

* Adobe Analytics
* Experience Cloud 訪客 ID 服務
* 核心擴充功能

在視訊播放器將轉譯的每個網頁的HTML中，使用Google開發人員檔案中的[「使用\&lt;iframe\>標籤嵌入播放器」](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds)程式碼片段。

此擴充功能（2.0.1版）可支援在同一網頁內嵌一或多部YouTube影片，方法是在iframe指令碼標籤中插入具有唯一值的`id`屬性，並將`enablejsapi=1`和`rel=0`附加至`src`屬性值的結尾（若尚未包含）。 例如：

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

此擴充功能也設計來動態檢查唯一ID屬性值，例如`player1`，不論`enablejsapi`和`rel`查詢字串引數是否存在，也不論其預期值是否正確。 因此，可以將YouTube指令碼標籤新增至具有或不具有`id`屬性，以及是否包含`enablejsapi`和`rel`查詢字串引數的網頁。

>[!NOTE]
>
>在含有多個視訊的頁面上，每個視訊會使用在該頁面上執行的標籤規則中設定的相同組態。 例如，若您建立的規則是要在影片播放到 50% 時觸發事件，頁面上的每部影片都會在 50% 的提示點觸發規則。

擴充功能需仰賴下列邏輯來重寫iFrame：

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

因此，頁面載入後會有稍微閃爍的現象。 這是預期中的正常行為。

## 資料元素

擴充功能中有6個可用的資料元素，且皆無需設定。

* **播放點位置：**&#x200B;在標籤規則呼叫時，記錄影片時間軸上的播放點位置（以秒為單位）。
* **影片 ID：**&#x200B;指定與影片相關聯的 YouTube ID。
* **影片名稱：**&#x200B;指定描述影片的名稱或易記名稱。
* **影片 URL：**&#x200B;傳回目前所載入/播放影片的 YouTube.com URL。
* **影片長度：**&#x200B;記錄影片內容長度 (以秒為單位)。
* **擴充功能版本：**&#x200B;此資料元素會記錄YouTube追蹤擴充功能版本，例如「Video Tracking_YouTube_2.0.0」。

## 事件

擴充功能提供 8 種事件，其中只有「自訂提示點追蹤」需要設定。

* **影片就緒：**&#x200B;影片收到提示並準備播放時觸發此事件。
* **影片開始：**&#x200B;影片首次開始播放及 `player.getCurrentTime() === 0` 時觸發此事件。
* **影片重播：**&#x200B;系統提示播放影片時觸發此事件，並在首次播放後重播。每次重播都會觸發此事件。
* **影片暫停：**&#x200B;影片暫停播放時觸發此事件。
* **影片繼續：**&#x200B;影片繼續播放及 `player.getCurrentTime() !== 0` 時觸發此事件。
* **自訂提示追蹤：**&#x200B;影片播放到指定的臨界值百分比時觸發此事件。 例如，如果影片長度為60秒，而指定的提示點為50%，則播放點位置等於30秒時會觸發此事件。 「提示點追蹤」適用於首次播放和重播。請注意，如果使用者在提示點之間隨機搜尋片段，事件不會觸發。 唯有當播放點越過時間軸上計算的提示點位置，且視訊播放器正在播放時，才會觸發提示點事件。
* **影片緩衝：**&#x200B;播放器開始播放影片前下載特定數量的資料時，就會觸發此事件。
* **影片結束：**&#x200B;影片播放完畢時觸發此事件。

## 使用方式

您可以為每個視訊事件（即上方列出的七個事件）設定一個標籤規則。 為每個您要追蹤的事件建立特定的標籤規則。 如果您不想追蹤事件，只需省略以為其建立規則即可。

規則包含三個動作：

* **設定變數：**&#x200B;設定 Adobe Analytics 變數 (對應至所有或部分包含的資料元素)。
* **傳送信標：**&#x200B;以自訂連結追蹤呼叫的形式傳送Adobe Analytics信標，並提供「連結名稱」的值。
* **清除變數：**&#x200B;清除 Adobe Analytics 變數。

## 「影片開始」的標籤規則範例

需包括以下影片擴充功能物件。

* **事件**：「影片開始」(此事件會在訪客開始播放YouTube影片時觸發規則)。

* **條件**：無

* **動作**：使用&#x200B;**Analytics擴充功能**&#x200B;來「設定變數」動作，以對應：

   * 視訊開始事件，
   * 「影片長度」資料元素的 prop/eVar
   * 「影片 ID」資料元素的 prop/eVar
   * 「影片名稱」資料元素的 prop/eVar
   * 「影片 URL」資料元素的 prop/eVar

  接著加入「傳送信標」動作(`s.tl`)，其連結名稱為「視訊開始」，之後緊接著「清除變數」動作。

>[!TIP]
> 
>對於無法對每個視訊元素使用多個eVar或prop的實作，可在Platform中串連資料元素值，使用「分類規則產生器」工具剖析為分類報表(如[https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)所述)，然後套用為Analysis Workspace中的區段。

若要串連視訊資訊值，請建立名為「視訊中繼資料」的新資料元素，並將其設定為提取所有視訊資料元素（如上所列），接著將其彙整起來。 例如：

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

如需如何在Platform內有效建立及運用資料元素的詳細資訊，請閱讀[資料元素](../../../ui/managing-resources/data-elements.md)檔案。
