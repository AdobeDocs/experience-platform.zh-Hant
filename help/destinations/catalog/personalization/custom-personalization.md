---
keywords: 自訂個人化；目的地；experience platform自訂目的地；
title: 自訂個人化連線
description: 此目的地提供外部個人化、內容管理系統、廣告伺服器和其他在您網站上執行的應用程式，讓您能從Adobe Experience Platform擷取區段資訊。 此目的地會根據使用者設定檔區段成員資格提供即時個人化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# 自訂個人化連線 {#custom-personalization-connection}

## 目標更改日誌 {#changelog}

透過測試版， **[!UICONTROL 自訂個人化]** 目的地連接器，您可能會看到兩個 **[!UICONTROL 自訂個人化]** 目的地目錄中的卡。

此 **[!UICONTROL 使用屬性的自訂個人化]** 連接器目前為測試版，僅適用於特定數量的客戶。 除了 **[!UICONTROL 自訂個人化]**, **[!UICONTROL 使用屬性的自訂個人化]** 連接器新增可選 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 啟用工作流程，此工作流程可讓您將設定檔屬性對應至自訂個人化目的地，啟用以屬性為基礎的同頁和下一頁個人化。

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 為保護此資料， **[!UICONTROL 使用屬性的自訂個人化]** 目的地需要您使用 [邊緣網路伺服器API](/help/server-api/overview.md) 用於資料收集。 此外，所有伺服器API呼叫都必須在 [驗證內容](../../../server-api/authentication.md).
>
>如果您已使用Web SDK或Mobile SDK進行整合，則可透過伺服器API以兩種方式擷取屬性：
>
> * 新增伺服器端整合，可透過伺服器API擷取屬性。
> * 使用自訂Javascript程式碼更新用戶端設定，以透過伺服器API擷取屬性。
>
> 若您未遵循上述要求，個人化將僅根據區段成員資格，與提供的體驗相同 **[!UICONTROL 自訂個人化]** 連接器。

![並排檢視中兩個自訂個人化目的地卡片的影像。](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## 總覽 {#overview}

此目的地提供從Adobe Experience Platform擷取區段資訊至外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式的方法。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience Platform Web SDK](../../../edge/home.md) 或 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). 您必須使用其中一個SDK才能使用此目的地。

>[!IMPORTANT]
>
>建立自訂個人化連線之前，請參閱如何 [為同一頁面和下一頁個人化設定個人化目的地](../../ui/configure-personalization-destinations.md). 本指南會逐步引導您執行相同頁面和下一頁個人化使用案例所需的設定步驟，涵蓋多個Experience Platform元件。

## 匯出類型和頻率 {#export-type-frequency}

**設定檔要求**  — 您正在為單一設定檔請求在自訂個人化目的地中對應的所有區段。 可針對不同的項目設定不同的自訂個人化目的地 [Adobe資料收集資料流](../../../edge/datastreams/overview.md).

## 使用案例 {#use-cases}

此 [!DNL Custom Personalization Connection] 可讓您使用自己的個人化合作夥伴平台(例如 [!DNL Optimizely], [!DNL Pega])以及專屬系統（例如內部CMS），同時運用Experience Platform邊緣網路資料收集和分段功能，提供更深入的客戶個人化體驗。

以下說明的使用案例包括網站個人化和鎖定的站上廣告。

若要啟用這些使用案例，客戶需要快速、簡化的方式，從Experience Platform擷取區段資訊，並將這些資訊傳送至其指定系統，這些系統在Experience PlatformUI中設定為自訂個人化連線。

這些系統可以是外部個人化平台、內容管理系統、廣告伺服器，以及在客戶的Web和行動屬性上執行的其他應用程式。

### 同一頁面的個人化 {#same-page}

使用者造訪您網站的某個頁面。 客戶可使用目前的頁面瀏覽資訊（例如，反向連結URL、瀏覽器語言、內嵌產品資訊），使用非Adobe平台的自訂個人化連線(例如， [!DNL Pega], [!DNL Optimizely]等)。

### 下一頁個人化 {#next-page}

使用者造訪您網站上的頁面A。 根據此互動，使用者已符合一組區段的資格。 然後，使用者點按連結，將使用者從頁面A帶往頁面B。使用者在頁面A的上次互動期間符合資格的區段，以及目前網站造訪所決定的設定檔更新，將用來支援下一個動作/決策（例如要向訪客顯示哪個廣告橫幅，或在A/B測試的情況下，要顯示哪個頁面版本）。

### 下一個工作階段的個人化 {#next-session}

使用者瀏覽您網站上的數個頁面。 根據這些互動，使用者已符合一組區段的資格。 然後，用戶終止當前瀏覽會話。

次日，使用者返回同一個客戶網站。 他們在先前與所有已造訪網站頁面互動期間符合資格的區段，以及目前網站造訪所決定的設定檔更新，將用於選取下一個動作/決策（例如要向訪客顯示哪個廣告橫幅，或若是A/B測試，要顯示哪個頁面版本）。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料收集資料流中會在頁面回應中包含區段。下拉式選單僅顯示已啟用目的地設定的資料流。您必須先設定資料流，然後才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="了解如何設定資料流"

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。 例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
* **[!UICONTROL 整合別名]**:此值會以JSON物件名稱的形式傳送至Experience PlatformWeb SDK。
* **[!UICONTROL 資料流ID]**:這會決定要將區段納入頁面回應中的資料收集資料流。 下拉式選單僅顯示已啟用目的地設定的資料流。請參閱 [設定資料流](../../../edge/datastreams/overview.md) 以取得更多詳細資訊。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

如果您使用 [Adobe Experience Platform中的標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [傳送事件完成](../../../edge/extension/event-types.md) 功能和您的自訂程式碼動作 `event.destinations` 變數，以便查看匯出的資料。

以下是 `event.destinations` 變數：

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

如果您未使用 [標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [處理事件的回應](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能，檢視匯出的資料。

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 的範例回應 [!UICONTROL 使用屬性的自訂個人化]

使用時 **[!UICONTROL 使用屬性的自訂個人化]**，則API回應看起來會類似於下列範例。

兩者的差異 **[!UICONTROL 使用屬性的自訂個人化]** 和 **[!UICONTROL 自訂個人化]** 是將 `attributes` 一節。

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](../../../data-governance/home.md).
