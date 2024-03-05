---
title: applyPropositions
description: 重新呈現已使用sendEvent呈現的主張。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

此 `applyPropositions` 命令可讓您重新呈現已使用 [`sendEvent`](sendevent/overview.md) 命令。 在使用單頁應用程式時，如果頁面部分重新呈現，可能會覆寫已套用至頁面的任何個人化，這個命令會很有用。

這個命令支援下列欄位：

* **主張**：您要重新呈現的主張物件陣列。
* **檢視名稱**：要呈現的檢視名稱。 這些決定的顯示通知會被快取，並可包含在後續中 `sendEvent` 命令使用 `personalization.includePendingDisplayNotifications` 選項。
* **中繼資料**：決定如何套用HTML選件的物件。 它包含下列屬性：
   * 範圍
   * 選擇器
   * 動作型別

## 使用Web SDK標籤擴充功能套用主張

套用主張是在Adobe Experience Platform資料收集標籤介面的規則中作為動作執行的。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 套用主張]**.
1. 在右側設定所要的欄位。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫套用主張

執行 `applyPropositions` 命令來呼叫Web SDK的已設定執行個體。 包含組態選項的物件支援下列欄位：

* **`propositions`**：您要重新呈現的主張物件陣列。 此物件通常不會使用，因為 `propositionScopes` 欄位通常會決定您要重新呈現哪些範圍或表面。
* **`metadata`**：決定HTML選件的套用方式。 這是一個對映，其中鍵是範圍或曲面，而值是包含鍵的物件 `selector` 和 `actionType`.
   * `selector`：字串，其中包含套用HTML位置的CSS選取器。
   * `actionType`：HTML要採取的動作。 有效值包括 `setHtml`、`replaceHtml` 和 `appendHtml`。
* **`viewName`**：要在單頁應用程式中轉譯的檢視名稱。 這些決定的顯示通知會被快取，並可包含在後續中 `sendEvent` 命令使用 `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
