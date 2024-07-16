---
title: xdm
description: 瞭解如何透過XDM結構描述對齊的物件傳送資料給Adobe。
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

`xdm`物件包含傳送給Adobe的資料裝載。 在此物件中設定的欄位會直接對應到資料集結構描述中定義的元素。

Adobe Experience Platform使用結構描述，以一致且可重複使用的方式說明資料結構。 藉由定義跨系統的一致資料，將可輕鬆保留意義，進而從資料中獲得價值。

此物件的最大限製為32 KB。

## 使用Web SDK擴充功能設定XDM物件

在標籤規則的動作中設定&#x200B;**[!UICONTROL XDM]**&#x200B;物件。 [XDM物件](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)提供直覺式介面，可將其他資料元素對應至其各自的XDM欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 在&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中提供包含所需物件的資料元素。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫設定XDM物件

執行`sendEvent`命令時設定`xdm`物件。 確定此物件中的階層符合已設定資料集的結構描述。 您可以在相同的`sendEvent`命令中同時包含`xdm`物件和[`data`](data.md)物件。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

下列範例使用[Commerce詳細資料結構描述欄位群組](/help/xdm/field-groups/event/commerce-details.md)：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```
