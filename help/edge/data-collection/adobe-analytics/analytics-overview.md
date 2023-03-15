---
title: 搭配使用Adobe Analytics與Platform Web SDK
description: 了解如何使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics。
keywords: adobe analytics;analytics；對應資料；對應的var;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 搭配使用Adobe Analytics與Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] 可將資料傳送至Adobe Analytics。 這通過翻譯 `xdm` 轉換為Adobe Analytics可使用的格式。

## 設定

如果客戶設定UI中已對應報表套裝，Adobe Analytics會自動擷取您傳送的資料。 您可以在此將一或多個報表對應至指定的設定。 報表套裝對應後，資料會自動開始流動。

## XDM欄位群組

為了更方便擷取最常見的Adobe Analytics量度，我們提供您可使用的Analytics欄位群組。 如需此結構的詳細資訊，請參閱 [Adobe Analytics ExperienceEvent完整擴充功能結構欄位群組](../../../xdm/field-groups/event/analytics-full-extension.md)

## 自動映射的資料

Adobe Experience Platform [!DNL Edge Network] 自動對應許多XDM變數。 會列出這些變數的完整清單 [此處](automatically-mapped-vars.md).

## 手動對應資料

未由 [!DNL Edge Network] 可透過處理規則來存取。 資料會使用點標籤法扁平化，並可作為contextData使用。

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

>[!NOTE]
>
>透過Experience Edge集合，所有事件都會傳送至Analytics，以及您為資料流設定的任何其他服務。 例如，如果您同時將Analytics和Target設定為服務，並且您分別呼叫個人化和Analytics，則兩個事件都會傳送至Analytics和Target。 這些事件將記錄在Analytics報表中，且可能影響跳出率之類的量度。
