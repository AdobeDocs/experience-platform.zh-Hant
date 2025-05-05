---
title: 使用Web SDK傳送資料至Adobe Analytics
description: 瞭解如何使用Adobe Experience Platform Web SDK傳送資料給Adobe Analytics。
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 使用Web SDK傳送資料給Adobe Analytics

Experience Platform Web SDK可透過Experience PlatformEdge Network傳送資料至Adobe Analytics。 Adobe提供數個選項，可讓您使用Web SDK將資料傳送至Adobe Analytics：

* 將[**[!UICONTROL Adobe Analytics ExperienceEvent欄位群組]**](../../xdm/field-groups/event/analytics-full-extension.md)新增到您的結構描述，然後使用[`XDM`物件](../commands/sendevent/xdm.md)。
* 使用[`data`物件](../commands/sendevent/data.md)傳送資料至Adobe Analytics而不使用XDM結構描述。
* 使用自動產生的[內容資料變數](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/page-vars/contextdata)和[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about)。

## 使用`XDM`物件 {#use-xdm-object}

如果您想要使用Adobe Analytics專屬的預先定義結構描述，您可以將[Adobe Analytics ExperienceEvent結構描述欄位群組](../../xdm/field-groups/event/analytics-full-extension.md)新增到您的結構描述。 新增後，您可以使用Web SDK中的`xdm`物件填入此結構描述，以傳送資料至報表套裝。 資料到達Edge Network時，會將XDM物件轉譯為Adobe Analytics可瞭解的格式。

您可透過下列兩種方式，透過Web SDK將資料傳送至Adobe Analytics：

* [使用Web SDK標籤延伸功能將資料傳送至Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [使用Web SDK JavaScript資料庫，將資料傳送至Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

請參閱Adobe Analytics實作指南中的[XDM物件變數對應至Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/xdm-var-mapping)，以取得XDM欄位的完整參考資料，以及它們如何對應至Analytics變數。

## 使用`data`物件 {#use-data-object}

除了使用XDM物件外，您也可以改用資料物件。 資料物件適合目前使用AppMeasurement的實施，可大幅簡化升級至Web SDK的程式。

根據您使用的是AppMeasurement或Analytics標籤擴充功能，請參閱下列指南以取得有關如何移轉至Web SDK的詳細資訊：

* [從Adobe Analytics標籤擴充功能移轉至Web SDK標籤擴充功能](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [從AppMeasurement移轉至Web SDK](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

如需資料物件欄位的完整參考資料，以及它們如何對應至Adobe Analytics變數，請參閱Adobe Analytics實作指南中有關[資料物件變數對應至Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/data-var-mapping)的檔案。

## 使用上下文資料變數 {#use-context-data-variables}

任何未自動對應的變數都可做為[內容資料變數](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/page-vars/contextdata)。 您接著可以使用[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about)，將內容資料變數對應至Analytics變數。 例如，如果您的自訂XDM結構描述如下所示：

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

然後，這些欄位將是「處理規則」介面中可供您使用的內容資料索引鍵：

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## 常見問題集

+++如何在Web SDK中區分頁面檢視呼叫和連結追蹤呼叫？

Adobe Analytics中的AppMeasurement針對頁面檢視（[`t()`方法](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/functions/t-method)）和連結追蹤呼叫（[`tl()`方法](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/functions/tl-method)）使用個別的方法呼叫。 Web SDK只提供用於傳送頁面檢視和連結追蹤的[`sendEvent`](../commands/sendevent/overview.md)命令。 您在事件中包含的資料會判斷它是Adobe Analytics中的[頁面檢視](https://experienceleague.adobe.com/zh-hant/docs/analytics/components/metrics/page-views)或[頁面事件](https://experienceleague.adobe.com/zh-hant/docs/analytics/components/metrics/page-events)。

依預設，所有事件在Adobe Analytics中都會被視為頁面檢視。 如果您想要將Web SDK事件設定為Adobe Analytics連結追蹤呼叫，請設定下列欄位：

* **XDM物件**： `xdm.web.webInteraction.name`、`web.webInteraction.type`和`web.webInteraction.URL`
* **資料物件**： `data.__adobe.analytics.linkName`、`data.__adobe.analytics.linkType`和`data.__adobe.analytics.linkURL`
* **內容資料**：不支援

如需詳細資訊，請參閱Adobe Analytics實作指南中的[`tl()`方法](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/vars/functions/tl-method)。

如果您在`configure`命令中啟用[`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md)，系統會為您填入這些欄位。

+++

+++資料串流如何透過專為Adobe Analytics提供的資料，將資料與其他服務區分開來？

傳送至資料流的所有事件都會傳遞至所有已設定的服務。 例如，如果您分別呼叫個人化和Analytics，這兩個事件都會傳送至Analytics和Target。 這些事件會記錄在Analytics報表中，並可能影響跳出率等量度。

如果您使用Web SDK，這些呼叫通常會合併到[`sendEvent`](../commands/sendevent/overview.md)命令中。

+++
