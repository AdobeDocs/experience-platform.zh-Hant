---
title: 資料
description: 瞭解如何透過資料物件將非XDM資料傳送至Adobe。
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

此 `data` 物件可讓您將裝載傳送至不符合XDM結構描述的Adobe。 它在非XDM情況下相當實用，例如直接將資料傳送至Adobe Analytics、Adobe Target或Adobe Audience Manager。 當資料到達資料流時，您可以使用 [資料準備對應](/help/data-prep/ui/mapping.md) 將XDM欄位指派給 `data` 物件。

>[!IMPORTANT]
>
>此物件中的資料必須至少有下列其中一個動作：
>
>* 資料串流中的服務必須設定為從中的指定屬性擷取資料 `data` 物件。
>* 指定的屬性必須使用「資料準備」對應至XDM欄位。
>
>如果指定的屬性未對應至XDM欄位，或供設定的服務使用，該資料將會永久遺失。

## 使用 `data` 物件（透過Web SDK標籤擴充功能） {#tag-extension}

在中提供資料元素 **[!UICONTROL 資料]** 標籤規則動作中的欄位。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 提供包含中所需物件的資料元素 **[!UICONTROL 資料]** 欄位。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用 `data` 物件（透過Web SDK JavaScript資料庫） {#library}

設定 `data` 物件，作為引數內JSON物件的一部分 `sendEvent` 命令。 對於您打算在資料串流中對應的資料，您可以視需要建構此物件。 針對特定服務使用的資料，請確定物件階層符合服務的預期。 您可以同時包含 `data` 物件與 [`xdm`](xdm.md) 相同中的物件 `sendEvent` 命令。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 使用 `data` 使用Adobe Analytics的物件 {#analytics}

您可以使用 `data` Adobe Analytics物件，可傳送資料至沒有XDM結構描述的報表套裝。 變數的設定語法與相同 [!DNL AppMeasurement] 變數，簡化Web SDK的升級程式。 另請參閱 [資料物件變數對應至Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/data-var-mapping) Adobe Analytics實作指南以瞭解詳細資訊。
