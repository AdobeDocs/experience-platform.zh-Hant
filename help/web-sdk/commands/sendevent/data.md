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

`data`物件可讓您傳送裝載至不符合XDM結構描述的Adobe。 它在非XDM情況下相當實用，例如直接將資料傳送至Adobe Analytics、Adobe Target或Adobe Audience Manager。 當資料到達資料流時，您可以使用[資料準備對應](/help/data-prep/ui/mapping.md)將XDM欄位指派給`data`物件中的每個欄位。

>[!IMPORTANT]
>
>此物件中的資料必須至少有下列其中一個動作：
>
>* 資料串流中的服務必須設定為從`data`物件中的指定屬性擷取資料。
>* 指定的屬性必須使用「資料準備」對應至XDM欄位。
>
>如果指定的屬性未對應至XDM欄位，或供設定的服務使用，該資料將會永久遺失。

## 透過Web SDK標籤延伸使用`data`物件 {#tag-extension}

在標籤規則動作內的&#x200B;**[!UICONTROL 資料]**&#x200B;欄位中提供資料元素。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 在&#x200B;**[!UICONTROL 資料]**&#x200B;欄位中提供包含所需物件的資料元素。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 透過Web SDK JavaScript程式庫使用`data`物件 {#library}

在`sendEvent`命令的引數內，將`data`物件設定為JSON物件的一部分。 對於您打算在資料串流中對應的資料，您可以視需要建構此物件。 針對特定服務使用的資料，請確定物件階層符合服務的預期。 您可以在相同的`sendEvent`命令中同時包含`data`物件和[`xdm`](xdm.md)物件。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 搭配Adobe Analytics使用`data`物件 {#analytics}

您可以搭配Adobe Analytics使用`data`物件，將資料傳送至沒有XDM結構描述的報表套裝。 變數已設定為使用與[!DNL AppMeasurement]變數相同的語法，以簡化Web SDK的升級程式。 如需詳細資訊，請參閱Adobe Analytics實作指南中的[資料物件變數對應至Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping)。
