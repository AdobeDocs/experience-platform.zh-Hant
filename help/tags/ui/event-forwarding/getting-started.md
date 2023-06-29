---
title: 事件轉送快速入門
description: 請依照此逐步教學課程，開始使用Adobe Experience Platform中的事件轉送。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 27%

---

# 事件轉送快速入門

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

若要在Adobe Experience Platform中使用事件轉送，您必須使用下列一個或多個選項，將資料傳送至Adobe Experience Platform Edge Network：

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [伺服器對伺服器API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Platform Web SDK和Platform Mobile SDK不需要透過Adobe Experience Platform中的標籤進行部署。 不過，建議使用標籤來部署這些SDK。

將資料傳送至 Edge Network 後，您就可以開啟 Adobe 解決方案，將資料傳送至該處。若要將資料傳送至非Adobe解決方案，請在事件轉送中設定。

## 先決條件

* Adobe Experience Platform Collection Enterprise (如需定價，請聯絡您的Adobe客戶團隊)
* Adobe Experience Platform中的事件轉送
* 設定 Adobe Experience Platform Web 或 Mobile SDK，將資料傳送至 Edge Network
* 將資料對應至Experience Data Model (XDM) （此對應可使用標籤完成）

## 建立 XDM 結構描述

在 Adobe Experience Platform 中建立結構描述。

1. 選取以下專案建立結構描述： **[!UICONTROL 結構描述]**>**[!UICONTROL 建立結構描述]** 並選取 **[!UICONTROL XDM ExperienceEvent]** 選項。

1. 為結構描述命名並提供簡短說明。

1. 您可以選取「 」，新增「ExperienceEvent Web詳細資訊」欄位群組 **[!UICONTROL 新增]** 旁邊 **[!UICONTROL 欄位群組]**.

   >[!NOTE]
   >
   >如有需要，可新增多個欄位群組。

1. 儲存結構描述並記下您命名的名稱。

如需結構描述的詳細資訊，請參閱 [Experience Data Model (XDM) 系統說明](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)。

## 建立事件轉送屬性

在 **[!UICONTROL 標籤]** workspace，建立型別的屬性 **[!UICONTROL Edge]**.

1. 選取&#x200B;**[!UICONTROL 「新屬性」]**。

1. 為屬性命名。

1. 選擇「邊緣」平台型別。

1. 選取「**[!UICONTROL 儲存]**」。

建立屬性後，前往 **[!UICONTROL 環境]** 索引標籤中的專案並記下環境ID。 如果資料流中使用的Adobe組織與事件轉送中使用的Adobe組織不同，您可以從 **[!UICONTROL 環境]** 建立資料流時按Tab鍵並貼上。 或者，您也可以從下拉式選單中選取環境。

## 建立資料串流

若要在Adobe Experience Platform中建立資料串流，請使用建立事件轉送屬性時產生的環境ID。

1. 選取 **[!UICONTROL 資料串流]** 左側導覽列中。

1. 為組態命名並選擇是否填寫相關說明。說明可協助您在組態清單中識別各個組態。

1. 選取「**[!UICONTROL 儲存]**」。

## 啟用事件轉送

接下來，設定Edge Network將資料傳送至事件轉送和其他Adobe產品。

1. 在 **[!UICONTROL 資料串流]** 工作區中，選取您建立的屬性。

1. 選取「開發」、「生產」或「預備」環境。

   或者，若要將資料傳送至Adobe組織外部的事件轉送環境，請選取 **[!UICONTROL 切換到進階模式]** 並貼入ID。 ID是在您建立事件轉送屬性時提供。

1. 開啟必要工具並依需求設定。

   * Adobe Analytics 會要求您輸入報表套裝 ID。

   * Adobe Experience Platform中的事件轉送需要屬性ID和環境ID。 這是事件轉送屬性的發佈路徑。

完成設定後，記下新屬性的環境 ID。

## 設定Platform Web SDK擴充功能，將資料傳送至先前建立的資料流

在中建立您的屬性 **[!UICONTROL 標籤]** 工作區，然後導覽至 **[!UICONTROL 擴充功能]** 並從目錄中選取Experience PlatformWeb SDK擴充功能以進行設定和安裝。

請參閱 [Web SDK擴充功能檔案](../../extensions/client/web-sdk/overview.md) 以取得組態選項的詳細資訊。

## 建立標籤規則以將資料傳送至Platform Web SDK

完成上述設定後，即可建立使用事件轉送和標籤，但只需要從頁面提出單一請求的資料定義、規則等。

使用Platform Web SDK擴充功能和「傳送事件」動作型別，建立頁面載入規則：

1. 開啟 **[!UICONTROL 規則]** 索引標籤，然後選取 **[!UICONTROL 建立新規則]**.

1. 為規則命名。

1. 選取 **[!UICONTROL 事件新增]**.

1. 選擇擴充功能及該擴充功能提供的任一事件類型以新增事件，然後設定事件相關設定，例如，選取 **[!UICONTROL 核心 — 視窗已載入]**.

1. 使用 Platform Web SDK 擴充功能新增動作。選取 **[!UICONTROL 傳送事件]** 從 **[!UICONTROL 動作型別]** 清單中，選取所需的執行個體（之前設定的Alloy執行個體），然後選取要新增至Alloy點選內XDM資料區塊的資料元素。

1. 其餘設定維持此範例中的預設值，並選取 **[!UICONTROL 儲存]**.

再舉個例子：您可能可以建立一項規則，在使用者將游標停留在指定按鈕上時，將資料層傳送至邊緣。

## 摘要

設定好下列專案後，您現在可以建立事件轉送規則，將資料轉送至非Adobe目的地。

* Experience Data Model結構描述（記下您命名的名稱）
* 事件轉送屬性（追蹤屬性ID和環境ID）。
* 資料串流（記下環境ID，切勿與事件轉送的環境ID混淆）。
* 標籤屬性
