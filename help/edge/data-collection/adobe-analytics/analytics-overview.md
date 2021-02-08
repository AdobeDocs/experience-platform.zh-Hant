---
title: 傳送資料至Adobe Analytics
seo-title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics
description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Analytics
seo-description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Analytics
keywords: adobe analytics;analytics；映射資料；映射變數；
translation-type: tm+mt
source-git-commit: 723711ee0c2b7b5ca4aea617a81241dbebbc839c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---


# 傳送資料至Adobe Analytics

Adobe Experience Platform [!DNL Web SDK]可傳送資料至Adobe Analytics。 這可將`xdm`轉譯為Adobe Analytics可使用的格式。

## 設定

如果您在「客戶設定」使用者介面中對應了報表套裝，Adobe Analytics會自動擷取您要傳送的資料。 您可以在這裡將一或多個報表對應至指定的設定。 報表套裝映射後，資料會自動開始流動。

## 自動映射的資料

Adobe Experience Platform [!DNL Edge Network]會自動映射許多XDM變數。 這些變數的完整清單列於[這裡](automatically-mapped-vars.md)。

## 手動映射的資料

邊緣網路收集的所有資料都可透過處理規則來存取。資料會使用點記號平面化，並可用作contextData。

如果你有這樣的架構的話。

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

然後，這些將是可供您使用的上下文資料索引鍵。

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

以下是會使用此資料的處理規則範例。

![處理規則介面](../../../assets/edge_analytics_processing_rules.png)
