---
title: eventType
description: 設定sendEvent呼叫的事件型別。
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

`eventType`屬性可讓您定義使用Web SDK傳送的事件型別。 此欄位最終會填入`xdm.eventType`欄位。 當您想要區分您傳送至Adobe的事件型別時，這個選項很有價值。

Adobe提供一些預先定義的事件型別，供您使用。 如需預先定義值的完整清單，請參閱XDM使用手冊中[的`eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)可用值。 您也可以視偏好使用自己的值。

如果您在此設定`type`，並在`xdm.eventType`物件中設定[`xdm`](xdm.md)，則此欄位中的值優先。

執行`eventType`命令時設定`sendEvent`字串屬性。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## 使用網頁SDK標籤擴充功能的事件型別

這個屬性的Web SDK標籤延伸等效專案是設定&#39;[**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)&#39;動作時的[!UICONTROL Send event]下拉式功能表。
