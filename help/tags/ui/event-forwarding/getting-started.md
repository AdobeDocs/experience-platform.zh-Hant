---
title: 事件轉發入門
description: 按照本逐步教程開始使用Adobe Experience Platform的事件轉發。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 27%

---

# 事件轉發入門

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

要在Adobe Experience Platform使用事件轉發，必須使用以下三個選項中的一個或多個將資料發送到Adobe Experience Platform邊緣網路：

* [Adobe Experience Platform Web SDK](../../extensions/client/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [伺服器到伺服器API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>平台Web SDK和平台移動SDK不需要通過Adobe Experience Platform的標籤進行部署。 但是，建議使用標籤來部署這些SDK。

將資料傳送至 Edge Network 後，您就可以開啟 Adobe 解決方案，將資料傳送至該處。要將資料發送到非Adobe解決方案，請在事件轉發時設定該解決方案。

## 先決條件

* Adobe Experience Platform收集企業(請與您的Adobe帳戶團隊聯繫以獲取定價)
* Adobe Experience Platform事件轉發
* 設定 Adobe Experience Platform Web 或 Mobile SDK，將資料傳送至 Edge Network
* 將資料映射到體驗資料模型(XDM)（此映射可使用標籤完成）

## 建立 XDM 結構描述

在 Adobe Experience Platform 中建立結構描述。

1. 通過選擇 **[!UICONTROL 架構]**>**[!UICONTROL 建立架構]** 選擇 **[!UICONTROL XDM體驗事件]** 的雙曲餘切值。

1. 為結構描述命名並提供簡短說明。

1. 通過選擇 **[!UICONTROL 添加]** 下 **[!UICONTROL 欄位組]**。

   >[!NOTE]
   >
   >如果需要，可以添加多個欄位組。

1. 保存架構並記下您給它的名稱。

如需結構描述的詳細資訊，請參閱 [Experience Data Model (XDM) 系統說明](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)。

## 建立事件轉發屬性

在 **[!UICONTROL 標籤]** 工作區，建立類型的屬性 **[!UICONTROL 邊緣]**。

1. 選取&#x200B;**[!UICONTROL 「新屬性」]**。

1. 為屬性命名。

1. 選擇「邊緣」平台類型。

1. 選取「**[!UICONTROL 儲存]**」。

建立屬性後，轉到 **[!UICONTROL 環境]** 的子菜單。 如果資料流中使用的Adobe組織與事件轉發中使用的Adobe組織不同，則可以從 **[!UICONTROL 環境]** 頁籤，並在建立資料流時貼上。 或者，您也可以從下拉式選單中選取環境。

## 建立資料流

要在Adobe Experience Platform建立資料流，請使用建立事件轉發屬性時生成的環境ID。

1. 選擇 **[!UICONTROL 資料流]** 的子菜單。

1. 為組態命名並選擇是否填寫相關說明。說明可協助您在組態清單中識別各個組態。

1. 選取「**[!UICONTROL 儲存]**」。

## 啟用事件轉發

接下來，配置邊緣網路以將資料發送到事件轉發和其它Adobe產品。

1. 在 **[!UICONTROL 資料流]** 工作區，選擇您建立的屬性。

1. 選取「開發」、「生產」或「預備」環境。

   或者，要將資料發送到Adobe組織外的事件轉發環境，請選擇 **[!UICONTROL 切換到高級模式]** 然後貼上到ID中。 建立事件轉發屬性時提供ID。

1. 開啟必要工具並依需求設定。

   * Adobe Analytics 會要求您輸入報表套裝 ID。

   * Adobe Experience Platform的事件轉發需要屬性ID和環境ID。 這是事件轉發屬性的發佈路徑。

完成設定後，記下新屬性的環境 ID。

## 配置平台Web SDK擴展以將資料發送到以前建立的資料流

在 **[!UICONTROL 標籤]** 工作區，然後導航 **[!UICONTROL 擴展]** 並從目錄中選擇Experience PlatformWeb SDK擴展以配置和安裝它。

查看 [Web SDK擴展文檔](../../extensions/client/sdk/overview.md) 的子菜單。

## 建立標籤規則以將資料發送到平台Web SDK

在上述設定到位後，生成資料定義、規則等，這些使用事件轉發和標籤，但只需從頁面中發出一個請求。

使用平台Web SDK擴展和「發送事件」操作類型建立頁面載入規則：

1. 開啟 **[!UICONTROL 規則]** ，然後選擇 **[!UICONTROL 建立新規則]**。

1. 為規則命名。

1. 選擇 **[!UICONTROL 添加事件]**。

1. 選擇擴充功能及該擴充功能提供的任一事件類型以新增事件，然後設定事件相關設定，例如，選擇 **[!UICONTROL 核心 — 已載入窗口]**。

1. 使用 Platform Web SDK 擴充功能新增動作。選擇 **[!UICONTROL 發送事件]** 從 **[!UICONTROL 操作類型]** 清單中，選擇所需的「實例」（先前配置的「合金」實例），然後選擇要添加到「合金」命中的「XDM資料」塊中的資料元素。

1. 將其餘設定保留為本示例的預設設定，然後選擇 **[!UICONTROL 保存]**。

再舉個例子：您可能可以建立一項規則，在使用者將游標停留在指定按鈕上時，將資料層傳送至邊緣。

## 摘要

現在，您可以建立事件轉發規則，將資料轉發到非Adobe目標。

* 體驗資料模型架構（請注意您給它的名稱。）
* 事件轉發屬性（跟蹤屬性ID和環境ID）
* 資料流（注意環境ID，不要與事件轉發的環境ID混淆。）
* 標籤屬性
