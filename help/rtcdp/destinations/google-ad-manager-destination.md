---
title: Google廣告管理員目標
seo-title: Google廣告管理員目標
description: 'Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。 '
seo-description: 'Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。 '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# Google廣告管理員目標

## 概述

Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。

## 目標規格

請注意Google廣告管理員目標專屬的下列詳細資訊：

* 您可以傳送下列身 [分](../../identity-service/namespaces.md) ，到Google Ad Manager目的地： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 在Google平台中以程式設計方式建立已啟用的觀眾。
* Adobe即時CDP目前不包含測量量度，以驗證啟動是否成功。 請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

>[!IMPORTANT]
>
>如果您想要使用Google Ad Manager建立您的第一個目標，而過去（使用Audience Manager或其他應用程式）未啟用 [Experience Cloud ID服務中的](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，您設定的ID同步化會轉存至Adobe即時CDP。

## 必要條件

### 允許清單

>[!NOTE]
>
>在Adobe Real-time CDP中設定您的第一個Google Ad Manager目標之前，允許清單是必填的。 請確定Google在建立目標之前已完成下列說明的允許清單程式。

在Adobe即時CDP中建立Google Ad Manager目標之前，您必須連絡Google,Adobe才能將其列入允許的資料提供者清單，而您的帳戶也必須新增至允許清單。 聯絡Google並提供下列資訊：

* **帳戶ID** : 這是Adobe與Google的帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** : 這是Adobe與Google的客戶帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **網路ID** : 這是您在Google廣告管理員的帳戶
* **對象連結ID** : 這是您在Google廣告管理員的帳戶
* 您的帳戶類型。 **DFP，由Google** 或 **AdX購買者提供**。

## 建立目標

1. 在「連 **[!UICONTROL 線>目的地]**」中，選取「Google廣告管理員」，然後選取「 **[!UICONTROL 建立目的地」]**。
   ![Connect Google Ad Manager目標](/help/rtcdp/destinations/assets/google-1-destination.png)

2. 在「建立目標」工作流程中，填入目 [!UICONTROL 標的「基本] 」資訊。 <br>
   ![基本資訊Google廣告管理員](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **[!UICONTROL 名稱]**: 填寫此目標的首選名稱。
* **[!UICONTROL 說明]**: 可選。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**: 根據您使用Google的帳戶，選取一個選項：
   * DoubleClick `DFP by Google` for Publishers的使用
   * 用 `AdX buyer` 於Google AdX
* **[!UICONTROL 帳戶ID]**: 使用Google填寫您的帳戶ID。 這可以是您的網路ID或對象連結ID。 通常，這是8位數的ID。

>[!NOTE]
>
>設定Google廣告管理員目標時，請與您的Google客戶經理或Adobe代表合作，以瞭解您擁有的帳戶類型。

## 啟用區段至Google廣告管理員

如需如何將區段啟用至Google廣告管理員的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。