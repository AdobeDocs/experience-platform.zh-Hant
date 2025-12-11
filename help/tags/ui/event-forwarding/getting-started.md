---
title: 事件轉送快速入門
description: 請依照此逐步教學課程，開始在Adobe Experience Platform中使用事件轉送。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 30%

---

# 事件轉送快速入門

>[!NOTE]
>
>事件轉送是一項付費功能，包含在Adobe Real-Time Customer Data Platform連線、Prime或Ultimate供應專案中。

若要在Adobe Experience Platform中使用事件轉送，必須使用下列一個或多個選項，將資料傳送至Adobe Experience Platform Edge Network：

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>Experience Platform Web SDK和Experience Platform Mobile SDK不需要透過Adobe Experience Platform中的標籤進行部署。 不過，建議使用標籤來部署這些SDK。

將資料傳送至 Edge Network 後，您就可以開啟 Adobe 解決方案，將資料傳送至該處。若要將資料傳送至非Adobe解決方案，請在事件轉送中設定。

## 先決條件

* Adobe Real-Time CDP Connections、Prime或Ultimate (如需定價，請聯絡您的Adobe客戶團隊)
* Adobe Experience Platform中的事件轉送
* Adobe Experience Platform Web SDK、Mobile SDK或Edge Network API已設定為傳送資料至Edge Network
* 將資料對應至Experience Data Model (XDM) （此對應可使用標籤完成）

## 建立 XDM 結構描述

在 Adobe Experience Platform 中建立結構描述。

1. 選取&#x200B;**[!UICONTROL Schemas]**>**[!UICONTROL Create Schema]**&#x200B;並選擇&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;選項以建立結構描述。

1. 為結構描述命名並提供簡短說明。

1. 您可以選取&#x200B;**[!UICONTROL Add]**&#x200B;旁的&#x200B;**[!UICONTROL Field Groups]**，新增「ExperienceEvent Web詳細資料」欄位群組。

   >[!NOTE]
   >
   >如果需要，可以新增多個欄位群組。

1. 儲存結構描述，並記下您命名的名稱。

如需結構描述的詳細資訊，請參閱 [Experience Data Model (XDM) 系統說明](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)。

## 建立事件轉送屬性

在&#x200B;**[!UICONTROL Tags]**&#x200B;工作區中，建立型別&#x200B;**[!UICONTROL Edge]**&#x200B;的屬性。

1. 選擇「**[!UICONTROL New Property]**」。

1. 為屬性命名。

1. 選擇「Edge」平台型別。

1. 選擇「**[!UICONTROL Save]**」。

建立屬性後，請前往新屬性的「**[!UICONTROL Environments]**」索引標籤，然後記下環境 ID。如果資料流中使用的Adobe組織與事件轉送中使用的Adobe組織不同，您可以從「**[!UICONTROL Environments]**」索引標籤複製環境ID，並在建立資料流時貼上。 或者，您也可以從下拉式選單中選取環境。

## 建立資料串流

若要在Adobe Experience Platform中建立資料串流，請使用建立事件轉送屬性時產生的環境ID。

1. 在左側導覽中選取&#x200B;**[!UICONTROL Datastreams]**。

1. 為組態命名並選擇是否填寫相關說明。說明可協助您在組態清單中識別各個組態。

1. 選擇「**[!UICONTROL Save]**」。

## 啟用事件轉送 {#enable-event-forwarding}

接下來，設定Edge Network將資料傳送至事件轉送及其他Adobe產品。

1. 在&#x200B;**[!UICONTROL Datastreams]**&#x200B;工作區中，選取您建立的屬性。

1. 選取「開發」、「生產」或「預備」環境。

   若要將資料傳送至Adobe組織以外的事件轉送環境，請選取「**[!UICONTROL Switch to Advanced Mode]**」並貼入ID。 ID是在您建立事件轉送屬性時提供。

1. 開啟必要工具並依需求設定。

   * Adobe Analytics 會要求您輸入報表套裝 ID。

   * Adobe Experience Platform中的事件轉送需要屬性ID和環境ID。 這是事件轉送屬性的發佈路徑。

完成設定後，記下新屬性的環境 ID。

## 設定Experience Platform Web SDK擴充功能，將資料傳送至先前建立的資料流

在&#x200B;**[!UICONTROL Tags]**&#x200B;工作區中建立您的屬性，然後導覽至&#x200B;**[!UICONTROL Extensions]**，並從目錄中選取Experience Platform Web SDK擴充功能以設定和安裝它。

如需設定選項的詳細資訊，請參閱[Web SDK擴充功能檔案](../../extensions/client/web-sdk/overview.md)。

## 建立標籤規則以將資料傳送至Experience Platform Web SDK

完成上述設定後，即可建立使用事件轉送和標籤，但只需要來自頁面的單一請求的資料定義、規則等。

使用Experience Platform Web SDK擴充功能和「傳送事件」動作型別，建立頁面載入規則：

1. 開啟「**[!UICONTROL Rules]**」索引標籤，然後選取「**[!UICONTROL Create New Rule]**」。

1. 為規則命名。

1. 選擇「**[!UICONTROL Events Add]**」。

1. 選擇擴充功能及該擴充功能提供的任一事件類型以新增事件，然後設定事件相關設定，例如選取「**[!UICONTROL Core - Window Loaded]**」。

1. 使用Experience Platform Web SDK擴充功能新增動作。 在「**[!UICONTROL Action Type]**」清單中選取「**[!UICONTROL Send Event]**」，接著選取所需例項 (之前設定的 Alloy 例項)，再選取要新增至 Alloy 點擊內 XDM 資料區塊的資料元素。

1. 其餘設定維持此範例中的預設值，並選取「**[!UICONTROL Save]**」。

再舉個例子：您可能可以建立一項規則，在使用者將游標停留在指定按鈕上時，將資料層傳送至邊緣。

## 摘要

設定好下列專案，您就可以建立事件轉送規則，將資料轉送至Adobe以外的目的地。

* Experience Data Model結構描述（記下您命名的名稱）
* 事件轉送屬性（追蹤屬性ID和環境ID）。
* 資料串流（記下環境ID，別與事件轉送的環境ID混淆）
* 標籤屬性
