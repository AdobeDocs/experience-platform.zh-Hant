---
title: Google資料層擴展
description: 瞭解Google客戶端資料層標籤擴展在Adobe Experience Platform。
source-git-commit: 638b4fea8a80763a2b46863ecb0e3969a6fc127a
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# Google資料層擴展(Beta)

>[!IMPORTANT]
>
>此擴展目前處於測試版，尚未在生產中完全測試。

Google資料層擴展允許您在標籤實現中使用Google資料層。 該擴展可以單獨或同時與Google解決方案和Google的開放源使用 [資料層幫助程式庫](https://github.com/google/data-layer-helper)。

幫助程式庫提供與Adobe客戶端資料日期器(ACDL)類似的事件驅動功能。 Google資料層擴展的資料元素、規則和操作提供了與 [ACDL擴展](../client-data-layer/overview.md)。

## 到期

擴展的1.0.x版是Beta版。 此擴展尚未在生產中完全測試。

## 安裝

要安裝擴展，請導航到資料收集UI中的擴展目錄並選擇 **Google資料層**。

安裝後，每次標籤庫載入到您的網站上時，擴展會建立或訪問資料層。

## 擴展視圖

配置擴展時(安裝擴展時或選擇 **[!UICONTROL 配置]** 從擴展目錄)必須定義擴展所使用的資料層的名稱。 如果載入庫時不存在具有已配置名稱的資料層，則擴展將建立一個。

>[!NOTE]
>
>無論是Google還是Adobe代碼首先載入並建立資料層都無關緊要。 兩個系統都將建立資料層（如果不存在），或使用現有資料層。

預設情況下，資料層使用Google預設名稱 `dataLayer`。

## 活動

擴展允許您監聽資料層中的更改（事件）。 事件可以是下列任一項：

* 標籤事件（如正在載入的庫）
* JavaScript事件
* 將資料推送到資料層， `event` 的雙曲餘切值。

瞭解使用 [`event` 關鍵字](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) 將資料推送到Google資料層時，與Adobe客戶端資料層類似。 的 `event` 關鍵字更改Google資料層的行為，因此擴展的行為會相應更新。

以下各節概述了擴展可以偵聽的不同事件類型。

### 偵聽所有推送到資料層的內容

如果選擇此選項，擴展將監聽對資料層所做的任何更改。

### 收聽推送排除事件

如果選擇此選項，擴展將偵聽任何被推入到資料層的內容，但不包括事件。

監聽程式將跟蹤以下推式事件示例：

```js
dataLayer.push({"data":"something"})
```

監聽程式將不跟蹤以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 偵聽所有事件

如果選擇此選項，擴展將偵聽任何推送到資料層的事件。

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

如果要偵聽特定事件，請選擇此選項，以便事件偵聽器跟蹤與特定字串匹配的所有事件。

例如，設定 `myEvent` 使用此配置時，偵聽器將只跟蹤以下推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

也可以使用規則運算式字串來匹配事件名稱。 例如，設定 `myEvent\d` 將跟蹤以 `myEvent` 後跟數字：

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 動作

以下各節概述了擴展在包含在 [規則](../../../ui/managing-resources/rules.md)。

### 推送到資料層 {#push-to-data-layer}

此操作將JSON內容推送到資料層本身，使直接在JSON負載中使用資料元素成為可能。 在提供的JSON編輯器中，可以使用百分比表示法引用資料元素(例如， `%dataElementName%`)。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### GoogleDL重置為計算狀態

>[!NOTE]
>
>此操作從v1.0.5開始可用。

此操作將重置資料層。 如果在處理Google資料層更改的規則中使用，則資料層被重置為觸發規則時資料層的計算狀態。 如果在不處理Google資料層更改的規則中使用該操作，則該操作會清空資料層。

## 資料元素

該擴展提供了使用密鑰訪問資料層的唯一資料元素(例如， `page.url` 的 [上面的代碼段](#push-to-data-layer))。

資料元素可以提供以下任一內容：

* 資料層的特定值(例如， `page.url`)
* 整個資料層陣列（空鍵欄位）
* 使用鍵(如果 `event` 已使用關鍵字)
* 整個事件對象（空鍵欄位）

擴展始終優先於事件資訊。 如果資料層 `event` 正在處理，始終從該事件讀取值。 如果 `event` 不存在，則從直接資料層讀取值。

## 其他資訊

有關其他資訊，請參閱 [項目自述檔案](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) 以及擴展的資料元素和事件對話框。
