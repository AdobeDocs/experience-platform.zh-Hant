---
title: applyPropositions
description: 重新呈現已使用sendEvent呈現的主張。
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# `applyPropositions`

`applyPropositions`命令可讓您重新呈現已使用[`sendEvent`](sendevent/overview.md)命令呈現的主張。 在使用單頁應用程式時，如果頁面部分重新呈現，可能會覆寫已套用至頁面的任何個人化，這個命令會很有用。

這個命令支援下列欄位：

* **主張**：您要重新呈現的主張物件陣列。
* **檢視名稱**：要呈現的檢視名稱。 已快取這些決定的顯示通知，並可使用`sendEvent`選項包含在後續`personalization.includeRenderedPropositions`命令中。
* **Meta資料**：決定如何套用HTML選件的物件。 它包含下列屬性：
   * 範圍
   * 選擇器
   * 動作型別

呼叫您設定的Web SDK執行個體時執行`applyPropositions`命令。 包含組態選項的物件支援下列欄位：

* **`propositions`**：您要重新呈現的主張物件陣列。 一般不會使用此物件，因為`propositionScopes`欄位通常會決定您要重新呈現哪些範圍或介面。
* **`metadata`**：決定HTML選件的套用方式。 這是一個對應，其中索引鍵是範圍或表面，而值是包含索引鍵`selector`和`actionType`的物件。
   * `selector`：字串，其中包含套用HTML位置的CSS選取器。
   * `actionType`：HTML要採取的動作。 有效值包括`setHtml`、`replaceHtml`和`appendHtml`。
* **`viewName`**：要在單頁應用程式中轉譯的檢視名稱。 已快取這些決定的顯示通知，並可使用`sendEvent`納入後續`personalization.includeRenderedPropositions`命令中。

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## 使用網頁SDK標籤擴充功能套用主張

等同於這個命令的網頁SDK標籤延伸是[**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)動作。
