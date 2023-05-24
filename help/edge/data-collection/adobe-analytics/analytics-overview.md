---
title: 將Adobe Analytics與平台Web SDK配合使用
description: 瞭解如何使用Adobe Experience PlatformWeb SDK向Adobe Analytics發送資料。
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 將Adobe Analytics與平台Web SDK配合使用

Adobe Experience Platform [!DNL Web SDK] 可以把資料發給Adobe Analytics。 通過翻譯 `xdm` 變成Adobe Analytics能用的格式。

## 設定

如果在客戶配置UI中映射了報告套件，Adobe Analytics會自動提取您發送的資料。 在此，您可以將一個或多個報告映射到給定的配置。 映射報表套件後，資料將自動開始流動。

## XDM欄位組

為了便於捕獲最常見的Adobe Analytics度量，我們提供了一個可供您使用的分析欄位組。 有關此架構的詳細資訊，請參閱 [Adobe AnalyticsExperienceEvent完整擴展架構欄位組](../../../xdm/field-groups/event/analytics-full-extension.md)

## 自動映射資料

Adobe Experience Platform [!DNL Edge Network] 自動映射許多XDM變數。 列出了這些變數的完整清單 [這裡](automatically-mapped-vars.md)。

## 手動映射的資料

未由 [!DNL Edge Network] 可通過處理規則訪問。 資料使用點表示法展平，並可作為contextData使用。

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

然後這些是上下文資料鍵。

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

下面是一個將使用此資料的處理規則的示例。

![處理規則介面](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>使用「體驗邊緣」集合，所有事件都會發送到分析以及您為資料流配置的任何其他服務。 例如，如果將Analytics和Target都配置為服務，並且您單獨呼叫個性化和Analytics ，則這兩個事件都將發送到Analytics和Target。 這些事件將記錄在分析報告中，並可能影響彈跳率等指標。
