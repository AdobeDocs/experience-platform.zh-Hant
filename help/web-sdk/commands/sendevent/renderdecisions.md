---
title: renderDecisions
description: 呈現符合自動呈現資格的個人化內容。
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

`renderDecisions`屬性可讓您強制Web SDK轉譯任何符合自動轉譯條件的個人化內容。

## 使用Web SDK標籤擴充功能呈現個人化內容

選取標籤規則動作內的&#x200B;**[!UICONTROL 呈現視覺化個人化決定]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 向下捲動至[!UICONTROL Personalization]區段，然後選取&#x200B;**[!UICONTROL 呈現視覺個人化決策]**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫呈現個人化內容

執行`sendEvent`命令時設定`renderDecisions`布林值。 如果省略，此屬性會預設為`false`。 如果您要自動轉譯個人化內容，請將此屬性設定為`true`。

>[!IMPORTANT]
>
>`renderDecisions`屬性與[`documentUnloading`](documentunloading.md)屬性不相容。 您不應該同時設定兩個屬性為`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
