---
title: eventType
description: 設定sendEvent呼叫的事件型別。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

此 `eventType` 屬性可讓您定義使用Web SDK傳送的事件型別。 此欄位最終會填入 `xdm.eventType` 欄位。 當您想要區分傳送給Adobe的事件型別時，這個選項很有價值。

Adobe提供一些預先定義的事件型別，供您使用。 另請參閱 [可用的值 `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) XDM使用手冊中的完整預先定義值清單。 您也可以視偏好使用自己的值。

如果您同時設定 `type` 此處和 `xdm.eventType` 在 [`xdm`](xdm.md) 物件，此欄位中的值優先。

## 使用Web SDK標籤擴充功能設定事件型別

設定 **[!UICONTROL 型別]** 標籤規則動作中的下拉式欄位。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 使用下方的下拉式清單 **[!UICONTROL 型別]** 欄位，或輸入您自己的值。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫設定事件型別

設定 `eventType` 字串屬性 `sendEvent` 命令。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
