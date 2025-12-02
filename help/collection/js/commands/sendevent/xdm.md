---
title: xdm
description: 瞭解如何透過XDM結構描述對齊的物件將資料傳送至Adobe。
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

`xdm`物件包含傳送至Adobe的資料裝載。 在此物件中設定的欄位會直接對應到資料集結構描述中定義的元素。

Adobe Experience Platform使用結構描述，以一致且可重複使用的方式說明資料結構。 藉由定義跨系統的一致資料，將可輕鬆保留意義，進而從資料中獲得價值。

執行`xdm`命令時設定`sendEvent`物件。 確定此物件中的階層符合已設定資料集的結構描述。 您可以在相同的`xdm`命令中同時包含[`data`](data.md)物件和`sendEvent`物件。

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

## 使用Web SDK標籤延伸功能來使用`xdm`物件

使用Web SDK標籤擴充功能時，`xdm`物件可作為[變數資料元素](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)或[XDM物件資料元素](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)使用。 Adobe建議在大部分情況下使用變數資料元素。
