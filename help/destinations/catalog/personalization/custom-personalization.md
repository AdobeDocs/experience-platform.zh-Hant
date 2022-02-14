---
keywords: 自定義個性化；目的地；體驗平台定制目標；
title: 自定義個性化連接
description: 此目標提供外部個性化、內容管理系統、廣告伺服器以及您站點上運行的其他應用程式，以便從Adobe Experience Platform檢索段資訊。 此目標基於用戶配置檔案段成員身份提供即時個性化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: fb79d0697244518cc713efeada7d017d64ce6214
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# 自定義個性化連接 {#custom-personalization-connection}

## 總覽 {#overview}

此目的地提供了從Adobe Experience Platform檢索段資訊到外部個性化平台、內容管理系統、廣告伺服器以及在客戶網站上運行的其他應用程式的方法。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience PlatformWeb SDK](../../../edge/home.md) 或 [Adobe Experience Platform移動SDK](https://aep-sdks.gitbook.io/docs/)。 您必須使用其中一個SDK才能使用此目標。

## 導出類型 {#export-type}

**配置檔案請求**  — 您正在請求在自定義個性化目標中映射的所有段，以用於單個配置檔案。 可以為不同設定不同的自定義個性化目標 [Adobe資料收集資料流](../../../edge/fundamentals/datastreams.md)。

## 使用案例 {#use-cases}

此目標與廣告伺服器和非Adobe個性化應用程式共用受眾，用於即時確定用戶應在網站上看到哪些廣告。

### 用例#1

**個性化首頁**

一家房屋租賃和銷售網站希望根據Adobe Experience Platform的分部資格，將自己的首頁個性化。 公司可以選擇哪些受眾應獲得個性化體驗，並將這些體驗映射到為其非Adobe個性化應用程式設定的定製個性化目標，作為目標標準。

**定向現場廣告**

使用針對其廣告伺服器的單獨的自定義個性化目標，同一網站可以使用來自Adobe Experience Platform的不同段集作為目標標準來針對現場廣告。

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>在建立自定義個性化連接之前，我們建議您閱讀我們的指南，瞭解如何 [為同一頁和下一頁個性化設定配置個性化目標](../../ui/configure-personalization-destinations.md)。 本指南將引導您跨多個Experience Platform元件完成同一頁和下一頁個性化使用案例所需的配置步驟。

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流ID"
>abstract="此選項確定在響應頁面時將包括段的資料收集資料流的位置。 下拉菜單僅顯示啟用了目標配置的資料流。 必須先配置資料流，然後才能配置目標。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="瞭解如何配置資料流。"

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:輸入目標的說明。 例如，您可以提及您為此目標使用的市場活動。 此欄位為可選欄位。
* **[!UICONTROL 整合別名]**:此值將作為JSON對象名發送到Experience PlatformWeb SDK。
* **[!UICONTROL 資料流ID]**:這確定在響應頁面時將包括段的資料收集資料流的位置。 下拉菜單僅顯示啟用了目標配置的資料流。 請參閱 [配置資料流](../../../edge/fundamentals/datastreams.md) 的子菜單。

## 將段激活到此目標 {#activate}

閱讀 [激活配置檔案和段以配置請求目標](../../ui/activate-profile-request-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

如果您使用 [Adobe Experience Platform標籤](../../../tags/home.md) 要部署Experience PlatformWeb SDK，請使用 [發送事件完成](../../../edge/extension/event-types.md) 功能和自定義代碼操作將 `event.destinations` 可用於查看導出資料的變數。

下面是 `event.destinations` 變數：

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

如果您不使用 [標籤](../../../tags/home.md) 要部署Experience PlatformWeb SDK，請使用 [處理事件響應](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能，查看導出的資料。

可以分析來自Adobe Experience Platform的JSON響應，以查找您正與Adobe Experience Platform整合的應用程式的相應整合別名。 段ID可以作為目標參數傳遞給應用程式的代碼。 下面是特定於目標響應的示例。

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](../../../data-governance/home.md)。
