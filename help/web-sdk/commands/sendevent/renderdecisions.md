---
title: renderDecisions
description: 呈現符合自動呈現資格的個人化內容。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `renderDecisions`

此 `renderDecisions` 屬性可讓您強制Web SDK轉譯任何符合自動轉譯條件的個人化內容。

## 使用Web SDK標籤擴充功能呈現個人化內容

選取 **[!UICONTROL 呈現視覺個人化決定]** 標籤規則動作中的核取方塊。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 向下捲動至 [!UICONTROL 個人化] 區段，然後選取 **[!UICONTROL 呈現視覺個人化決定]** 核取方塊。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫轉譯個人化內容

設定 `renderDecisions` 執行時的布林值 `sendEvent` 命令。 如果省略，此屬性會預設為 `false`. 將此屬性設為 `true` 如果您想要自動呈現個人化內容。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
