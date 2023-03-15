---
title: 非同步部署
description: 了解如何在網站上非同步部署Adobe Experience Platform標籤程式庫。
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 55%

---

# 非同步部署 {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="非同步部署"
>abstract="如果啟用此選項，在剖析此指令碼標籤時，瀏覽器將開始載入JavaScript檔案，但與其等待程式庫載入及執行，瀏覽器會繼續剖析及轉譯其餘的檔案。 這可以改善網頁效能，但對於執行特定規則的方式有重要影響。 如需詳細資訊，請參閱文件。"

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

產品所需的JavaScript程式庫效能和非封鎖部署，對Adobe Experience Cloud使用者而言日益重要。 工具，例如 [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) 建議使用者變更在網站上部署Adobe程式庫的方式。 本文說明如何以非同步方式使用AdobeJavaScript程式庫。

## 同步與非同步

### 同步部署

程式庫在頁面的 `<head>` 標籤中通常是同步載入。例如：

```markup
<script src="example.js"></script>
```

根據預設，瀏覽器會剖析文件並到達這一行，然後開始從伺服器擷取 JavaScript 檔案。瀏覽器會等到檔案傳回為止，然後剖析並執行 JavaScript 檔案。最後，它會繼續剖析其餘的 HTML 文件。

如果剖析器在轉譯顯示內容之前遇到 `<script>` 標籤，內容顯示則會延遲。如果載入的 JavaScript 檔案在向使用者顯示內容時並非絕對必要，您未必需要讓訪客等待內容出現。程式庫愈大，延遲時間愈長。因此，[!DNL Google PageSpeed] 或 [!DNL Lighthouse] 等網站效能基準工具通常會同步標幟載入的指令碼。

如果您有許多要管理的標籤，標籤管理程式庫可能會快速擴大。

### 非同步部署

您可以將 `async` 屬性新增到 `<script>` 標籤，以非同步載入任何程式庫。例如：

```markup
<script src="example.js" async></script>
```

這會向瀏覽器指出，在剖析此指令碼標記時，瀏覽器應開始載入 JavaScript 檔案，但與其等待程式庫載入及執行，瀏覽器應繼續剖析及轉譯其餘的文件。

## 非同步部署的考量事項

如上所述，在同步部署中，瀏覽器會在Adobe Experience Platform標籤庫載入及執行時，暫停剖析及轉譯頁面。 另一方面，在非同步部署中，瀏覽器會在程式庫載入時，繼續剖析及轉譯頁面。標籤程式庫可能在何時完成載入與頁面剖析及轉譯之間相關性的變化，這些都是您必須納入考量的事項。

首先，因為標籤程式庫可能會在頁面底部剖析及執行完之前或之後完成載入，您不應再呼叫 `_satellite.pageBottom()` 從頁面程式碼(`_satellite` 在程式庫載入後才可用)。 這在 [非同步載入標籤內嵌程式碼](#loading-the-tags-embed-code-asynchronously).

接著，標籤程式庫可在 [`DOMContentLoaded`](https://developer.mozilla.org/zh-TW/docs/Web/Events/DOMContentLoaded) 瀏覽器事件（DOM就緒）已發生。

因為這兩點，值得說明的是 [程式庫已載入](../../extensions/client/core/overview.md#library-loaded-page-top), [頁面底部](../../extensions/client/core/overview.md#page-bottom), [DOM已就緒](../../extensions/client/core/overview.md#page-bottom)，和 [視窗已載入](../../extensions/client/core/overview.md#window-loaded) 非同步載入標籤程式庫時，從核心擴充功能中輸入事件類型。

如果您的標籤屬性包含下列四個規則：

* 規則 A：使用程式庫已載入事件類型
* 規則 B：使用頁面底部事件類型
* 規則 C：使用 DOM 已就緒事件類型
* 規則 D：使用視窗已載入事件類型

無論標籤程式庫何時完成載入，所有規則必定都會執行，而且會依下列順序執行：

規則 A → 規則 B → 規則 C → 規則 D

雖然順序一律會強制執行，但有些規則可能會在標籤程式庫完成載入時立即執行，而有些可能會稍後執行。 當標籤程式庫完成載入時，會發生下列情況：

1. 規則 A 會立即執行。
1. 如果 `DOMContentLoaded` 瀏覽器事件 (DOM Ready) 已發生，規則 B 和規則 C 就會立即執行。否則，規則 B 和規則 C 會在 [`DOMContentLoaded`](https://developer.mozilla.org/zh-TW/docs/Web/Events/DOMContentLoaded) 瀏覽器事件發生的稍後執行。
1. 如果 [`load`](https://developer.mozilla.org/zh-TW/docs/Web/Events/load) 瀏覽器事件 (已載入視窗) 已發生，則會立即執行規則 D。否則，當 [`load`](https://developer.mozilla.org/zh-TW/docs/Web/Events/load) 瀏覽器事件發生時，規則 D 將在稍後執行。請注意，如果您已根據指示安裝標籤程式庫，則標籤程式庫 *always* 在完成載入之前 [`load`](https://developer.mozilla.org/zh-TW/docs/Web/Events/load) 瀏覽器事件。

將這些原則套用到您自己的網站時，請考量下列事項：

* **使用程式庫已載入事件類型的規則，可能會在資料層完全載入之前執行。**  這可能會導致規則的動作在遺失資料的狀態下執行，因為頁面上還沒有資料。您可以調整規則設定，藉此緩解這些類型的問題。舉例來說，與其讓程式庫已載入事件類型觸發規則，您可以改用自訂事件或直接呼叫事件類型，這會在資料層完成載入時，立即由頁面程式碼觸發。
* **非同步載入程式庫時，頁面底部事件類型不會特別提供值。**  請改為考慮使用程式庫已載入、DOM 已就緒、視窗已載入或其他事件類型。

如果您發現順序錯亂，您可能有一些需要處理的時間問題。針對需要精準時間的部署，您可能需要使用事件監聽器以及自訂事件或直接呼叫事件類型，讓其實施更強大且一致。

## 非同步載入標籤內嵌程式碼

標籤可提供切換，讓您在設定 [環境](../publishing/environments.md). 您也可以自行設定非同步載入：

1. 將非同步屬性新增到 `<script>` 標籤以非同步載入指令碼。

   針對標籤內嵌程式碼，這表示會變更此項目：

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   這個：

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. 移除您之前可能在標籤底部新增的任何程式碼：

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   此程式碼會告訴Platform瀏覽器剖析器已到達頁面底部。 此時之前，標籤可能不會載入及執行，因此呼叫 `_satellite.pageBottom()` 會導致錯誤，而Page Bottom事件類型可能不會如預期般運作。
