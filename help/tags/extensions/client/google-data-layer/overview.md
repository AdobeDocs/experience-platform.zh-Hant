---
title: Google資料層擴展
description: 瞭解Google客戶端資料層標籤擴展在Adobe Experience Platform。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Google資料層擴展

Google資料層擴展允許您在標籤實現中使用Google資料層。 該擴展可以單獨或同時與Google解決方案和Google的開放源使用 [資料層幫助程式庫](https://github.com/google/data-layer-helper)。

幫助程式庫提供與Adobe客戶端資料日期器(ACDL)類似的事件驅動功能。 Google資料層擴展的資料元素、規則和操作提供了與 [ACDL擴展](../client-data-layer/overview.md)。

## 到期

版本1.2.x是生產使用中的較晚的Beta。

## 安裝

要安裝擴展，請導航到資料收集UI中的擴展目錄並選擇 **[!UICONTROL Google資料層]**。

安裝後，擴展將在Adobe Experience Platform標籤庫的每個負載上建立或訪問資料層。

## 擴展視圖

擴展配置可用於定義擴展所使用的資料層的名稱。 如果載入Adobe Experience Platform標籤時不存在具有配置名稱的資料層，則擴展將建立一個。

資料層名稱預設為Google預設名稱 `dataLayer`。

>[!NOTE]
>
>無論是Google還是Adobe代碼首先載入並建立資料層都無關緊要。 兩個系統的行為相同 — 如果資料層不存在或使用現有資料層，則建立資料層。

## 活動

>[!NOTE]
>
>詞 _事件_ 當事件驅動資料層在Adobe Experience Platform標籤中使用時會超載。 _事件_ 可以：
> - Adobe Experience Platform標籤事件（庫已載入等）。
> - JavaScript事件。
> - 將資料推送到資料層， _事件_ 的雙曲餘切值。


擴展功能使您能夠偵聽資料層上的更改。

>[!NOTE]
>
>瞭解使用 _事件_ 關鍵字將資料推送到Google資料層時，與Adobe客戶端資料層類似。 的 _事件_ 關鍵字更改Google資料層的行為，因此更改此擴展。\
> 請閱讀Google的檔案，如果您不確定這一點，請進行研究。

### 偵聽所有推送到資料層的內容

如果選擇此選項，事件偵聽器將監聽對資料層所做的任何更改。

### 收聽推送排除事件

如果選擇此選項，則事件偵聽器將監聽任何資料推送到資料層，但不包括事件。

監聽器將跟蹤以下推送事件示例：

```js
dataLayer.push({"data":"something"})
```

監聽程式將不跟蹤以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 偵聽所有事件

如果選擇此選項，則事件偵聽器將監聽任何推送到資料層的事件。

監聽器將跟蹤以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

監聽程式將不跟蹤以下示例推送事件：

```js
dataLayer.push({"data":"something"})
```

### 偵聽特定事件

在指定事件的情況下，事件偵聽器將跟蹤與特定字串匹配的所有事件。

例如，設定 `myEvent` 使用此配置時，偵聽器將只跟蹤以下推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

(ECMAScript / JavaScript)規則運算式可用於匹配事件名稱。

例如，設定「myEvent\d」將跟蹤 `myEvent` 帶數字(\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 動作

### 推送到資料層 {#push-to-data-layer}

該擴展提供了兩個將JSON推送到資料層的操作；用於手動建立要推送的JSON的自由文本欄位，以及從1.2.0版中的鍵值多欄位對話框。

#### 自由文本JSON

自由文本操作使直接在JSON中使用資料元素成為可能。 在JSON編輯器中，應使用百分比表示法引用資料元素。 例如 `%dataElementName%`。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### 鍵值多欄位

較新的key-value多欄位對話框是一個更方便用戶的介面，它允許配置推送，而無需手動寫入JSON。

### GoogleDL重置為計算狀態

該擴展為您提供了重置資料層的操作。 如果在處理Google資料層更改的規則中使用，則資料層被重置為觸發規則時資料層的計算狀態。 如果在不處理Google資料層更改的規則中使用該操作，則該操作會清空資料層。

## 資料元素

所提供的資料元素可在執行由Google資料層更改（推送事件）觸發的規則期間或在諸如庫載入的不相關規則中使用。 在前一種情況下，資料元素返回在資料層改變時從計算狀態獲取的值。 在後一種情況下，使用規則執行時的計算狀態。

切換開關允許您選擇資料元素應從整個計算狀態返回值還是僅從事件資訊返回值（如果用於由資料層更改觸發的規則）。

因此，資料元素可以返回：

- 空欄位：資料層計算狀態。
- 帶鍵的欄位（如上例中的page.previous_url）:事件對象或計算狀態中鍵的值。

## 其他資訊

擴展的資料元素和事件對話框包含詳細的使用資訊和示例。

其他一般資訊位於 [項目自述檔案](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
