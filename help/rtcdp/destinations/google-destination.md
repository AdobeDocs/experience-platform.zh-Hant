---
title: Google目的地
seo-title: Google目的地
description: Adobe Real-time CDP與Google整合，讓您能夠在DV360、Google Ad Manager、Google AdWords和Google AdX中執行並啟用您的資料。
seo-description: Adobe Real-time CDP與Google整合，讓您能夠在DV360、Google Ad Manager、Google AdWords和Google AdX中執行並啟用您的資料。
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google目的地

## 概述

Adobe Real-time CDP與Google整合，讓您能夠在DV360、Google Ad Manager、Google AdWords Display和Google AdX上執行並啟動您的資料。

## 目標規格

請注意Google目標專屬的下列詳細資訊：

* 您可以傳送下列身 [分](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) ，到Google目的地：Google **Cookie ID、IDFA、GAID**。
* 在Google平台中以程式設計方式建立已啟用的觀眾。
* Adobe即時CDP目前不包含測量量度，以驗證啟動是否成功。 請參閱Google中的觀眾計數，以驗證整合併瞭解資料下拉。

## 必要條件

### 白名單

在Adobe Real-time CDP中連接Google目標之前，您必須聯絡Google，要求將您的帳戶列入白名單。 聯絡Google並提供下列資訊：

* **帳戶ID** :這是Adobe與Google的帳戶ID。 請聯絡Adobe支援以取得此ID。
* **客戶ID** :這是Adobe與Google的客戶帳戶ID。 請聯絡Adobe支援以取得此ID。
* **合作夥伴ID** :這是你與谷歌的三位數合作夥伴ID;
* **網路ID** :這是你在谷歌的賬戶；
* **對象連結ID** :這是你在谷歌的賬戶；
* 您的帳戶類型。 這可以是邀請廣告商 **、邀請**&#x200B;合作夥伴 **、** DFP **、AdX********** Words、AdXWords。


## 連接目標

1. 在「連 **[!UICONTROL 線>目的地]**」中，選取「Google」，然後選取「 **[!UICONTROL 建立目的地」]**。
   ![Connect Google目標](/help/rtcdp/destinations/assets/google-destination.png)

2. 在「連接目標」嚮導中，填寫目標的基本資訊。
   ![基本資訊Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **名稱**:填寫此目標的首選名稱。
* **說明**:可選。 例如，您可以提及您使用此目的地的促銷活動。
* **帳戶類型**:根據您使用Google的帳戶，選取一個選項：
   * Google `Invite advertiser` DV360的使用
   * Google `Invite partner` DV360的使用
   * 用於 `DFP by Google` Google廣告管理員
   * 用於 `AdWords` Google AdWords顯示
   * 用 `AdX buyer` 於Google AdX
* **帳戶ID**:使用Google填寫您的帳戶ID。

>[!NOTE]
>
>設定Google目標時，請與您的Google帳戶管理員或Adobe代表合作，以瞭解您的帳戶屬於何種產品類型。 若是Google DV360，請詢問您的Google帳戶管理員，您的帳戶屬於哪一種產品類型。 

## 啟用區段至Google

如需如何將區段啟用至Google的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。