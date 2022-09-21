---
title: 事件轉送快速入門
description: 請依照此逐步教學課程，開始使用Adobe Experience Platform中的事件轉送。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 26%

---

# 事件轉送快速入門

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

若要在Adobe Experience Platform中使用事件轉送，必須使用下列三個選項之一或多個，將資料傳送至Adobe Experience Platform邊緣網路：

* [Adobe Experience Platform Web SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [伺服器對伺服器API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Platform Web SDK和Platform Mobile SDK不需要透過Adobe Experience Platform中的標籤進行部署。 不過，建議使用標籤來部署這些SDK。

將資料傳送至 Edge Network 後，您就可以開啟 Adobe 解決方案，將資料傳送至該處。若要將資料傳送至非Adobe解決方案，請在事件轉送中設定。

## 先決條件

* Adobe Experience Platform Collection Enterprise（請洽詢您的客戶經理以取得價格）
* Adobe Experience Platform中的事件轉送
* 設定 Adobe Experience Platform Web 或 Mobile SDK，將資料傳送至 Edge Network
* 將資料對應至Experience Data Model(XDM)（此對應可使用標籤完成）

## 建立 XDM 結構描述

在 Adobe Experience Platform 中建立結構描述。

1. 透過選取 **[!UICONTROL 結構]**>**[!UICONTROL 建立結構]** 和選擇 **[!UICONTROL XDM ExperienceEvent]** 選項。

1. 為結構描述命名並提供簡短說明。

1. 您可以選取 **[!UICONTROL 新增]** 下一頁 **[!UICONTROL 欄位群組]**.

   >[!NOTE]
   >
   >如有需要，可新增多個欄位群組。

1. 儲存結構並記下您提供的名稱。

如需結構描述的詳細資訊，請參閱 [Experience Data Model (XDM) 系統說明](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)。

## 建立事件轉送屬性

在 **[!UICONTROL 標籤]** 工作區，建立類型的屬性 **[!UICONTROL Edge]**.

1. 選擇 **[!UICONTROL 新屬性]**.

1. 為屬性命名。

1. 選擇「Edge」平台類型。

1. 選取「**[!UICONTROL 儲存]**」。

建立屬性後，請前往 **[!UICONTROL 環境]** 標籤，並記下環境ID。 如果資料流中使用的Adobe組織與事件轉送中使用的Adobe組織不同，您可以從 **[!UICONTROL 環境]** 標籤，並在建立資料流時貼上。 或者，您也可以從下拉式選單中選取環境。

## 建立資料流

若要在Adobe Experience Platform中建立資料流，請使用建立事件轉送屬性時產生的環境ID。

1. 選擇 **[!UICONTROL 資料流]** 的下一頁。

1. 為組態命名並選擇是否填寫相關說明。說明可協助您在組態清單中識別各個組態。

1. 選取「**[!UICONTROL 儲存]**」。

## 啟用事件轉送

接下來，設定邊緣網路，將資料傳送至事件轉送和其他Adobe產品。

1. 在 **[!UICONTROL 資料流]** 工作區中，選取您建立的屬性。

1. 選取「開發」、「生產」或「預備」環境。

   或者，若要將資料傳送至Adobe組織以外的事件轉送環境，請選取 **[!UICONTROL 切換到高級模式]** 並貼入ID。 建立事件轉送屬性時，會提供ID。

1. 開啟必要工具並依需求設定。

   * Adobe Analytics 會要求您輸入報表套裝 ID。

   * Adobe Experience Platform中的事件轉送需要屬性ID和環境ID。 這是事件轉送屬性的發佈路徑。

完成設定後，記下新屬性的環境 ID。

## 設定Platform Web SDK擴充功能，將資料傳送至先前建立的資料流

在 **[!UICONTROL 標籤]** 工作區，然後導覽至 **[!UICONTROL 擴充功能]** 並從目錄中選取「Experience PlatformWeb SDK」擴充功能，以進行設定及安裝。

請參閱 [Web SDK擴充功能檔案](../../extensions/web/sdk/overview.md) 以取得設定選項的詳細資訊。

## 建立標籤規則以將資料傳送至Platform Web SDK

完成上述設定後，請建置資料定義、規則等，這些使用事件轉送和標籤，但只需要頁面中的單一要求。

使用Platform Web SDK擴充功能和「傳送事件」動作類型，建立頁面載入規則：

1. 開啟 **[!UICONTROL 規則]** ，然後選取 **[!UICONTROL 建立新規則]**.

1. 為規則命名。

1. 選擇 **[!UICONTROL 事件新增]**.

1. 選擇擴充功能及該擴充功能提供的任一事件類型以新增事件，然後設定事件相關設定，例如，選取 **[!UICONTROL 核心 — 視窗已載入]**.

1. 使用 Platform Web SDK 擴充功能新增動作。選擇 **[!UICONTROL 傳送事件]** 從 **[!UICONTROL 動作類型]** 清單中，選取所需的執行個體（先前設定的Alloy執行個體），然後選取資料元素，以在Alloy點擊中新增至XDM資料區塊。

1. 將其餘的設定保留為此範例的預設值，然後選取 **[!UICONTROL 儲存]**.

再舉個例子：您可能可以建立一項規則，在使用者將游標停留在指定按鈕上時，將資料層傳送至邊緣。

## 摘要

具備下列功能後，您現在可以建立事件轉送規則，將資料轉送至非Adobe目的地。

* 體驗資料模型結構（請注意您提供的名稱。）
* 事件轉送屬性（追蹤屬性ID和環境ID）。
* 資料流（請注意環境ID，不要與事件轉送的環境ID混淆）。
* 標籤屬性
