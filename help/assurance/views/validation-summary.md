---
title: 驗證編輯器視圖
description: 本指南詳細說明Adobe Experience Platform Assurance中驗證編輯器檢視的相關資訊。
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# 驗證編輯器視圖

驗證編輯器可讓您快速輕鬆地管理JavaScript函式，以驗證Adobe Experience Platform保證工作階段中的事件。 每個函式都會接收保證工作階段中的事件。 您可以編寫函式來驗證客戶端配置、事件條件、測試和使用案例。

## 開始使用驗證編輯器

之後 [設定保證](../tutorials/implement-assurance.md)，在 **[!UICONTROL 首頁]** 檢視，選取 **[!UICONTROL 驗證編輯器]**.

![驗證 — 編輯器 — 螢幕擷取畫面](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 編寫驗證函式

此功能可讓您建立、編輯或刪除Adobe Experience Platform Assurance工作階段的驗證功能。

1. 選擇 **[!UICONTROL 建立新驗證]**.
2. 輸入 **名稱** 若要識別驗證，請提供 **類別** 和 **說明**.
3. 在編輯器中編輯程式碼，驗證您的保證工作階段的事件。

完成函式測試後，請選取 **[!UICONTROL 發佈]** 以儲存驗證。

### 事件定義

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 事件的通用唯一識別碼。 |
| `timestamp` | 數字 | 將事件傳送至保證時來自用戶端的時間戳記。 |
| `eventNumber` | 數字 | 用於傳送事件時排序。 當事件的時間戳記相同時，此索引鍵就十分實用。 |
| `vendor` | 字串 | 反向域名格式的供應商標識字串（例如com.adobe.assurance）。 |
| `type` | 字串 | 用來表示事件的類型。 |
| `payload` | 物件 | 定義事件的資料，並包含唯一和通用的屬性。 某些常見屬性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`. |
| `annotations` | 陣列 | 注釋對象的陣列。 |

### 注釋定義

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 注釋的通用唯一標識符。 |
| `type` | 字串 | 用來表示注釋的類型，且通常是外掛程式的名稱（例如analytics）。 |
| `payload` | 物件 | 定義應補充事件的資料。 若為Adobe Analytics，此處會包含處理後點擊資料。 |

### 驗證結果

驗證函式應會傳回包含下列項目的物件：

| 代碼 | 類型 | 說明 |
| :--- | :--- | :--- |
| `message` | 字串 | 要在摘要結果中顯示的驗證訊息。 |
| `events` | 陣列 | 要報告為匹配或不匹配的事件uuid陣列。 |
| `links` | 陣列 | 陣列 `ValidationResultLink` 參考文檔和其他資源的對象 `{( type: 'doc'|'product', url: String )}` |
| `result` | 字串 | 這是驗證結果，應為列舉字串之一：&quot;matched&quot;、&quot;not matched&quot;、&quot;unknown&quot; |

## 查看驗證結果

函式的結果會顯示在程式碼編輯器下方的結果區段中。 如果驗證結果為 `unknown` 或 `not matched` 和 `events` 陣列具有一個或多個 `uuids`，時間軸中會以下列顏色強調顯示事件：

* 綠色 — 符合
* 橙色 — 未知
* 紅色 — 不匹配

![Timeling-Validation-Hights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 疑難排解

您可以新增 `console.log()` 在函式中，將項目列印至開發人員主控台。 或者，您也可以使用結果對象的消息屬性來調試到結果面板的消息。

如果JavaScript程式碼編輯器中發生錯誤，則會顯示錯誤狀態及原因。

若要進一步了解驗證，請造訪 [Adobe Experience Platform驗證](https://github.com/adobe/griffon-validation-plugins) GitHub。 此處提供Adobe擁有的驗證範例。 請參閱 [維基](https://github.com/adobe/griffon-validation-plugins/wiki) 有關驗證的詳細說明。
