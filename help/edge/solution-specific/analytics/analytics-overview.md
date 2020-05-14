---
title: 傳送資料至Adobe Analytics
seo-title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics
description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Analytics
seo-description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Analytics
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 傳送資料至Adobe Analytics

Adobe Experience Platform Web SDK可傳送資料至Adobe Analytics。 如此可轉譯 `xdm` 為Adobe Analytics可使用的格式。

## 設定

如果您在「客戶設定」使用者介面中對應了報表套裝，Adobe Analytics會自動擷取您要傳送的資料。 您可以在這裡將一或多個報表對應至指定的設定。 報表套裝映射後，資料會自動開始流動。

## 自動映射的資料

Adobe Experience Platform Edge Network會自動映射許多XDM變數。 此處列出自動映射變數的完整 [清單](../analytics/automatically-mapped-vars.md)。

## 手動映射的資料

邊緣網路收集的所有資料都可透過處理規則存取。 資料會使用點記號平面化，並可用作contextData。

如果你有這樣的架構的話。

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

然後，這些將是可供您使用的上下文資料索引鍵。

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

以下是會使用此資料的處理規則範例。

![處理規則介面](../../../assets/edge_analytics_processing_rules.png)
