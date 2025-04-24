---
keywords: 自訂個人化；目的地；experience platform自訂目的地；
title: 自訂個人化連線
description: 此目的地提供外部個人化、內容管理系統、廣告伺服器，以及在您的網站上執行的其他應用程式，以便從Adobe Experience Platform擷取對象資訊。 此目的地會根據使用者設定檔對象成員資格，提供即時個人化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 25697d341b2970eeb20d9f2507ee701ade8046d3
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 9%

---


# 自訂個人化連線 {#custom-personalization-connection}

## 目的地變更記錄檔 {#changelog}

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 5 月 | 功能和檔案更新 | 自2023年5月起，**[!UICONTROL 自訂個人化]**&#x200B;連線支援[屬性式個人化](../../ui/activate-edge-personalization-destinations.md#map-attributes)，通常可供所有客戶使用。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 若要保護此資料，您必須在為屬性式個人化設定&#x200B;**[!UICONTROL 自訂Personalization]**&#x200B;目的地時，使用[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)。 所有Edge Network API呼叫都必須在[已驗證的內容](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication)中進行。
>
><br>您可以新增伺服器端整合，利用您已在網頁或行動SDK實作中使用的相同資料流，透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)擷取設定檔屬性。
>
><br>如果您未遵循上述要求，個人化將僅以對象成員資格為基礎。

## 概觀 {#overview}

設定此目的地，以允許客戶網站上執行的外部個人化平台、內容管理系統、廣告伺服器及其他應用程式，從Adobe Experience Platform擷取對象資訊。

## 先決條件 {#prerequisites}

根據您的實作，此目的地需要使用下列其中一個資料收集方法：

* 如果您想要從網站收集資料，請使用[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)。
* 如果您想要從行動應用程式收集資料，請使用[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)。
* 如果您未使用[網頁SDK](/help/web-sdk/home.md)或[行動SDK](https://developer.adobe.com/client-sdks/documentation/)，或您想要根據設定檔屬性個人化使用者體驗，請使用[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)。

>[!IMPORTANT]
>
>在建立自訂個人化連線之前，請閱讀如何[啟用對象資料至Edge個人化目的地](../../ui/activate-edge-personalization-destinations.md)的指南。 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行所需設定步驟。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!DNL Profile request]** | 您正在請求已對應至單一設定檔之自訂個人化目的地的所有對象。 可以為不同的[Adobe資料收集資料串流](../../../datastreams/overview.md)設定不同的自訂個人化目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

## 連線到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料集合資料流中會在頁面回應中包含對象。下拉選單僅顯示已啟用目的地設定的資料流。您必須先設定資料流，然後才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="了解如何設定資料流"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：輸入目的地的描述。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **[!UICONTROL 整合別名]**：此值會作為JSON物件名稱傳送到Experience Platform Web SDK。
* **[!UICONTROL 資料串流ID]**：這會決定要在頁面的回應中包含對象的資料收集資料串流。 下拉選單僅顯示已啟用目的地設定的資料流。如需詳細資訊，請參閱[設定資料串流](../../../datastreams/overview.md)。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用設定檔與對象邊緣個人化目的地](../../ui/activate-edge-personalization-destinations.md)，以取得啟用此目的地的對象的指示。

## 匯出的資料 {#exported-data}

如果您使用Adobe Experience Platform](../../../tags/home.md)中的[標籤來部署Experience Platform Web SDK，請使用[傳送事件完成](../../../tags/extensions/client/web-sdk/event-types.md)功能，而您的自訂程式碼動作將有`event.destinations`變數，可用來檢視匯出的資料。

以下是`event.destinations`變數的範例值：

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

如果您不是使用[標籤](/help/tags/home.md)來部署Experience Platform Web SDK，請使用[命令回應](/help/web-sdk/commands/command-responses.md)來檢視匯出的資料。

來自Adobe Experience Platform的JSON回應可加以剖析，以找出您要與Adobe Experience Platform整合之應用程式的對應整合別名。 對象ID可傳入應用程式的程式碼中作為定位引數。 以下是目標回應特有的內容範例。

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
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 具有屬性]的[!UICONTROL 自訂Personalization的範例回應

使用具有屬性&#x200B;]**的**[!UICONTROL &#x200B;自訂Personalization時，API回應將與以下範例類似。

**[!UICONTROL 具有屬性的自訂Personalization]**&#x200B;與&#x200B;**[!UICONTROL 自訂Personalization]**&#x200B;之間的差異在於API回應中包含`attributes`區段。

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

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](../../../data-governance/home.md)。
