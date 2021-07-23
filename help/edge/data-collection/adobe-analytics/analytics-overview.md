---
title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics。
keywords: adobe analytics;analytics；對應資料；對應的var;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---

# 傳送資料至Adobe Analytics

Adobe Experience Platform [!DNL Web SDK]可將資料傳送至Adobe Analytics。 將`xdm`轉譯為Adobe Analytics可使用的格式即可。

## 設定

如果客戶設定UI中已對應報表套裝，Adobe Analytics會自動擷取您傳送的資料。 您可以在此將一或多個報表對應至指定的設定。 報表套裝對應後，資料會自動開始流動。

## 自動映射的資料

Adobe Experience Platform [!DNL Edge Network]會自動對應許多XDM變數。 這些變數的完整清單列於[此處](automatically-mapped-vars.md)。

## 手動對應資料

邊緣網路收集的所有資料都可透過處理規則來存取。資料會使用點標籤法扁平化，並可作為contextData使用。

如果你有這樣的架構。

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

然後這些就是可供您使用的內容資料索引鍵。

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

以下是會使用此資料的處理規則的範例。

![處理規則介面](./assets/edge_analytics_processing_rules.png)
