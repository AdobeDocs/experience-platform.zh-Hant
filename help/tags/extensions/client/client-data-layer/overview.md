---
title: Adobe客戶端資料層擴展
description: 瞭解Adobe Experience Platform的Adobe客戶端資料層標籤擴展。
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe客戶端資料層擴展

本文檔提供了有關如何使用Adobe客戶端資料層擴展的示例和最佳做法。

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 安裝

要安裝擴展，請導航到Experience PlatformUI或資料收集UI中的擴展目錄，然後選擇Adobe客戶端資料層。

![目錄中的ACDL擴展視圖](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 擴展視圖

預設情況下，ACDL指令碼會使用變數名稱建立新資料層 `adobeDataLayer`。 如果您願意，擴展視圖可以更改此名稱。 載入標籤時，將實例化您設定的名稱。

>[!NOTE]
>
>更改對象名稱時，原始 `adobeDataLayer` 對象仍在實例化中，然後複製到您選擇的新變數名稱。

## 活動

擴展功能使您能夠偵聽資料層上的事件。 以下事件可用：

### 偵聽所有資料更改

如果選擇此選項，事件偵聽器將監聽對資料層所做的任何更改。

>[!IMPORTANT]
>
>推送事件不會更改資料層本身。

監聽器將跟蹤以下推送事件示例：

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽程式將不跟蹤以下示例推送事件：

* ` adobeDataLayer.push({"event":"myevent"})`

### 收聽所有事件

如果選擇此選項，則事件偵聽器將監聽任何推送到資料層的事件。

監聽器將跟蹤以下推送事件示例：

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽程式將不跟蹤以下示例推送事件：

* ` adobeDataLayer.push({"data":"something"}) `

### 收聽特定事件

在指定事件的情況下，事件偵聽器將跟蹤與特定字串匹配的所有事件。

例如，設定 `myEvent` 使用此配置時，偵聽器將只跟蹤以下推送事件：

* `adobeDataLayer.push({"event":"myEvent"})`

您還可以更改事件偵聽器的範圍。 不同選項概述如下：

* `all`:這是預設選項，每次您在過去已滿足上述選定條件或將來要推送時，都會觸發規則。 如果您使用非同步實現，則這是最安全的選項。
* `future`:僅當將與條件匹配的新推送事件發送到資料層時，此選項才觸發規則。
* `past`:此選項僅針對與條件匹配的舊推送事件觸發規則。 將忽略與條件匹配的新推送，不再觸發規則。

## 動作

以下各節概述了擴展支援的操作。

### 重置資料層

該擴展為您提供了重置資料層長度的方法，這有助於保持單頁應用程式(SPA)的有限大小。

但是，目前不可能完全刪除在推送方法期間以前設定的資訊。

的 **重置和設定計算狀態** 操作複製上次計算的狀態，清空資料層對象，並重新推送最後的狀態。

### 推送到資料層

擴展功能提供了將JSON內容推送到資料層本身的操作。此操作使直接在JSON中使用資料元素成為可能。 在JSON編輯器中，應使用百分比表示法引用資料元素(例如， `%dataElementName%`)。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## 資料元素

以下各節涵蓋擴展提供的唯一資料元素類型。

### 計算狀態

資料層計算狀態資料元素可以返回以下兩種情況之一，具體取決於您如何配置它：

* 完整的資料層狀態：預設情況下，將返回完整的資料層計算狀態。
* 特定路徑：您可以指定要在資料層中返回的路徑。 路徑是使用點表示法指定的(例如， `data.foo`)。

### 資料層大小

此資料元素返回資料層的大小。 資料層的大小由已推送到此對象的元素數表示。

給定以下推送事件清單，此資料元素將返回整數 `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
