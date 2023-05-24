---
keywords: 自定義個性化；目的地；體驗平台定制目標；
title: 自定義個性化連接
description: 此目標提供外部個性化、內容管理系統、廣告伺服器以及您站點上運行的其他應用程式，以便從Adobe Experience Platform檢索段資訊。 此目標基於用戶配置檔案段成員身份提供即時個性化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# 自定義個性化連接 {#custom-personalization-connection}

## 目標更改日誌 {#changelog}

使用Beta版 **[!UICONTROL 自定義個性化]** 目標連接器，您可能看到兩個 **[!UICONTROL 自定義個性化]** 目的地目錄中的卡。

的 **[!UICONTROL 具有屬性的自定義個性化]** 連接器當前處於測試版中，並且僅適用於選定數量的客戶。 除了 **[!UICONTROL 自定義個性化]**，也請參見Wiki頁。 **[!UICONTROL 具有屬性的自定義個性化]** 連接器添加可選 [映射步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 激活工作流，它允許您將配置檔案屬性映射到自定義個性化目標，從而啟用基於屬性的同頁和下一頁個性化。

>[!IMPORTANT]
>
>配置檔案屬性可能包含敏感資料。 為保護此資料， **[!UICONTROL 具有屬性的自定義個性化]** 目標要求您使用 [邊緣網路伺服器API](/help/server-api/overview.md) 的下界。 此外，所有伺服器API調用必須在 [已驗證上下文](../../../server-api/authentication.md)。
>
>如果已使用Web SDK或Mobile SDK進行整合，則可以通過伺服器API以兩種方式檢索屬性：
>
> * 添加通過伺服器API檢索屬性的伺服器端整合。
> * 使用自定義Javascript代碼更新客戶端配置，以通過伺服器API檢索屬性。
>
> 如果您不遵循上述要求，個性化將僅基於段成員資格，與提供的體驗相同 **[!UICONTROL 自定義個性化]** 連接器。

![並排視圖中兩個自定義個性化目標卡的影像。](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## 總覽 {#overview}

此目的地提供了從Adobe Experience Platform檢索段資訊到外部個性化平台、內容管理系統、廣告伺服器以及在客戶網站上運行的其他應用程式的方法。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience PlatformWeb SDK](../../../edge/home.md) 或 [Adobe Experience Platform移動SDK](https://aep-sdks.gitbook.io/docs/)。 您必須使用其中一個SDK才能使用此目標。

>[!IMPORTANT]
>
>建立自定義個性化連接之前，請閱讀有關如何 [為同一頁和下一頁個性化設定配置個性化目標](../../ui/configure-personalization-destinations.md)。 本指南將引導您跨多個Experience Platform元件完成同一頁和下一頁個性化使用案例所需的配置步驟。

## 導出類型和頻率 {#export-type-frequency}

**配置檔案請求**  — 您正在請求在自定義個性化目標中映射的所有段，以用於單個配置檔案。 可以為不同設定不同的自定義個性化目標 [Adobe資料收集資料流](../../../edge/datastreams/overview.md)。

## 使用案例 {#use-cases}

的 [!DNL Custom Personalization Connection] 使您能夠使用您自己的個性化合作夥伴平台(例如， [!DNL Optimizely]。 [!DNL Pega])，以及專有系統（例如，內部CMS），同時還利用Experience Platform邊緣網路資料收集和分段功能，為更深入的客戶個性化體驗提供動力。

下面描述的使用案例包括站點個性化和目標現場廣告。

要啟用這些使用情形，客戶需要一種快速、簡化的方法，從Experience Platform中檢索段資訊，並將此資訊發送到他們在Experience PlatformUI中配置為自定義個性化連接的指定系統。

這些系統可以是外部個性化平台、內容管理系統、廣告伺服器，以及運行於客戶Web和移動屬性上的其他應用程式。

### 同一頁面的個人化 {#same-page}

用戶訪問您網站的頁面。 客戶可以使用當前頁面訪問資訊（例如，引用URL、瀏覽器語言、嵌入式產品資訊）來選擇下一個操作/決策（例如，個性化），使用非Adobe平台的自定義個性化連接(例如， [!DNL Pega]。 [!DNL Optimizely]等)。

### 下一頁個性化 {#next-page}

用戶訪問您網站上的A頁。 基於此交互，用戶已限定一組段。 然後，用戶按一下將其從A頁轉到B頁的連結。用戶在A頁上上次交互期間限定的段以及當前網站訪問確定的概要檔案更新，將用於支援下一操作/決定（例如，向訪問者顯示哪個廣告橫幅，或在A/B測試中顯示哪個版本的頁面）。

### 下一個工作階段的個人化 {#next-session}

用戶訪問您網站上的幾頁。 基於這些交互，用戶已限定一組段。 用戶然後終止當前瀏覽會話。

次日，用戶返回同一客戶網站。 他們在與所有訪問網站頁面的上次交互過程中限定的段，以及由當前網站訪問確定的配置檔案更新，將用於選擇下一操作/決定（例如，向訪問者顯示哪個廣告橫幅，或在A/B測試中顯示哪個版本的頁面）。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料收集資料流中會在頁面回應中包含區段。下拉式選單僅顯示已啟用目的地設定的資料流。您必須先設定資料流，然後才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="了解如何設定資料流"

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:輸入目標的說明。 例如，您可以提及您為此目標使用的市場活動。 此欄位為可選欄位。
* **[!UICONTROL 整合別名]**:此值將作為JSON對象名發送到Experience PlatformWeb SDK。
* **[!UICONTROL 資料流ID]**:這確定在響應頁面時將包括段的資料收集資料流的位置。 下拉式選單僅顯示已啟用目的地設定的資料流。請參閱 [配置資料流](../../../edge/datastreams/overview.md) 的子菜單。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

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

### 示例響應 [!UICONTROL 具有屬性的自定義個性化]

使用時 **[!UICONTROL 具有屬性的自定義個性化]**, API響應將與下面的示例類似。

兩者之差 **[!UICONTROL 具有屬性的自定義個性化]** 和 **[!UICONTROL 自定義個性化]** 是 `attributes` 的子菜單。

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

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](../../../data-governance/home.md)。
