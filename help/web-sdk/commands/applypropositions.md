---
title: applyPropositions
description: 重新呈現已使用sendEvent呈現的主張。
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 9aab41b338907f3c9fb15d08bfa877eb218f5627
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

`applyPropositions`命令可讓您重新呈現已使用[`sendEvent`](sendevent/overview.md)命令呈現的主張。 在使用單頁應用程式時，如果頁面部分重新呈現，可能會覆寫已套用至頁面的任何個人化，這個命令會很有用。

這個命令支援下列欄位：

* **主張**：您要重新呈現的主張物件陣列。
* **檢視名稱**：要呈現的檢視名稱。 已快取這些決定的顯示通知，並可使用`personalization.includePendingDisplayNotifications`選項包含在後續`sendEvent`命令中。
* **中繼資料**：決定如何套用HTML選件的物件。 它包含下列屬性：
   * 範圍
   * 選擇器
   * 動作型別

## 使用Web SDK標籤擴充功能套用主張

套用主張是在Adobe Experience Platform資料收集標籤介面的規則中作為動作執行的。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設定為&#x200B;**[!UICONTROL 套用主張]**。
1. 在右側設定所要的欄位。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫套用主張

呼叫Web SDK的已設定執行個體時執行`applyPropositions`命令。 包含組態選項的物件支援下列欄位：

* **`propositions`**：您要重新呈現的主張物件陣列。 一般不會使用此物件，因為`propositionScopes`欄位通常會決定您要重新呈現哪些範圍或介面。
* **`metadata`**：決定如何套用HTML選件。 這是一個對應，其中索引鍵是範圍或表面，而值是包含索引鍵`selector`和`actionType`的物件。
   * `selector`：字串，其中包含套用HTML位置的CSS選取器。
   * `actionType`：HTML要採取的動作。 有效值包括`setHtml`、`replaceHtml`和`appendHtml`。
* **`viewName`**：要在單頁應用程式中轉譯的檢視名稱。 已快取這些決定的顯示通知，並可使用`personalization.includePendingDisplayNotifications`納入後續`sendEvent`命令中。

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
