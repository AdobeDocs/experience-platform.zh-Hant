---
title: 資料流組態覆寫設定
description: 當符合某些條件時，修改組態設定。
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# 資料流組態覆寫設定

資料流覆寫可讓您為資料流定義其他設定，這些設定會透過網頁SDK傳遞到Edge Network。 此功能可協助您有條件地觸發不同的資料流行為，而不需要建立新的資料流或修改現有的設定。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Datastream configuration overrides]**&#x200B;區段。

資料流設定覆寫的流程包含兩個步驟：

1. 首先，當[在資料流UI中設定資料流](/help/datastreams/configure.md)時，您必須定義資料流設定覆寫。 請參閱資料串流檔案中的[資料串流設定覆寫](/help/datastreams/overrides.md)，以取得如何設定覆寫的指示。
1. 在資料串流UI中設定資料串流覆寫後，您可以設定標籤擴充功能。

資料流覆寫必須根據環境進行設定。 開發、測試和生產環境都有不同的覆寫。 您可以在任何所需環境之間複製覆寫設定：

![影像顯示使用網頁SDK標籤延伸功能頁面的Datastream設定覆寫。](../assets/datastream-overrides.png)

預設會停用資料流設定覆寫。 預設會選取&#x200B;**[!UICONTROL Match datastream configuration]**&#x200B;選項。

![顯示資料流設定的Web SDK標籤延伸使用者介面會覆寫預設設定。](../assets/datastream-override-default.png)

若要在標籤延伸中啟用資料流覆寫，請從下拉式功能表中選取&#x200B;**[!UICONTROL Enabled]**。

![顯示資料流組態覆寫[已啟用]設定的Web SDK標籤延伸使用者介面。](../assets/datastream-override-enabled.png)

啟用資料流設定覆寫後，您可以為每個服務設定覆寫，如下所述。 這些資料流覆寫設定會覆寫所選環境的任何伺服器端資料流設定和規則。

## Adobe Analytics

覆寫傳送至Adobe Analytics服務的資料路由。

![顯示Adobe Analytics資料流覆寫設定的Web SDK標籤擴充功能UI影像。](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：啟用或停用資料路由傳送至Adobe Analytics。
* **[!UICONTROL Report suites]**： Adobe Analytics中目標報表套裝的ID。 該值必須是來自您的資料流設定的預先設定覆寫報告套裝（或以逗號分隔的報告套裝清單）。 此設定會覆寫主要報表套裝。
* **[!UICONTROL Add Report Suite]**：選取此選項以新增其他報表套裝。

## Adobe Audience Manager

覆寫傳至Adobe Audience Manager的資料路由。

![顯示Adobe Audience Manager資料流覆寫設定的Web SDK標籤擴充功能UI影像。](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：啟用或停用資料路由傳送至Adobe Audience Manager。
* **[!UICONTROL Third-party ID sync container]**： Audience Manager中目的地協力廠商ID同步容器的識別碼。 值必須是來自資料流設定的預先設定次要容器，並覆寫主要容器。

## Adobe Experience Platform

覆寫傳至Adobe Experience Platform的資料路由。

![顯示Adobe Experience Platform資料流覆寫設定的Web SDK標籤擴充功能UI影像。](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：啟用或停用資料路由傳送至Adobe Experience Platform。
* **[!UICONTROL Event dataset]**： Adobe Experience Platform中目的地事件資料集的識別碼。 該值必須是來自您的資料流設定的預先設定次要資料集。
* **[!UICONTROL Offer Decisioning]**：啟用或停用到[!DNL Offer Decisioning]服務的資料路由。
* **[!UICONTROL Edge Segmentation]**：啟用或停用到[!DNL Edge Segmentation]服務的資料路由。
* **[!UICONTROL Personalization Destinations]**：啟用或停用個人化目的地的資料路由。
* **[!UICONTROL Adobe Journey Optimizer]**：啟用或停用對[!DNL Adobe Journey Optimizer]的資料路由。

## Adobe伺服器端事件轉送

覆寫路由傳送至Adobe伺服器端事件轉送服務的資料。

![顯示Adobe伺服器端事件轉送資料流覆寫設定的Web SDK標籤擴充功能UI影像。](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：啟用或停用資料路由傳送至Adobe伺服器端事件轉送服務。

## Adobe Target {#target}

覆寫傳至Adobe Target的資料路由。

![顯示Adobe Target資料流覆寫設定的Web SDK標籤擴充功能UI影像。](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：啟用或停用資料路由傳送至Adobe Target。
