---
title: 實施第三方圖書館
description: 瞭解在您的Adobe Experience Platform標籤擴展中托管第三方庫的不同方法。
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 68%

---

# 實作協力廠商程式庫

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

在Adobe Experience Platform，標籤擴展的主要目的之一是使您能夠輕鬆地將現有的營銷技術（庫）實施到您的網站中。 只要使用擴充功能，您就能實作協力廠商內容傳遞網路 (CDN) 提供的程式庫，不必手動編輯網站的 HTML。

在擴展中托管第三方（供應商）庫有幾種方法。 本文將概述這些實作方法，包括各方法的優缺點。

## 先決條件

本文檔要求對標籤內的擴展進行有效的理解，包括它們可以做什麼和如何構成。 查看 [擴展開發概述](./overview.md) 的子菜單。

## 基底程式碼載入程序

在標籤上下文之外，瞭解營銷技術通常如何載入到網站上非常重要。 協力廠商程式庫的廠商會提供程式碼片段 (稱為基底程式碼)，您必須將這內嵌在網站的 HTML 中，才能載入程式庫的功能。

一般而言，行銷技術的基底程式碼在您的網站上載入時，會執行類似以下的程序：

1. 設定與廠商程式庫互動所需的全域函數。
1. 載入廠商程式庫。
1. 對全域函數進行一連串初始呼叫，以便設定和追蹤。

一開始設定全域函數時，您仍可在程式庫載入完畢前呼叫函數。您所做的任何調用都會添加到基碼的排隊機制中，然後在庫載入後按順序執行。

程式庫載入完畢後，系統會採用新的全域函數，略過佇列並立即處理對函數的後續呼叫。

### 基底程式碼範例

以下JavaScript是Java的未定義基代碼的示例 [Pinterest轉換標籤](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?)將在本文檔的稍後部分中引用，以說明如何針對具有標籤的不同實施策略來調整基礎代碼：

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

簡而言之，上述基底程式碼提供[立即叫用函數運算式 (IIFE)](https://developer.mozilla.org/zh-TW/docs/Glossary/IIFE)，可建立全域函數與程式庫 (`window.pintrk`) 互動。這也會將 `https://s.pinimg.com/ct/core.js` 的值指派給 `scriptURL` 變數，而該值為程式庫所在位置。如前所述，在程式庫載入之前呼叫的所有函數都會推送至佇列 (`window.pintrk.queue`)，以便在程式庫可供使用時依序執行。

基底程式碼的以下部分與程式庫在您網站上載入的方式最為相關：

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

基底程式碼會建立指令碼元素、將其設為非同步載入，並將 `src` URL 設為 `https://s.pinimg.com/ct/core.js`。接著，基底程式碼會將該指令碼元素插入文件中的第一個指令碼元素前，將其新增至文件中。

## 標籤實現選項

下一節會以先前所示的 Pinterest 基底程式碼為例，示範在擴充功能中載入廠商程式庫的各種方法。每個示例都涉及建立 [Web擴展的操作類型](./web/action-types.md) 把圖書館裝到你的網站上。

>[!NOTE]
>
>雖然下面的示例使用操作類型進行演示，但您可以將相同的原則應用於載入站點上標籤庫的任何函式。


本文會說明下列方法：

- [實作協力廠商程式庫](#implementing-third-party-libraries)
   - [先決條件](#prerequisites)
   - [基底程式碼載入程序](#base-code-loading-process)
      - [基底程式碼範例](#base-code-example)
   - [標籤實現選項](#tags-implementation-options)
      - [在執行階段從廠商主機載入 {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [在運行時從標籤庫主機載入](#load-at-runtime-from-the-tag-library-host)
      - [直接內嵌程式庫](#embed-the-library-directly)
   - [後續步驟](#next-steps)

### 在執行階段從廠商主機載入 {#vendor-host}

託管廠商程式庫最常見的方法是使用廠商的 CDN。設定上，大多數廠商程式庫的基底程式碼都是從廠商的 CDN 載入程式庫，因此您可以設定擴充功能，從相同位置載入程式庫。

此方法通常最容易維護，因為對CDN上的檔案進行的任何更新都將由擴展自動載入。

如果使用此方法，您只需將整段基底程式碼直接貼進動作類型，如下所示：

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

或者，您也可以採取其他措施，重新調整此實作。變數 `scriptElement` 和 `firstScriptElement` 的適用範圍現在已設限於匯出函數，沒有變成全域函數的風險，因此您可以移除 IIFE。

此外，標籤提供 [核心模組](./web/core.md) 是任何擴展都可以使用的實用程式。 具體來說，`@adobe/reactor-load-script` 模組會建立指令碼元素並將其新增至文件，從遠端位置載入指令碼。針對指令碼載入程序使用此模組，您就能進一步重新調整動作程式碼：

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### 在運行時從標籤庫主機載入

使用廠商 CDN 託管程式庫有多種風險，包括 CDN 可能故障、檔案隨時可能更新而發生重大錯誤，或檔案可能遭有心人士惡意入侵。

若要消除這些疑慮，您可以選擇將廠商程式庫以個別檔案的形式加入擴充功能中。然後可以配置擴展，使得檔案與主標籤庫一起托管。 在執行階段，擴充功能會鎖定將主要程式庫傳送至網站的伺服器，從該伺服器載入廠商程式庫。

>[!IMPORTANT]
>
>部分情況下，廠商程式庫可能會從協力廠商伺服器載入額外程式碼，如同 Pinterest 廠商程式庫的範例一樣。在這些情況下，將廠商程式庫綁定您的擴充功能可能無法完全緩解所有風險疑慮。

若要實作，您必須先將廠商程式庫下載到您的電腦上。在 Pinterest 的案例中，廠商程式庫位於 [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js)。下載檔案後，您必須將檔案放在擴充功能專案中。下方範例中，該檔案位於專案目錄的 `vendor` 資料夾，名稱為 `pinterest.js`。

庫檔案在項目中後，必須更新 [擴展清單](./manifest.md) (`extension.json`)以指示供應商庫應與主標籤庫一起提供。 將路徑新增至 `hostedLibFiles` 陣列中的程式庫檔案，加以更新：

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

最後，您必須設定動作程式碼，從託管主要程式庫的同一部伺服器載入廠商程式庫。下方範例會以[上一節](#vendor-host)建立的動作程式碼為基礎來開始操作。您必須使用 [Turbine 物件](./turbine.md)，傳遞廠商檔案的檔案名稱 (不加任何路徑)，如下所示：

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

請注意，使用此方法時，必須在庫在其CDN上更新時手動更新下載的供應商檔案，並將更改釋放到新版本的擴展。

### 直接內嵌程式庫

通過直接將庫代碼嵌入操作代碼本身，可以繞過必須完全載入供應商庫的操作，這有效地使庫代碼成為主標籤庫的一部分。 使用此方法會增加主要程式庫的大小，但您不必另外提出 HTTP 要求來擷取個別檔案。

您能以[上一節](#vendor-host)建立的動作程式碼為基礎，以指令碼本身的內容取代要載入指令碼的程式：

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## 後續步驟

本文檔概述了在標籤擴展中托管第三方庫的不同方法。 雖然提供的範例著重於程式庫，但這些技巧適用於擴充功能可使用的任何程式碼片段。

請參閱整份指南中的文件連結，深入了解設定擴充功能的各種工具，包括動作類型、擴充功能資訊清單、核心模組和 Turbine 物件。
