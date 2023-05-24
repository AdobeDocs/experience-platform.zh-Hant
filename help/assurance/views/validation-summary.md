---
title: 驗證編輯器視圖
description: 本指南詳細介紹了有關Adobe Experience Platform保障中驗證編輯器視圖的資訊。
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# 驗證編輯器視圖

通過驗證編輯器，您可以快速輕鬆地管理JavaScript函式，以驗證Adobe Experience Platform保障會話中的事件。 每個函式在保證會話中接收事件。 您可以編寫函式來驗證客戶端配置、事件條件、test和使用案例。

## 開始使用驗證編輯器

之後 [設定保證](../tutorials/implement-assurance.md)的 **[!UICONTROL 首頁]** 選擇 **[!UICONTROL 驗證編輯器]**。

![驗證編輯器螢幕抓圖](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 編寫驗證函式

此功能允許您為Adobe Experience Platform保障會話建立、編輯或刪除驗證功能。

1. 選擇 **[!UICONTROL 建立新驗證]**。
2. 輸入 **名稱** 以標識驗證，然後提供 **類別** 和 **描述**。
3. 在編輯器中編輯代碼，以驗證您的保證會話的事件。

函式test完成後，選擇 **[!UICONTROL 發佈]** 保存驗證。

### 事件定義

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 事件的通用唯一標識符。 |
| `timestamp` | 數字 | 將事件發送到保證時客戶端的時間戳。 |
| `eventNumber` | 數字 | 用於發送事件時訂購。 當事件具有相同的時間戳時，此鍵非常有用。 |
| `vendor` | 字串 | 反向域名格式（例如com.adobe.assurance）的供應商標識字串。 |
| `type` | 字串 | 用於表示事件類型。 |
| `payload` | 物件 | 定義事件的資料，並包含唯一和公用屬性。 某些常見屬性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`。 |
| `annotations` | 陣列 | 注釋對象的陣列。 |

### 注釋定義

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 注釋的通用唯一標識符。 |
| `type` | 字串 | 用於表示批注的類型，通常是插件的名稱（例如，分析）。 |
| `payload` | 物件 | 定義應補充事件的資料。 對Adobe Analytics來說，這裡是後處理的命中資料。 |

### 驗證結果

驗證函式應返回包含以下內容的對象：

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `message` | 字串 | 要在摘要結果中顯示的驗證消息。 |
| `events` | 陣列 | 要報告為已匹配或未匹配的事件uid的陣列。 |
| `links` | 陣列 | 一組 `ValidationResultLink` 對象引用文檔和其他資源 `{( type: 'doc'|'product', url: String )}` |
| `result` | 字串 | 這是驗證結果，應為枚舉字串之一：&quot;matched&quot;、&quot;not matched&quot;、&quot;unknown&quot; |

## 查看驗證結果

函式的結果顯示在代碼編輯器下面的結果部分。 如果驗證結果為 `unknown` 或 `not matched` 和 `events` 陣列具有一個或多個 `uuids`，事件將在時間軸中以下列顏色加亮：

* 綠色 — 匹配
* 橙色 — 未知
* 紅色 — 不匹配

![計時 — 驗證 — 突出顯示 — 螢幕抓圖](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 疑難排解

可以添加 `console.log()` 函式將項目打印到開發人員控制台。 或者，可以使用結果對象的message屬性將消息調試到結果面板。

如果JavaScript代碼編輯器中出現錯誤，則將顯示錯誤狀態以及原因。

要瞭解有關驗證的詳細資訊，請訪問 [Adobe Experience Platform保證驗證](https://github.com/adobe/griffon-validation-plugins) GitHub。 您將在此處找到由Adobe擁有的驗證示例。 查看 [維基](https://github.com/adobe/griffon-validation-plugins/wiki) 以獲取驗證的詳細說明。
