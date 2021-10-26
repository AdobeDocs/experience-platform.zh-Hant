---
keywords: 自訂個人化；目的地；experience platform自訂目的地；
title: 自訂個人化連線（測試版）
description: 此目的地提供外部個人化、內容管理系統、廣告伺服器，以及網站上執行的其他應用程式，以從Adobe Experience Platform擷取區段資訊。 此目的地會根據使用者設定檔的區段成員資格提供即時1:1和個人化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 50ab34cb9147cf880e199afad88e718875fb591f
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# 自訂個人化連線（測試版） {#custom-personalization-connection}

## 總覽 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的自訂個人化連線目前處於測試階段。 檔案和功能可能會有所變更。

此目的地提供從Adobe Experience Platform擷取區段資訊至外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式的方法。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience Platform Web SDK](../../../edge/home.md). 您必須使用此SDK才能使用此目的地。

## 匯出類型 {#export-type}

**設定檔要求**  — 您正在為單一設定檔請求在自訂個人化目的地中對應的所有區段。 可針對不同的項目設定不同的自訂個人化目的地 [Adobe資料收集資料流](../../../edge/fundamentals/datastreams.md).

## 使用案例 {#use-cases}

此目的地會與廣告伺服器和非Adobe個人化應用程式共用閱聽眾，以用於即時決定使用者應在網站上看到的廣告。

### 使用案例#1

**個人化首頁**

一家房屋租賃與銷售網站想要根據Adobe Experience Platform中的區段資格來個人化其首頁。 公司可以選取哪些對象應該獲得個人化體驗，並將這些對象對應至已針對其非Adobe個人化應用程式所設定的自訂個人化目的地，作為鎖定目標條件。

**目標站上廣告**

使用其廣告伺服器的個別自訂個人化目的地，相同的網站可以使用來自Adobe Experience Platform的不同區段集來鎖定站上廣告作為鎖定目標條件。

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。 例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
* **[!UICONTROL 整合別名]**:此值會以JSON物件名稱的形式傳送至Experience PlatformWeb SDK。
* **[!UICONTROL 資料流ID]**:這會決定要將區段納入頁面回應中的資料收集資料流。 下拉式功能表只會顯示已啟用目的地設定的資料流。 請參閱 [設定資料流](../../../edge/fundamentals/datastreams.md) 以取得更多詳細資訊。

## 啟用此目的地的區段 {#activate}

閱讀 [啟動設定檔和區段至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

如果您使用 [Adobe標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [傳送事件完成](../../../edge/extension/event-types.md) 功能和您的自訂程式碼動作 `event.destinations` 變數，以便查看匯出的資料。

以下是 `event.destinations` 變數：

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77",
            "mergePolicyId":"69638c01-2099-4032-8b41-84bee8ebcfa4"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77",
            "mergePolicyId":"69638c01-2099-4032-8b41-84bee8ebcfa4"
         }
      ]
   }
]
```

如果您未使用 [Adobe標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [處理事件的回應](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能，檢視匯出的資料。

可剖析Adobe Experience Platform的JSON回應，以尋找您要與Adobe Experience Platform整合之應用程式的對應整合別名。 區段ID可作為定位參數傳遞至應用程式的程式碼中。 以下是特定於目的地回應的顯示範例。

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


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](../../../data-governance/home.md).
