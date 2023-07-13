---
title: 驗證編輯器檢視
description: 本指南會詳細介紹 Adob​​e Experience Platform Assurance 中驗證編輯器檢視的資訊。
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '527'
ht-degree: 100%

---

# 驗證編輯器檢視

驗證編輯器可讓您快速又輕鬆地管理 JavaScript 函數，以驗證 Ad&#x200B;&#x200B;ob&#x200B;&#x200B;e Experience Platform Assurance 工作階段中的事件。在 Assurance 工作階段中，每個函數都會收到事件。您可以編寫函數來驗證用戶端設定、事件條件、測試和使用案例。

## 開始使用驗證編輯器

[設定 Assurance](../tutorials/implement-assurance.md) (在「**[!UICONTROL 首頁]**」檢視中) 後，選取「**[!UICONTROL 驗證編輯器]**」。

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 編寫驗證函數

此功能可讓您為 Adob&#x200B;&#x200B;e Experience Platform Assurance 工作階段建立、編輯或刪除驗證函數。

1. 選取「**[!UICONTROL 建立新的驗證]**」。
2. 輸入&#x200B;**名稱**&#x200B;以識別驗證，然後提供&#x200B;**類別**&#x200B;和&#x200B;**說明**。
3. 在編輯器中編輯程式碼，以驗證 Assurance 工作階段的事件。

函數測試完成後，請選取「**[!UICONTROL 發佈]**」，即可儲存您的驗證。

### 事件定義

| 索引鍵 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 事件的通用唯一識別碼。 |
| `timestamp` | 數字 | 將事件傳送至 Assurance 時用戶端的時間戳記。 |
| `eventNumber` | 數字 | 用於傳送事件時的順序。事件具有相同的時間戳記時，可使用此索引鍵。 |
| `vendor` | 字串 | 反向網域名稱格式的廠商識別碼字串 (例如 com.adobe.assurance)。 |
| `type` | 字串 | 用於標示事件的類型。 |
| `payload` | 物件 | 定義事件的資料並包含唯一和常用屬性。部分常見的屬性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`。 |
| `annotations` | 陣列 | 註解物件的陣列。 |

### 註解定義

| 索引鍵 | 類型 | 說明 |
| :--- | :--- | :--- |
| `uuid` | 字串 | 註解的通用唯一識別碼。 |
| `type` | 字串 | 用於標示註解的類型，並且經常是外掛程式的名稱 (例如，analytics)。 |
| `payload` | 物件 | 定義應補充事件的資料。若為 Adob&#x200B;&#x200B;e Analytics，這指包含後續處理的點擊資料的位置。 |

### 驗證結果

驗證函數應該會傳回包含以下內容的物件：

| 索引鍵 | 類型 | 說明 |
| :--- | :--- | :--- |
| `message` | 字串 | 要在摘要結果中顯示的驗證訊息。 |
| `events` | 陣列 | 要報告為相符或不相符的事件 uuid 陣列。 |
| `links` | 陣列 | `ValidationResultLink`參照文件和其他資源之物件`{( type: 'doc'|'product', url: String )}`陣列 |
| `result` | 字串 | 這是驗證結果，並且應該是以下列舉字串之一：&quot;matched&quot;、&quot;not matched&quot;、&quot;unknown&quot; |

## 檢視驗證結果

該函數的結果會顯示在程式碼編輯器下方的結果區段中。如果驗證結果為 `unknown` 或 `not matched`，而且 `events` 陣列有一個或多個 `uuids`，則事件會在時間表中以下列顏色醒目提示：

* 綠色 - matched
* 橘色 - unknown
* 紅色 - not matched

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 疑難排解

你可以在函數中新增 `console.log()`，以將項目列印至開發人員主控台。或者，您可以使用結果物件的訊息屬性將偵錯訊息傳送至結果面板。

如果 JavaScript 程式碼編輯器中發生錯誤，則會顯示錯誤狀態以及原因。

若要了解有關驗證的詳細資訊，請造訪 [Adobe Experience Platform Assurance 驗證](https://github.com/adobe/griffon-validation-plugins) GitHub。您可在那裡找到 Adob&#x200B;&#x200B;e 所擁有的驗證範例。如需更多驗證的詳細說明，請參閱[維基百科](https://github.com/adobe/griffon-validation-plugins/wiki)。
