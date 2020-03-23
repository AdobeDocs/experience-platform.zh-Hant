---
title: Google AdsDestination
seo-title: Google廣告目的地
description: Google Ads（先前稱為Google AdWords）是線上廣告服務，可讓企業透過文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示，按點擊付費廣告。
seo-description: Google Ads（先前稱為Google AdWords）是線上廣告服務，可讓企業透過文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示，按點擊付費廣告。
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Google廣告目的地

## 概述

Google Ads（先前稱為Google AdWords）是線上廣告服務，可讓企業透過文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示，按點擊付費廣告。

## 目標規格

請注意Google Ads目標專屬的下列詳細資訊：

* 您可以傳送下列身 [分](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) ，到Google Ads目的地：Google **Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 在Google平台中以程式設計方式建立已啟用的觀眾。
* Adobe即時CDP目前不包含測量量度，以驗證啟動是否成功。 請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

>[!IMPORTANT]
>
>如果您想要使用Google Ads建立您的第一個目標，而過去（使用Audience Manager或其他應用程式）未啟用 [Experience Cloud ID服務中的](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，您設定的ID同步化會轉存至Adobe即時CDP。

## 必要條件

### 現有Google Ads帳戶

Google已暫停與協力廠商的任何新Google Ads整合。 您必須已與Google Ads整合，才能執行下一節的白名單步驟，並在Adobe即時CDP中建立Google Ads目標。

### 白名單

>[!NOTE]
>
>在Adobe即時CDP中設定您的第一個Google Ads目標之前，必須填入白名單。 在建立目標之前，請確定Google已完成下列說明的白名單程式。

在Adobe即時CDP中建立Google Ads目標之前，您必須連絡Google，要求Adobe以資料提供者的身分加入白名單，而您的帳戶必須加入白名單。 聯絡Google並提供下列資訊：

* **帳戶ID** :這是Adobe與Google的帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** :這是Adobe與Google的客戶帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* 您的帳戶類型： **AdWords**
* **Google AdWords ID** :這是您使用Google的ID。 ID格式通常為123-456-7890。

## 建立目標

1. 在中 **[!UICONTROL Connections > Destinations]**，選取「Google廣告」，然後選取 **[!UICONTROL Create destination]**。
   ![Connect Google Ads目的地](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 在「建立目標」嚮導中，填寫目標的基本資訊。
   ![基本資訊Google廣告](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **名稱**:填寫此目標的首選名稱。
* **說明**:可選。 例如，您可以提及您使用此目的地的促銷活動。
* **帳戶類型**:AdWords是唯一可用的選項。
* **帳戶ID**:使用Google廣告填寫您的帳戶ID。 ID格式通常為123-456-7890。

## 啟用區段至Google廣告

如需如何將區段啟用至Google廣告的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。

