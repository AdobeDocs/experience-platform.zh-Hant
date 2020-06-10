---
title: Google Display & Video 360 Destination
seo-title: Google Display & Video 360 Destination
description: Display & Video 360（先前稱為DoubleClick競標管理器）是一種工具，用於在顯示、視訊和行動庫存來源中執行重新鎖定目標及受眾目標數位促銷活動。
seo-description: 'Display & Video 360（先前稱為DoubleClick競標管理器）是一種工具，用於在顯示、視訊和行動庫存來源中執行重新鎖定目標及受眾目標數位促銷活動。 '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# Google Display &amp; Video 360 Destination

## 概述

Display &amp; Video 360（舊稱DoubleClick競標管理器）是一種工具，可用來在顯示、視訊和行動庫存來源中執行重新鎖定目標及受眾目標數位促銷活動。

## 目標規格

請注意Google Display &amp; Video 360目標專屬的下列詳細資訊：

* 您可以傳送下列 [身分](../../identity-service/namespaces.md) ，到Google Display &amp; Video 360目的地： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 在Google平台中以程式設計方式建立已啟用的觀眾。
* Adobe即時CDP目前不包含測量量度，以驗證啟動是否成功。 請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

>[!IMPORTANT]
>
>如果您想要使用Google Display &amp; Video 360建立您的第一個目的地，而且過去（使用Adobe Audience Manager或其他應用程式）未啟用 [Experience Cloud ID服務中的](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，您設定的ID同步化會轉存至Adobe即時CDP。

## 必要條件

### 允許清單

>[!NOTE]
>
>在Adobe Real-time CDP中設定您的第一個Google Display &amp; Video 360目標之前，允許清單是必填的。 請確定Google在建立目標之前已完成下列說明的允許清單程式。

在Adobe即時CDP中建立Google Display &amp; Video 360目標之前，您必須聯絡Google，要求Adobe將Adobe加入允許的資料提供者清單中，並將您的帳戶加入允許清單中。 聯絡Google並提供下列資訊：

* **帳戶ID** : 這是Adobe與Google的帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** : 這是Adobe與Google的客戶帳戶ID。 請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **您的帳戶類型**: 用 **[!DNL Invite advertiser]** 於允許觀眾僅分享到您Display &amp; Video 360帳戶中的特定品牌，或 **[!DNL Invite partner]** 用於允許觀眾分享到您Display &amp; Video 360帳戶中的所有品牌。

## 建立目標

1. 在「連 **[!UICONTROL 線>目的地]**」中，選取「Google顯示與視訊360」，然後選取「 **[!UICONTROL 建立目的地」]**。
   ![Connect Google Display &amp; Video 360目標](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. 在「建立目標」工作流程中，填入目 [!UICONTROL 標的「基本] 」資訊。 <br>
   ![基本資訊Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **[!UICONTROL 名稱]**: 填寫此目標的首選名稱。
* **[!UICONTROL 說明]**: 可選。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**: 根據您使用Google的帳戶，選取一個選項：
   * 使用 `Invite Advertiser` 可讓觀眾僅分享至您「顯示與視訊360」帳戶中的特定品牌。
   * 使用 `Invite Partner` 可讓觀眾分享至您「顯示與視訊360」帳戶中的所有品牌。
* **[!UICONTROL 帳戶ID]**: 使用Google填 **[!DNL Invite partner]** 寫您 **[!DNL Invite advertiser]** 或帳戶ID。 通常為6或7位數的ID。

>[!NOTE]
>
>設定Google Display &amp; Video 360目標時，請與您的Google帳戶管理員或Adobe代表合作，以瞭解您擁有的帳戶類型。

## 啟用區段至Google Display &amp; Video 360

如需如何啟用區段至Google Display &amp; Video 360的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。