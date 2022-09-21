---
title: 資料元素
description: 資料元素是資料字典 (或資料地圖) 的建置組塊。使用資料元素，在行銷和廣告技術之間收集、組織和傳遞資料。
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 74%

---

# 資料元素

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

資料元素是資料字典 (或資料地圖) 的建置組塊。使用資料元素，在行銷和廣告技術之間收集、組織和傳遞資料。

單一資料元素是變數，其值可對應至查詢字串、URL、Cookie 值、JavaScript 變數等資料。您可以在整個Adobe Experience Platform中透過變數名稱參考此值。 此資料元素集合會成為定義資料的字典，您可用來建立規則 (事件、條件和動作)。此資料字典會在各標籤間共用，以搭配您新增至屬性的任何擴充功能使用。

>[!IMPORTANT]
>
>變更項目會等到[發佈](../publishing/overview.md)後才生效。

在建立規則的過程中，請盡量廣泛使用資料元素，以便確立動態資料的定義，並提高標記時的效率。您只須定義資料規則一次，之後便可在多處使用。

可重複使用資料元素的概念非常強大，您應該使用它們作為最佳做法。

例如，如果您有參考頁面名稱或產品ID的特定方式，或透過附屬行銷連結的查詢字串參數或從 [!DNL AdWords]等等，您可以透過資料字典（資料元素）的來源取得資訊，然後在各種標籤規則中使用此資料，借此建立資料字典（資料元素）。

以頁面名稱為例，假設您透過參照資料層、`document.title` 元素或網站內的標題標籤來使用特定頁面名稱結構描述。Adobe Experience Platform中的標籤可讓您將資料元素建立為該特定資料點的單一參照點。 之後，您就可以在需要參照頁面名稱的任何規則中使用此資料元素。如果以後基於某些原因，您決定變更參照頁面名稱的方式 (例如您原本是參照 `document.title`，但現在您想參照特定資料層)，您不必編輯許多不同的規則即可變更該參照。只需在資料元素中變更參照一次，參照該資料元素的所有規則即會自動更新。

>[!NOTE]
>
>如果規則中未參考某個資料元素，除非特別在自訂指令碼中呼叫，否則任何頁面都不會載入該資料元素。

在規則中使用資料元素，或在指令碼中手動呼叫資料元素時，資料元素中便會填入資料。基本上，您可以：

1. [建立資料元素性](#create-a-data-element) (如果尚未這麼做的話)。
1. 在[規則](./rules.md)或自訂指令碼中使用資料元素。

## 資料元素用途

### 規則

您可以使用搜尋方塊來尋找資料元素的名稱，以在規則編輯介面中使用資料元素。

### 自訂指令碼

您可以使用 `_satellite` 物件語法，以在自訂指令碼中使用資料元素：

`_satellite.getVar('data element name');`

## 建立資料元素 {#create-a-data-element}

資料元素是規則的基礎要素。資料元素可讓您為網站上包含的任何物件在頁面上經常使用的項目建立資料字典 (或資料地圖)，而不論其來源為何 (查詢字串、URL 或 Cookie 值)。

1. 從「屬性」頁面，開啟 [!UICONTROL 資料元素] ，然後選取 **[!UICONTROL 建立新資料元素]**.
1. 命名資料元素。
1. 選取擴充功能和類型。

   可用的資料元素類型由擴充功能決定。如需核心標籤擴充功能可用類型的相關資訊，請參閱 [資料元素類型](data-elements.md#types-of-data-elements).

1. 在提供的欄位中提供關於所選類型的任何要資訊。
1. (選用) 輸入預設值。

   如果您未選取此選項，則沒有預設值。大部分的使用者會保留預設狀態。不同的系統會以不同的方式處理空白的變數。有些人會選擇輸入「none」或「n/a」等，以便在資料元素未傳回值時，在報告中保持一致。

1. 選取是否強制小寫值，以及是否移除分行和空格。
1. 選取持續時間。

   可用選項包括：

   * None
      * 值不會儲存。
   * Page view
      * 此值會保留在 JavaScript 變數中，直到頁面重新整理或載入新頁面為止。
      * 可使用 `_satellite` 物件語法，以指令碼方式來建立與設定：

         `_satellite.setVar('data_element_name')`
   * Session
      * 值會存續在瀏覽器的工作階段儲存區中，直到瀏覽器標籤關閉為止。
      * 整個網站瀏覽期間都可使用。
   * Visitor
      * 值會無限期儲存在瀏覽器的本機儲存體中。

1. 選取「**[!UICONTROL 儲存]**」。

建立或編輯元素時，您可以儲存並建置您[使用中的程式庫](../publishing/libraries.md#active-library)。這樣會立即將變更儲存至您的程式庫並執行組建。組件狀態會隨即顯示。您也可以從 [!UICONTROL 作用中程式庫] 下拉式清單。

## 資料元素類型 {#types-of-data-elements}

資料元素類型由擴充功能決定。可建立的類型沒有限制。

以下各節會說明核心擴充功能中可用的資料元素類型。其他擴充功能則使用其他類型的資料元素。

### Cookie

任何可在下列欄位中參考的可用網域 Cookie：Cookie 名稱欄位。

#### 範例：

`cookieName`

### 自訂程式碼

在UI中可以選取  [!UICONTROL 開啟編輯器] 和在編輯器視窗中插入程式碼。

您必須在編輯器視窗中輸入傳回陳述式，以指明應設為資料元素值的值。如果未包含傳回陳述式，資料元素會解析為 `undefined`。這會觸發遞補機制開始尋找所儲存的值；如果未儲存任何值，則系統會尋找預設值。

**範例：**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

自訂程式碼可接受呼叫規則的 `event` 物件做為引數。這可讓程式碼讀取其中的值。

**範例：**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

您可以使用 `_satellite` 物件語法，在自訂指令碼中使用此方法：

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

使用百分比時(`%`)語法，您只需指定資料元素名稱。 不需指定 `event`。

```text
%data element name%
```

### DOM 屬性

任何可擷取的元素值，例如 div 或 H1 標籤。

#### 範例：

CSS 選擇器鏈結：

`id#dc logo img`

取得下列項目的值：

`src`

### JavaScript 變數

任何可用的 JavaScript 物件或變數可使用下列路徑欄位參照。

如果您想要在標籤中收集JavaScript變數或物件屬性，並搭配任何擴充功能或規則使用，則可使用資料元素來擷取這些值。 這樣的話，您可以在全部規則中參照資料元素，而如果資料來源有所變更，您只需在單一位置變更來源的參照（資料元素）即可。

例如，假設您的標記包含稱為 `Page_Name` 的 JavaScript 變數，如下所示：

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

建立資料元素時，您必須提供該變數的路徑。

如果您使用資料收集器物件作為資料層的一方，只需在路徑中使用點記號來參照您要擷取到資料元素中的物件和屬性，如 `_myData.pageName` 或 `digitalData.pageName` 等等。

#### 範例：

`window.document.title`

### 本機儲存

在 [!UICONTROL 本地儲存項目名稱] 欄位。

本機儲存讓瀏覽器能在頁面之間儲存資訊 ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp))。本機儲存的運作方式與Cookie類似，但更大也更有彈性。

使用提供的欄位來指定您為本機儲存項目建立的值，例如 `lastProductViewed.`

### 頁面資訊

使用這些資料點來擷取頁面資訊，以便用於規則邏輯或者傳送資訊至 [!DNL Analytics] 或外部追蹤系統。

您可以選取下列其中一個頁面屬性以用於資料元素：

* URL
* 主機名稱
* 路徑名稱
* 通訊協定
* 反向連結
* 標題

### 查詢字串參數

在 [!UICONTROL URL參數] 欄位。

只需指定名稱部分，且任何特殊指示項都應省略 (例如「?」或「=」)

#### 範例：

`contentType`

### 隨機數字

使用此資料元素產生隨機數字。它通常用於取樣資料或建立ID，例如點擊ID。 隨機數字也可用來模糊化敏感資料，或對其執行 Salt 處理。某些範例可能包括：

* 產生點擊 ID
* 將數字串聯至使用者代號或時間戳記以確保獨特性
* 對 PII 資料執行單向雜湊
* 隨機決定在網站上顯示調查要求的時機

指定隨機數字的最小值和最大值。

**預設值：**

最小：0

最大：1000000000

### 工作階段儲存

在 [!UICONTROL 會話儲存項名稱] 欄位。

工作階段儲存與本機儲存類似，除了在工作階段結束後會捨棄資料，但本機儲存或 Cookie 可能會保留資料。

### 訪客行為

與「頁面資訊」類似，此資料元素使用常見行為類型，在規則或其他Platform解決方案中擴充邏輯。

選取下列其中一個訪客行為屬性：

* 登陸頁面
* 流量來源
* 網站逗留分鐘數
* 工作階段計數
* 工作階段頁面檢視計數
* 期限頁面檢視計數
* 新訪客身分

常見的使用案例包括：

* 訪客在網站逗留 5 分鐘後顯示調查
* 如果這是造訪的登陸頁面，請填入 [!DNL Analytics] 量度
* 在 X 次工作階段計數後向訪客顯示新活動內容
* 如果這是首次訪客，則顯示電子報註冊

## 內建資料元素

如果您先前曾使用下列任何資料元素，則必須建立其他自訂資料元素：

* URI
* 通訊協定
* 主機名稱
