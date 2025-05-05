---
title: eventType
description: 設定sendEvent呼叫的事件型別。
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

`eventType`屬性可讓您定義使用Web SDK傳送的事件型別。 此欄位最終會填入`xdm.eventType`欄位。 當您想要區分傳送給Adobe的事件型別時，這個選項很有價值。

Adobe提供一些預先定義的事件型別，供您使用。 如需預先定義值的完整清單，請參閱XDM使用手冊中`eventType`[&#128279;](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)的可用值。 您也可以視偏好使用自己的值。

如果您在此設定`type`，並在[`xdm`](xdm.md)物件中設定`xdm.eventType`，則此欄位中的值優先。

## 使用Web SDK標籤擴充功能設定事件型別

設定標籤規則動作內的&#x200B;**[!UICONTROL Type]**&#x200B;下拉式欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 使用&#x200B;**[!UICONTROL 型別]**&#x200B;欄位下的下拉式清單，或輸入您自己的值。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫設定事件型別

執行`sendEvent`命令時設定`eventType`字串屬性。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
