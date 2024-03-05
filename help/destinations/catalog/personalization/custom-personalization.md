---
keywords: 自訂個人化；目的地；experience platform自訂目的地；
title: 自訂個人化連線
description: 此目的地提供外部個人化、內容管理系統、廣告伺服器，以及在您的網站上執行的其他應用程式，以便從Adobe Experience Platform擷取對象資訊。 此目的地會根據使用者設定檔對象成員資格，提供即時個人化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 9%

---


# 自訂個人化連線 {#custom-personalization-connection}

## 目的地變更記錄檔 {#changelog}

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 5 月 | 功能和檔案更新 | 截至2023年5月， **[!UICONTROL 自訂個人化]** 連線支援 [屬性型個人化](../../ui/activate-edge-personalization-destinations.md#map-attributes) 並且通常可供所有客戶使用。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 若要保護此資料，您必須使用 [Edge Network伺服器API](/help/server-api/overview.md) 設定時 **[!UICONTROL 自訂個人化]** 屬性型個人化的目的地。 所有伺服器API呼叫都必須在 [已驗證的內容](../../../server-api/authentication.md).
>
><br>如果您已在使用Web SDK或Mobile SDK進行整合，您可以透過新增伺服器端整合來透過伺服器API擷取屬性。
>
><br>如果您未遵循上述要求，個人化將僅以對象成員資格為基礎。

## 概觀 {#overview}

設定此目的地，以允許客戶網站上執行的外部個人化平台、內容管理系統、廣告伺服器及其他應用程式，從Adobe Experience Platform擷取對象資訊。

## 先決條件 {#prerequisites}

這項整合由以下提供技術支援 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 或 [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/). 您必須使用其中一個SDK才能使用此目的地。

>[!IMPORTANT]
>
>在建立自訂個人化連線之前，請先參閱以下操作指南： [啟用對象資料至邊緣個人化目的地](../../ui/activate-edge-personalization-destinations.md). 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行所需設定步驟。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!DNL Profile request]** | 您正在請求已對應至單一設定檔之自訂個人化目的地的所有對象。 您可以為不同的設定不同的自訂個人化目的地 [Adobe資料收集資料串流](../../../datastreams/overview.md). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

## 連線到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料集合資料流中會在頁面回應中包含對象。下拉選單僅顯示已啟用目的地設定的資料流。您必須先設定資料流，然後才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=zh-Hant" text="了解如何設定資料流"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：輸入目的地的說明。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **[!UICONTROL 整合別名]**：此值會以JSON物件名稱的形式傳送至Experience PlatformWeb SDK。
* **[!UICONTROL 資料串流ID]**：這會決定將對象包含在頁面的回應中的資料收集資料串流。 下拉選單僅顯示已啟用目的地設定的資料流。另請參閱 [設定資料串流](../../../datastreams/overview.md) 以取得更多詳細資料。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [啟用設定檔和受眾邊緣個人化目的地](../../ui/activate-edge-personalization-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料 {#exported-data}

如果您使用 [Adobe Experience Platform中的標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [傳送事件完成](../../../tags/extensions/client/web-sdk/event-types.md) 功能和您的自訂程式碼動作將具有 `event.destinations` 變數，可用來檢視匯出的資料。

以下是的範例值 `event.destinations` 變數：

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

如果您沒有使用 [標籤](/help/tags/home.md) 若要部署Experience Platform Web SDK，請使用 [命令回應](/help/web-sdk/commands/command-responses.md) 以檢視匯出的資料。

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

### 的範例回應 [!UICONTROL 使用屬性的自訂個人化]

使用時 **[!UICONTROL 使用屬性的自訂個人化]**，API回應將與下列範例類似。

兩者之間的差異 **[!UICONTROL 使用屬性的自訂個人化]** 和 **[!UICONTROL 自訂個人化]** 是包含的 `attributes` API回應中的區段。

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

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](../../../data-governance/home.md).
