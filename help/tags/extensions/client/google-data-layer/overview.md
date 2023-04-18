---
title: Google資料層擴充功能
description: 了解Adobe Experience Platform中的Google用戶端資料層標籤擴充功能。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Google資料層擴充功能

Google資料層擴充功能可讓您在標籤實施中使用Google資料層。 此擴充功能可獨立使用，或與Google解決方案以及Google的開放原始碼同時使用 [資料層協助程式庫](https://github.com/google/data-layer-helper).

Helper Library提供與Adobe用戶端資料播出時(ACDL)類似的事件導向功能。 Google資料層擴充功能的資料元素、規則和動作，提供與 [ACDL擴充功能](../client-data-layer/overview.md).

## 期限

1.2.x版是生產使用中的最新測試版。

## 安裝

若要安裝擴充功能，請導覽至資料收集UI中的擴充功能目錄，然後選取 **[!UICONTROL Google資料層]**.

安裝後，擴充功能會在Adobe Experience Platform標籤程式庫的每個負載上建立或存取資料層。

## 擴充功能檢視

擴充功能組態可用來定義擴充功能所使用的資料層名稱。 如果載入Adobe Experience Platform標籤時沒有顯示已設定名稱的資料層，擴充功能會建立資料層。

資料層名稱預設為Google預設名稱 `dataLayer`.

>[!NOTE]
>
>Google或Adobe程式碼是否先載入並建立資料層並不重要。 兩個系統的行為都相同 — 如果資料層不存在，請建立該資料層，或使用現有資料層。

## 活動

>[!NOTE]
>
>這個詞 _事件_ 在Adobe Experience Platform標籤中使用事件導向資料層時，會超載。 _事件_ 可以是：
> - Adobe Experience Platform標籤事件（程式庫已載入等）。
> - JavaScript事件。
> - 將資料推送至資料層，使用 _事件_ 關鍵字。


擴充功能可讓您監聽資料層的變更。

>[!NOTE]
>
>請務必了解 _事件_ 關鍵字，與「Google用戶端資料層」類似。 此 _事件_ 關鍵字會變更Google資料層的行為，因此也會變更此擴充功能。\
> 如果您不確定此點，請閱讀Google檔案或進行研究。

### 監聽所有推送至資料層

如果選擇此選項，則事件偵聽器將監聽對資料層所做的任何更改。

### 接聽推播排除事件

如果您選取此選項，則事件接聽程式會監聽資料層的任何推送資料，排除事件。

偵聽器會追蹤下列推送事件範例：

```js
dataLayer.push({"data":"something"})
```

監聽程式不會追蹤下列推送事件範例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 監聽所有事件

如果您選取此選項，則事件接聽程式會監聽推送至資料層的任何事件。

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

在您指定事件的情況下，事件偵聽器將跟蹤與特定字串匹配的任何事件。

例如，設定 `myEvent` 使用此設定時，偵聽器只會追蹤下列推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

A(ECMAScript / JavaScript)規則運算式可用來比對事件名稱。

例如，設定&#39;myEvent\d&#39;將會追蹤 `myEvent` 帶數字(\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 動作

### 推送至資料層 {#push-to-data-layer}

擴充功能提供將JSON推送至資料層的兩個動作；手動建立要推送的JSON的自由文字欄位，以及在1.2.0版中的機碼值多欄位對話方塊。

#### 自由文字JSON

自由文字動作可讓您直接在JSON中使用資料元素。 在JSON編輯器中，應使用百分比標籤法來參考資料元素。 例如 `%dataElementName%`。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### 索引鍵值多欄位

較新的機碼值多欄位對話方塊是更方便使用的介面，可讓您不需手動撰寫JSON即可設定推播。

### Google DL重置為計算狀態

擴充功能提供您重設資料層的動作。 若用於處理Google資料層變更的規則中，則資料層會在觸發規則時重設為資料層的計算狀態。 如果動作用於不會處理Google資料層變更的規則中，動作會清空資料層。

## 資料元素

提供的資料元素可在執行由Google資料層變更（推送事件）觸發的規則或不相關的規則（例如「載入的程式庫」）時使用。 在前一種情況下，資料元素返回資料層改變時從計算狀態提取的值。 在後一種情況下，使用規則執行時的計算狀態。

切換開關可讓您選取資料元素是否應從整個計算狀態傳回值，或僅從事件資訊傳回值（若用於資料層變更所觸發的規則中）。

因此，資料元素可傳回：

- 空白欄位：資料層計算狀態。
- 帶索引鍵的欄位（例如上述範例中的page.previous_url）:事件物件或計算狀態中索引鍵的值。

## 其他資訊

擴充功能的資料元素和事件對話方塊包含詳細的使用資訊和範例。

其他一般資訊位於 [專案讀我檔案](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
