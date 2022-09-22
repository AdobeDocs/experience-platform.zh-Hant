---
title: Google資料層擴充功能
description: 了解Adobe Experience Platform中的Google用戶端資料層標籤擴充功能。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# Google資料層擴充功能（測試版）

>[!IMPORTANT]
>
>此擴充功能目前仍在測試階段，尚未在生產環境中完全測試。

Google資料層擴充功能可讓您在標籤實施中使用Google資料層。 此擴充功能可獨立使用，或與Google解決方案以及Google的開放原始碼同時使用 [資料層協助程式庫](https://github.com/google/data-layer-helper).

Helper Library提供與Adobe用戶端資料播出時(ACDL)類似的事件導向功能。 Google資料層擴充功能的資料元素、規則和動作，提供與 [ACDL擴充功能](../client-data-layer/overview.md).

## 期限

擴充功能1.0.x版為測試版。 此擴充功能尚未在生產環境中完全測試。

## 安裝

若要安裝擴充功能，請導覽至資料收集UI中的擴充功能目錄，然後選取 **Google資料層**.

安裝後，擴充功能會在每次標籤程式庫載入您的網站時建立或存取資料層。

## 擴充功能檢視

設定擴充功能時(安裝擴充功能時或選取 **[!UICONTROL 設定]** 從擴充功能目錄)，您必須定義擴充功能所使用的資料層名稱。 如果載入程式庫時沒有顯示已設定名稱的資料層，擴充功能會改為建立資料層。

>[!NOTE]
>
>Google或Adobe程式碼是否先載入並建立資料層並不重要。 兩個系統都會建立資料層（如果不存在），或使用現有的資料層。

依預設，資料層會使用Google預設名稱 `dataLayer`.

## 活動

擴充功能可讓您監聽資料層內的變更（事件）。 事件可以是下列任一項：

* 標籤事件（例如要載入的程式庫）
* JavaScript事件
* 將資料推送至資料層，使用 `event` 關鍵字。

請務必了解 [`event` 關鍵字](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) 將資料推送至Google資料層時，會與Adobe用戶端資料層類似。 此 `event` 關鍵字會變更Google資料層的行為，因此擴充功能的行為會隨之更新。

以下各節將概述擴充功能可監聽的不同事件類型。

### 監聽所有推送至資料層

如果您選取此選項，擴充功能會監聽對資料層所做的任何變更。

### 接聽推播排除事件

如果您選取此選項，擴充功能會監聽任何推送至資料層的項目，排除事件。

接聽程式會追蹤下列推送事件範例：

```js
dataLayer.push({"data":"something"})
```

監聽程式不會追蹤下列推送事件範例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 監聽所有事件

如果您選取此選項，擴充功能會監聽任何推送至資料層的事件。

偵聽器會追蹤下列推送事件範例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

監聽程式不會追蹤下列推送事件範例：

```js
dataLayer.push({"data":"something"})
```

### 監聽特定事件

如果要監聽特定事件，請選擇此選項，以便事件偵聽器跟蹤匹配特定字串的任何事件。

例如，設定 `myEvent` 使用此設定時，偵聽器只會追蹤下列推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

您也可以使用規則運算式字串來比對事件名稱。 例如，設定 `myEvent\d` 會追蹤以 `myEvent` 後跟數字：

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 動作

以下各節將概述當包含在 [規則](../../../ui/managing-resources/rules.md).

### 推送至資料層 {#push-to-data-layer}

此動作會將JSON內容推播至資料層本身，以便直接在JSON裝載中使用資料元素。 在提供的JSON編輯器中，您可以使用百分比標籤法來參考資料元素(例如 `%dataElementName%`)。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL重置為計算狀態

>[!NOTE]
>
>此動作可從1.0.5版開始使用。

此動作會重設資料層。 若用於處理Google資料層變更的規則中，則資料層會在觸發規則時重設為資料層的計算狀態。 如果動作用於不會處理Google資料層變更的規則中，動作會清空資料層。

## 資料元素

擴充功能提供使用鍵存取資料層的唯一資料元素(例如， `page.url` 在 [以上程式碼](#push-to-data-layer))。

資料元素可提供下列任一項：

* 來自資料層的特定值(例如 `page.url`)
* 整個資料層陣列（空鍵欄位）
* 使用索引鍵(若 `event` 關鍵字)
* 整個事件物件（空鍵欄位）

擴充功能一律會優先處理事件資訊。 若資料層 `event` 處理中，一律會從該事件讀取值。 若 `event` 不存在，則會改為從直接資料層讀取值。

## 其他資訊

如需其他資訊，請參閱 [專案讀我檔案](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) 和擴充功能的資料元素和事件對話方塊中取得Advertising Cloud和Analytics的說明。
