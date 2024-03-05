---
title: 資料
description: 瞭解如何將非XDM資料傳送至Adobe。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 資料

此 `data` 屬性可讓您將資料傳送至不符合XDM結構描述的Adobe。 它在非XDM情況下很有用，例如更新 [Adobe Target設定檔](/help/web-sdk/personalization/adobe-target/target-overview.md). 當資料到達Adobe時，您可以使用資料流對應工具將XDM欄位指派給中的每個欄位 `data` 屬性。

>[!IMPORTANT]
>
>此屬性中的資料必須至少有下列其中一個動作：
>
>* 資料串流中的服務必須設定為從中的特定屬性擷取資料 `data` 物件
>* 每個屬性都必須對應至XDM欄位
>
>如果指定的欄位未對應到XDM欄位或供設定的服務使用，該資料會永久遺失。

## 使用Web SDK標籤擴充功能來使用資料屬性

在中提供資料元素 **[!UICONTROL 資料]** 標籤規則動作中的欄位。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 提供包含中所需物件的資料元素 **[!UICONTROL 資料]** 欄位。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫的data屬性

設定 `data` 屬性，屬於引數的JSON物件 `sendEvent` 命令。 對於您打算在資料串流中對應的資料，您可以視需要建構此屬性。 針對特定服務使用的資料，請確定物件階層符合服務的預期。 您可以同時包含 `data` 物件與 [`xdm`](xdm.md) 相同中的物件 `sendEvent` 命令。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
