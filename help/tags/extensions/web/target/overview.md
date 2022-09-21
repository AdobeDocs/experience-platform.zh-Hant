---
title: Adobe Target擴充功能概述
description: 了解Adobe Experience Platform中Adobe Target的標籤擴充功能。
exl-id: b1c5e25b-42ea-4835-b2d4-913fa2536e77
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 73%

---

# Adobe Target擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

您可參閱此參考文件，了解使用此擴充功能建立規則時可使用哪些選項。

## 設定 Adobe Target 擴充功能

>[!IMPORTANT]
>
> Adobe Target 擴充功能需使用 at.js。不支援 mbox.js。

如果尚未安裝Adobe Target擴充功能，請開啟屬性，然後選取 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在Target擴充功能上，然後選取 **[!UICONTROL 安裝]**.

若要設定擴充功能，請開啟 [!UICONTROL 擴充功能] 標籤，將游標暫留在擴充功能上，然後選取 **[!UICONTROL 設定]**.

![](../../../images/ext-target-config.png)

### at.js 設定

所有at.js設定（除了逾時以外）都會從Target使用者介面的at.js設定中自動擷取。 擴充功能只會在首次新增時從Target使用者介面擷取設定，因此在需要其他更新時，應在UI中管理所有設定。

下列組態選項可供使用：

#### 用戶端代碼

用戶端代碼是Target的帳戶識別碼。 在大部分情況中，此值應一律保持為預設值。

可使用資料元素進行變更。

#### 組織 ID

此 ID 會將您的實作連結至 Adobe Experience Cloud 帳戶。在大部分情況中，此值應一律保持為預設值。

可使用資料元素進行變更。

#### 全域 mbox 名稱

顯示全域 Target 要求的名稱。依預設，此名稱為 target-global-mbox，除非您在新增擴充功能前即已在 Target 使用者介面中變更名稱。

可使用資料元素進行變更。

#### 伺服器網域

作為 Target 要求傳送目標的網域。在大部分情況中，此值應一律保持為預設值。

#### 跨網域

判斷 Target 在瀏覽器中設定 Cookie 的位置。

* **停用：**&#x200B;僅在第一方網域上設定 Cookie。此為一般設定。
* **啟用：**&#x200B;在第一方網域和協力廠商 Target 網域 (「伺服器網域」) 上設定 Cookie。

#### 逾時 (毫秒)

如果未在定義的期間內收到 Target 的回應，則要求逾時，系統會顯示預設內容。在訪客工作階段期間會繼續嘗試其他要求。預設值為 3000 毫秒，可能與 Target 使用者介面中設定的「逾時」不同。

如需「逾時」設定如何運作的詳細資訊，請參閱 [Adobe Target 說明](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html)。

#### Target 使用者介面中可用的其他 at.js 設定

上提供的數個設定 [!UICONTROL 編輯at.js設定] Target UI的頁面不屬於Target擴充功能的一部分。 建議因應措施如下：

* 自動建立全域 mbox 此設定會由 Target 擴充功能中的「引發全域 mbox」動作取代。
* 程式庫頁首 此設定不屬於 Target 擴充功能的一部分。在使用「載入 Target」動作之前，先將需要在 at.js 之前載入的程式碼置於「核心擴充功能 > 自訂程式碼」動作中。
* 程式庫頁尾 此設定不屬於 Target 擴充功能的一部分。在使用「載入 Target」動作之後，將需要在 at.js 之後載入的程式碼置於「核心擴充功能 > 自訂程式碼」動作中。

## Target 擴充功能動作類型

本節說明 Target 擴充功能中可用的動作類型。

Target 擴充功能提供規則的「Then」部分中的下列動作：

### 載入 Target

將此動作新增至您的標籤規則，其中在規則內容中載入Target是可行的作法。 如此會將 at.js 程式庫載入頁面中。在大部分實作中，您網站的每個頁面上都應載入 Target。

無需設定。

### 新增 mbox 參數

新增參數至所有 mbox 要求。「載入 Target」動作必須較先使用。

1. 指定您要新增之參數的名稱和值。
1. 選取&#x200B;**加號 (+)** 圖示以新增更多參數。

### 新增全域 mbox 參數

只新增參數至全域 mbox 要求。「載入 Target」動作必須較先使用。

1. 指定您要新增之參數的名稱和值。
1. 選取&#x200B;**加號 (+)** 圖示以新增更多參數。

### 引發全域 mbox

引發頁面上的全域 mbox。「載入 Target」動作必須較先使用。

指定是否啟用主體隱藏以防止閃爍，以及在隱藏主體元素時所使用的樣式。

提供下列選項：

* **主體隱藏：**&#x200B;您可以啟用或停用此設定。預設值為 Enabled，表示 HTML BODY 隱藏。
* **主體隱藏樣式：**&#x200B;預設值為 `body{opacity:0}`。此值可以變更為其他不同值，例如 `body{display:none}`。

如需詳細資訊，請參閱 [Target 線上說明文件](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html)。

## Adobe Target 基本部署

安裝 Target 擴充功能後，您需要建立至少一個規則才能正確部署。您首先需要載入 Target 程式庫 (at.js)，指定要用於全域 mbox 的參數，然後引發全域 mbox。

具有此基本實作的 Target 規則看起來如下所示：

![](../../../images/basic_target_implementation.png)

儲存此規則後，您需要將它新增至程式庫，然後進行建立/部署，以便測試行為。

## 非同步部署的 Adobe Target 擴充功能

標籤可非同步部署。 如果您以非同步方式載入標籤程式庫，且其中包含Target，則Target也會以非同步方式載入。 這是完全支援的情況，但有一個額外考量必須處理。

在非同步部署中，頁面可以在Target程式庫完全載入並執行內容交換之前完成預設內容轉譯。 這可能會導致所謂的「閃爍」問題，即預設內容會短暫顯示，然後才會被 Target 指定的個人化內容取代。若要避免這種閃爍問題，建議您使用預先隱藏的程式碼片段，並以非同步方式載入標籤套件，以避免發生任何內容閃爍情形。

使用預先隱藏程式碼片段時應留意的事項如下：

* 載入標籤頁首內嵌程式碼之前，必須先新增程式碼片段。
* 此程式碼無法透過標籤管理，因此必須直接新增至頁面。
* 一旦發生下列事件，系統便會顯示頁面：
   * 收到全域 mbox 回應時
   * 全域 mbox 要求逾時
   * 程式碼片段本身逾時
* 應使用預先隱藏程式碼片段，在所有頁面上使用「引發全域Mbox」動作，將預先隱藏的時間減至最少。

預先隱藏的程式碼片段如下所示，且可縮小：可設定的選項位於末端：

```javascript
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

依預設，此程式碼片段會預先隱藏整個 HTML BODY。在某些情況下，您可能希望預先隱藏特定的 HTML 元素，而非整個頁面。您可以自訂 style 參數來達到此目的。以某些項目替換此參數，而只預先隱藏頁面的特定區域。

例如，若您有兩個區域，分別以 ID container-1 和 container-2 來識別，則樣式可以換成如下內容：

```css
#container-1, #container-2 {opacity: 0 !important}
```

代替預設值：

```css
body {opacity: 0 !important}
```

依預設，程式碼片段在 3000 毫秒或 3 秒後逾時。此值可自訂。
