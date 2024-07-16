---
title: 核心事件轉送擴充功能概觀
description: 瞭解Adobe Experience Platform中的核心事件轉送擴充功能。
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: 2ba02f94ff20281953d74b3213033e5f0a7fa111
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 90%

---

# 核心事件轉送擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

核心事件轉送擴充功能提供Adobe Experience Platform中事件轉送的預設事件、條件和資料型別。

您可參閱此參考文件，了解使用此擴充功能建立規則時可使用哪些選項。

## 核心擴充功能條件類型

本節說明核心擴充功能中可用的條件類型。這些條件類型可與正常或例外邏輯類型一起使用。

### 自訂程式碼

指定必須存在作為事件條件的任何自訂程式碼。使用內建程式碼編輯器輸入自訂程式碼。Adobe Experience Platform中的事件轉送支援ES13。

1. 選取&#x200B;**[!UICONTROL 開啟編輯器]**。
1. 輸入自訂程式碼。
1. 選取「**[!UICONTROL 儲存]**」。

若要存取自訂程式碼中資料元素的值，請使用 `getDataElementValue` 方法。舉例來說，若要擷取資料元素 `productName` 的值，請編寫以下內容：

```javascript
getDataElementValue('productName') 
```

#### ruleStash 物件

您也可以在自訂程式碼中使用 `ruleStash` 物件。

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` 是收集動作模組各個結果的物件。

每個擴充功能都有專屬的命名空間。舉例來說，如果您的擴充功能名為 `send-beacon`，則 `send-beacon` 動作的所有結果都會儲存在 `ruleStash['send-beacon']` 命名空間。

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

每個擴充功能的命名空間都是獨一無二，其開頭的值為 `undefined`。

每個動作傳回的結果將會覆寫命名空間。命名空間沒有什麼神奇的魔法發生。舉例來說，如果您擁有 `transform` 擴充功能，請先加入 `generate-fullname` 和 `generate-fulladdress` 兩個動作，然後將兩個動作新增至規則。

如果 `generate-fullname` 動作的結果為 `Firstname Lastname`，動作完成後，規則隱藏項目會如下所示：

```js
{
  transform: 'Firstname Lastname`
}
```

如果 `generate-address` 動作的結果為 `3900 Adobe Way`，動作完成後，規則隱藏項目則會如下所示：

```js
{
  transform: '3900 Adobe Way`
}
```

請注意，規則隱藏項目中不再有 `Firstname Lastname`，這是因為 `generate-address` 動作會以地址來加以覆寫。

如果要將這兩個動作的結果儲存於 `ruleStash` 中的 `transform` 命名空間，可參考以下範例編寫動作模組：

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

第一次執行此動作時，`ruleStash` 為 `undefined`，系統會以空白物件來初始化。下次執行此動作時，動作會傳回先前呼叫時的 `ruleStash`。若將物件作為 `ruleStash` 使用，您就能新增資料，同時不會失去擴充功能中其他動作先前設定的資料。

必須注意的是，在這個情況下，您必須一律傳回完整擴充功能規則的隱藏項目。如果只傳回值 (例如 5)，規則隱藏項目會如下所示：

```js
{
  transform: 5
}
```

### 值比較 {#value-comparison}

比較兩個值以判斷此條件是否傳回 true。

如果規則具有多個條件，則可能因為其他條件評估為 false，或有一個例外評估為 true，造成此條件會傳回 true，但規則仍不會引發。

1. 提供一個值。
1. 選取運算子。請參閱下方的值比較運算子清單，以了解詳細資訊。
1. 提供另一個值作為比較對象。

可使用下列的值比較運算子：

**等於：**&#x200B;如果使用非嚴格比較，且兩值相等 (在 JavaScript 中為「==」運算子)，則條件會傳回 true。值可為任何類型。在值欄位中輸入 _true_、_false_、_null_ 或 _undefined_ 時，系統會將該字詞當成字串進行比較，且不會轉換為其 JavaScript 相等值。

**不等於：**&#x200B;如果使用非嚴格 (non-strict) 比較，且兩值不相等 (在 JavaScript 中為「! =」運算子)，則條件會傳回 true。值可為任何類型。在值欄位中輸入 _true_、_false_、_null_ 或 _undefined_ 時，系統會將該字詞當成字串進行比較，且不會轉換為其 JavaScript 相等值。

**包含：**&#x200B;如果第一個值包含第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 false。

**不包含：**&#x200B;如果第一個值不包含第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值都會導致條件傳回 true。

**開頭為：**&#x200B;如果第一個值開頭為第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 false。

**開頭非為：**&#x200B;如果第一個值的開頭不是第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 true。

**結尾為：**&#x200B;如果第一個值的結尾是第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 false。

**結尾非為：**&#x200B;如果第一個值的結尾不是第二個值，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 true。

**符合 Regex：**&#x200B;如果第一個值符合規則運算式，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 false。

**不符合 Regex：**&#x200B;如果第一個值不符合規則運算式，則條件會傳回 true。數字會轉換為字串。數字或字串以外的任何值會都導致條件傳回 true。

**小於：**&#x200B;如果第一個值小於第二個值，則條件會傳回 true。代表數字的字串會轉換為數字。數字或可轉換字串以外的任何值都會導致條件傳回 false。

**小於或等於：**&#x200B;如果第一個值小於或等於第二個值，則條件會傳回 true。代表數字的字串會轉換為數字。數字或可轉換字串以外的任何值都會導致條件傳回 false。

**大於：**&#x200B;如果第一個值大於第二個值，則條件會傳回 true。代表數字的字串會轉換為數字。數字或可轉換字串以外的任何值都會導致條件傳回 false。

**大於或等於：**&#x200B;如果第一個值大於或等於第二個值，則條件會傳回 true。代表數字的字串會轉換為數字。數字或可轉換字串以外的任何值都會導致條件傳回 false。

**為 True：**&#x200B;如果值是布林值且為 true，則條件會傳回 true。若提供的值是任何其他類型，則不會轉換為布林值。帶有 true 值的布林值以外的任何值都會導致條件傳回 false。

**為 Truthy：**&#x200B;如果值在轉換為布林值後為 true，條件會傳回 true。如需 Truthy 值的範例，請參閱 [MDN 的 Truthy 文件](https://developer.mozilla.org/zh-TW/docs/Glossary/Truthy)。

**為 False：**&#x200B;如果值是布林值且為 false，則條件會傳回 true。若提供的值是任何其他類型，則不會轉換為布林值。帶有 false 值的布林值以外的任何值都會導致條件傳回 false。

**為 Falsy：**&#x200B;如果值轉換為布林值後為 false，條件會傳回 true。如需 Falsy 值的範例，請參閱 [MDN 的 Falsy 文件](https://developer.mozilla.org/zh-TW/docs/Glossary/Falsy)。



## 核心擴充功能動作類型

本節說明核心擴充功能中可用的動作類型。

### 自訂程式碼

提供觸發事件和評估條件後執行的程式碼。Adobe Experience Platform中的事件轉送支援ES13。

1. 為動作程式碼命名。
1. 選取&#x200B;**[!UICONTROL 開啟編輯器]**。
1. 編輯程式碼，然後選取&#x200B;**[!UICONTROL 儲存]**。

若要存取自訂程式碼中資料元素的值，請使用 `getDataElementValue` 方法。舉例來說，若要擷取資料元素 `productName` 的值，請編寫以下內容：

```javascript
getDataElementValue('productName') 
```

事件轉送動作會依序執行。 自訂程式碼也可以在一個動作中傳回可用於後續動作的值。傳回的值可能來自該動作中的程式碼，或來自呼叫外部來源的回應內文。若要參照使用核心擴充功能之單一規則中先前執行動作的資料，請建立 `Path` 類型資料元素，並使用以下路徑來參照核心擴充功能中自訂程式碼定義之 `productCategory` 變數的值：

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## 核心擴充功能資料元素類型

資料元素類型由擴充功能決定。可建立的類型沒有限制。

以下各節會說明核心擴充功能中可用的資料元素類型。其他擴充功能則使用其他類型的資料元素。

### 自訂程式碼

選取&#x200B;**[!UICONTROL 開啟編輯器]**&#x200B;並將程式碼插入編輯器視窗，即可在UI中輸入自訂JavaScript。

編輯器視窗中需有傳回陳述式，以指明應作為資料元素值使用的值。如果未包含傳回陳述式，或系統傳回 `null` 或 `undefined` 值，則資料元素的預設值會反映 `null` 或 `undefined`。

若要存取自訂程式碼中資料元素的值，請使用 `getDataElementValue` 方法。舉例來說，若要擷取資料元素 `productName` 的值，請編寫以下內容：

```javascript
getDataElementValue('productName') 
```

**範例：**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### 路徑

如果是傳送至 Adobe Experience Platform Edge Network 的事件，可使用「路徑」資料元素類型來參照其索引鍵/值組路徑。

若要參照事件的整個物件，請輸入 `arc` 作為路徑。縮寫 `arc` 代表 Adobe Resource Context，這是傳送至 Adobe Experience Platform Edge Network 之事件的最上層路徑。

舉例來說，假設用戶端對 Edge Network 的 `interact` 呼叫中具有以下要求，瀏覽器主控台顯示的畫面如下：

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

若要輸入參照 `pageName` 的路徑，請在路徑欄位中輸入以下內容：

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>來自使用者端的`interact`呼叫有`events`，但若要進行事件轉送，您需要`event`。 這是因為事件轉送會個別檢查每個事件，而非如使用者端一樣，一次檢查多個事件。
