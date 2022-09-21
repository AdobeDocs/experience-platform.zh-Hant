---
title: Adobe用戶端資料層擴充功能
description: 了解Adobe Experience Platform中的Adobe用戶端資料層標籤擴充功能。
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe用戶端資料層擴充功能

本檔案提供如何使用Adobe用戶端資料層擴充功能的範例和最佳實務。

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 安裝

若要安裝擴充功能，請導覽至Experience PlatformUI或資料收集UI中的擴充功能目錄，然後選取Adobe用戶端資料層。

![目錄中的ACDL擴充功能檢視](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 擴充功能檢視

依預設，ACDL指令碼會以變數名稱建立新的資料層 `adobeDataLayer`. 擴充功能檢視可讓您視需要變更此名稱。 載入標籤時，您設定的名稱會實例化。

>[!NOTE]
>
>更改對象名稱時，原始 `adobeDataLayer` 物件仍在實例化，然後複製到您選取的新變數名稱。

## 活動

擴充功能可讓您監聽資料層上的事件。 可使用下列事件：

### 監聽所有資料更改

如果選擇此選項，則事件偵聽器將監聽對資料層所做的任何更改。

>[!IMPORTANT]
>
>推送事件不會變更資料層本身。

偵聽器會追蹤下列推送事件範例：

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽程式不會追蹤下列推送事件範例：

* ` adobeDataLayer.push({"event":"myevent"})`

### 監聽所有事件

如果您選取此選項，則事件接聽程式會監聽推送至資料層的任何事件。

偵聽器會追蹤下列推送事件範例：

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽程式不會追蹤下列推送事件範例：

* ` adobeDataLayer.push({"data":"something"}) `

### 監聽特定事件

在您指定事件的情況下，事件偵聽器將跟蹤與特定字串匹配的任何事件。

例如，設定 `myEvent` 使用此設定時，偵聽器只會追蹤下列推送事件：

* `adobeDataLayer.push({"event":"myEvent"})`

您也可以變更事件接聽程式的範圍。 不同的選項概述如下：

* `all`:這是預設選項，且每當您先前選取的條件符合或將來推播時，就會觸發規則。 如果您使用非同步實作，這是最安全的選項。
* `future`:只有在將符合條件的新推送事件傳送至資料層時，此選項才會觸發規則。
* `past`:此選項只會針對符合您條件的舊推送事件觸發規則。 符合條件的新推送會遭忽略，不再觸發規則。

## 動作

以下各節將概述擴充功能支援的動作。

### 重設資料層

擴充功能可讓您重設資料層長度，有助於維持單頁應用程式(SPA)的有限大小。

不過，目前不可能完全移除推送方法期間先前設定的資訊。

此 **重置和設定計算狀態** 動作會複製最後一個計算狀態、清空資料層物件，然後重新推播最後一個狀態。

### 推送至資料層

擴充功能提供您推送JSON內容至資料層本身的動作。此動作可讓您直接在JSON中使用資料元素。 在JSON編輯器中，應使用百分比標籤法來參考資料元素(例如 `%dataElementName%`)。

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

以下各節涵蓋擴充功能提供的不重複資料元素類型。

### 計算狀態

資料層計算狀態資料元素可以根據您的設定方式，傳回兩個項目之一：

* 完整的資料層狀態：依預設，會傳回完整的資料層計算狀態。
* 特定路徑：您可以指定要在資料層中傳回的路徑。 路徑是使用點記號來指定(例如 `data.foo`)。

### 資料層大小

此資料元素會傳回資料層的大小。 資料層的大小由已推送至此物件的元素數量表示。

在下列推送事件清單中，此資料元素會傳回整數 `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
