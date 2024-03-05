---
title: 使用Web SDK傳送資料至Adobe Analytics
description: 瞭解如何使用Adobe Experience Platform Web SDK傳送資料給Adobe Analytics。
keywords: adobe analytics；analytics；對應的資料；對應的變數；
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# 使用Web SDK傳送資料給Adobe Analytics

Adobe Experience Platform Web SDK可透過Adobe Experience Platform Edge Network傳送資料給Adobe Analytics。 資料到達Edge Network時，會將XDM物件轉譯為Adobe Analytics可瞭解的格式。

## xdm欄位群組

為了更方便擷取最常見的Adobe Analytics量度，Adobe提供您可使用的以Adobe Analytics為目標的欄位群組。 如需此結構的詳細資訊，請參閱 [Adobe Analytics ExperienceEvent完整擴充功能結構欄位群組](/help/xdm/field-groups/event/analytics-full-extension.md).

## 變數對應

邊緣網路會自動對應許多XDM變數。 另請參閱 [邊緣網路中的Analytics變數對應](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=zh-Hant) Adobe Analytics實作指南中的，以取得自動對應變數的完整變數清單。

任何未自動對應的變數都可在 [上下文資料變數](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html). 然後您可以使用 [處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) 將上下文資料變數對應至Analytics變數。 例如，如果您的自訂XDM結構描述如下所示：

```js
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

然後，這些會是處理規則介面中可供您使用的內容資料索引鍵：

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

>[!NOTE]
>
>透過Edge Network集合，所有事件都會傳送至Analytics以及您為資料流設定的任何其他服務。 例如，如果您將Analytics和Target都設定為服務，並為個人化和Analytics分別發出呼叫，則兩個事件都會傳送至Analytics和Target。 這些事件會記錄在Analytics報表中，並可能影響跳出率等量度。

## 頁面檢視和連結追蹤呼叫

Adobe Analytics中的AppMeasurement功能會針對頁面檢視使用個別方法呼叫([`t()` 方法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html))和連結追蹤呼叫([`tl()` 方法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html))。 Web SDK僅會提供 [`sendEvent`](../commands/sendevent/overview.md) 用於傳送頁面檢視和連結追蹤的命令。 您在事件中包含的資料會判斷它是否為 [頁面檢視](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html) 或 [頁面事件](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) 在Adobe Analytics中。

依預設，所有事件在Adobe Analytics中都會被視為頁面檢視。 如果您想要將Web SDK事件設定為Adobe Analytics連結追蹤呼叫，請設定下列XDM欄位：

* **`web.webInteraction.URL`**：連結URL。
* **`web.webInteraction.name`**：自訂連結、下載連結或退出連結維度名稱，視中的值而定 `web.webInteraction.type`
* **`web.webInteraction.type`**：判斷點按的連結型別。 有效值包括 `other` (自訂連結)、`download` (下載連結) 和 `exit` (退出連結)。

如果您啟用 [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) 在 `configure` 會為您填入這些XDM欄位。
