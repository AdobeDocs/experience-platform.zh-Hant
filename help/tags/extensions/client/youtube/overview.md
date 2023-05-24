---
title: YouTube視頻跟蹤擴展概述
description: 瞭解YouTube視頻跟蹤標籤在Adobe Experience Platform的擴展。
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 40%

---

# YouTube視頻跟蹤擴展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

**先決條件**

Adobe Experience Platform的每個標籤屬性都要求在「擴展」螢幕中安裝和配置以下擴展：

* Adobe Analytics
* Experience Cloud 訪客 ID 服務
* 核心擴充功能

使用 [&quot;使用\嵌入播放器&lt;iframe> 標籤](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) 在要呈現視頻播放器的每個網頁的HTML中，從Google開發人員文檔中找到代碼片段。

此擴展版2.0.1支援通過插入 `id` iframe指令碼標籤中具有唯一值的屬性，並附加 `enablejsapi=1` 和 `rel=0` 到 `src` 屬性值（如果尚未包括）。 例如：

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

此擴展還設計為動態檢查唯一ID屬性值，例如 `player1`，無論 `enablejsapi` 和 `rel` 查詢字串參數存在，並且其預期值是否正確。 因此，可以將YouTube指令碼標籤添加到具有或不具有 `id` 屬性和 `enablejsapi` 和 `rel` 查詢字串參數是否包括。

>[!NOTE]
>
>在具有多個視頻的頁面上，每個視頻在該頁面上執行的標籤規則中使用相同的配置集。 例如，若您建立的規則是要在影片播放到 50% 時觸發事件，頁面上的每部影片都會在 50% 的提示點觸發規則。

擴展依賴於以下邏輯來重寫iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

因此，在載入頁面後出現輕微閃爍。 這是預期中的正常行為。

## 資料元素

擴展中有六個可用的資料元素，其中沒有一個需要配置。

* **播放頭位置：** 當在標籤規則內調用播放頭位置時，在視頻時間線上記錄播放頭位置的位置（秒）。
* **影片 ID：**&#x200B;指定與影片相關聯的 YouTube ID。
* **影片名稱：**&#x200B;指定描述影片的名稱或易記名稱。
* **影片 URL：**&#x200B;傳回目前所載入/播放影片的 YouTube.com URL。
* **影片長度：**&#x200B;記錄影片內容長度 (以秒為單位)。
* **擴展版本：** 此資料元素記錄YouTube跟蹤擴展版本，例如「視頻跟蹤YouTube2.0.0」。

## 事件

擴充功能提供 8 種事件，其中只有「自訂提示點追蹤」需要設定。

* **影片就緒：**&#x200B;影片收到提示並準備播放時觸發此事件。
* **影片開始：**&#x200B;影片首次開始播放及 `player.getCurrentTime() === 0` 時觸發此事件。
* **影片重播：**&#x200B;系統提示播放影片時觸發此事件，並在首次播放後重播。每次重播都會觸發此事件。
* **影片暫停：**&#x200B;影片暫停播放時觸發此事件。
* **影片繼續：**&#x200B;影片繼續播放及 `player.getCurrentTime() !== 0` 時觸發此事件。
* **自訂提示追蹤：**&#x200B;影片播放到指定的臨界值百分比時觸發此事件。例如，如果視頻為60秒，而指定的提示點為50%，則當播放頭位置等於30秒時，將觸發該事件。 「提示點追蹤」適用於首次播放和重播。請注意，如果用戶在提示點之間搜索，則事件不會觸發。 僅當播放頭在時間軸上越過計算的提示點位置並且視頻播放器正在播放時，提示點事件才會觸發。
* **影片緩衝：**&#x200B;播放器開始播放影片前下載特定數量的資料時，就會觸發此事件。
* **影片結束：**&#x200B;影片播放完畢時觸發此事件。

## 使用方式

可以為每個視頻事件（上面列出的七個事件）設定一個標籤規則。 為要跟蹤的每個事件建立特定標籤規則。 如果不想跟蹤事件，只需省略以建立事件規則。

規則包含三個動作：

* **設定變數：**&#x200B;設定 Adobe Analytics 變數 (對應至所有或部分包含的資料元素)。
* **傳送信標：**&#x200B;以自訂連結追蹤呼叫的形式傳送 Adobe Analytics 信標，並提供「連結名稱」的值。
* **清除變數：**&#x200B;清除 Adobe Analytics 變數。

## 「視頻開始」的標籤規則示例

將包括以下視頻擴展對象。

* **事件**:「視頻開始」(當訪問者開始播放YouTube視頻時，此事件會導致規則激發。)

* **條件**：無

* **動作**： 使用 **分析擴展** 到「設定變數」操作，映射：

   * 視頻啟動的事件，
   * 「影片長度」資料元素的 prop/eVar
   * 「影片 ID」資料元素的 prop/eVar
   * 「影片名稱」資料元素的 prop/eVar
   * 「影片 URL」資料元素的 prop/eVar

   然後，包括「發送信標」操作(`s.tl`)，連結名稱為「video start」，後跟「Clear Variables」（清除變數）操作。

>[!TIP]
> 
>對於無法使用每個視頻元素的多個eVar或道具的實現，資料元素值可以在平台內級聯，使用分類規則生成器工具分析為分類報告，如中所述 [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)，然後作為分部應用於Analysis Workspace。

若要串連影片資訊的值，請建立名為「影片中繼資料」的新資料元素，並以程式導入所有影片資料元素 (如上所列)，將所有資料元素彙整起來。例如：

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
