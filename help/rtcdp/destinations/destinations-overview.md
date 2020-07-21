---
title: 目的地概述
seo-title: 目的地概述
description: 目標是與目標平台預先建立的整合，可讓即時客戶資料平台順暢地啟動資料。 您可以使用Adobe即時客戶資料平台中的「目標」來啟用您已知和未知的跨通道行銷宣傳、電子郵件宣傳、目標廣告及許多其他使用案例資料。
seo-description: 目標是與目標平台預先建立的整合，可讓即時客戶資料平台順暢地啟動資料。 您可以使用Adobe即時客戶資料平台中的「目標」來啟用您已知和未知的跨通道行銷宣傳、電子郵件宣傳、目標廣告及許多其他使用案例資料。
translation-type: tm+mt
source-git-commit: 7aa15772003cce1dfc7c3636048bce9a35bf8197
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# [!DNL Destinations]概述{#overview}

![目標概述橫幅](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**[!DNL Destinations]** 是與目標平台預先建立的整合，可讓即時客戶資料平台順暢地啟動資料。 您可以使用目的地來啟用跨通道行銷宣傳、電子郵件宣傳、目標廣告和許多其他使用案例的已知和未知資料。

## 目標和來源 {#destinations-and-sources}

即時CDP的核心功能之一是接收第一方資料並根據業務需要激活它。 使用源將資料嵌入即時CDP中，並使用目標從即時CDP中導出資料。

## 目標步驟 {#steps}

* 從即時 [CDP中所有可用目標的自助](/help/rtcdp/destinations/destinations-catalog.md) -服務目錄中進行選擇。
* 使用 **[!UICONTROL 目的地]** 啟動 [](/help/rtcdp/destinations/activate-destinations.md) ，並傳送個人檔案或區段至行銷自動化平台、數位廣告平台等。
* 定期排程匯出至您偏好目的地的資料。

## 控制項 {#controls}

「目標」工作區 [中的控制項](/help/rtcdp/destinations/destinations-workspace.md) ，可讓您：

* 瀏覽可啟動資料的目標平台目錄；
* 建立、編輯、啟用和停用目錄中目的地的資料流；
* 在儲存位置建立帳戶或將即時CDP連結到目標平台中的帳戶；
* 選擇哪些區段應啟動至目標；
* 在啟用 [區段至電子郵件行銷目標時](../../xdm/home.md) ，選取要匯出的體驗資料模型(XDM)欄位。

## Destination types and categories {#types-and-categories}

如需詳細資訊，請參 [閱目標類型和類別概觀](/help/rtcdp/destinations/destination-types.md)。

## 目標與存取控制 {#access-controls}

即時CDP的目標功能可與Adobe Experience Platform存取控制權限搭配使用。 視使用者的權限層級而定，您可以檢視、管理和啟用目標。 如需個別權限的詳細資訊，請參 [閱Adobe Experience Platform中的存取控制](../../access-control/home.md) ，並向下捲動至頁面底部。

如需存取控制的詳細資訊，請參閱存取控 [制使用指南](../../access-control/ui/overview.md)。

## [!DNL Data Governance] 啟用資料至目的地的限制 {#data-governance}

通過以下方式對即時CDP目標實施資料治理：

* *您可在建立目標* ，工作流程中選擇的行銷使用案例；
* *資料使用原則* ，可限制包含特定使用標籤的資料被啟動至具有特定行銷使用案例的目的地。

有關行 [!DNL Data Governance] 銷使用案例和解決資料原則違規 [的詳細資訊](/help/rtcdp/privacy/data-governance-overview.md#destinations) ，請 [參閱即時CDP檔案](/help/rtcdp/privacy/data-governance-overview.md#enforcement)。

有關在建立目標工作流中選擇市場營銷使用案例的詳細資訊，請參閱以下有關即時CDP中不同目標類型的頁：

* [廣告目的地- Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [廣告目的地- Google Ads](/help/rtcdp/destinations/google-ads-destination.md)
* [廣告目的地- Google Display &amp; Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [雲端儲存空間目標](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [電子郵件行銷目標](/help/rtcdp/destinations/email-marketing-destinations.md)
* [社交網路目的地](/help/rtcdp/destinations/social-network-destinations-workflow.md)

如需區段啟動工作流程中違反資料原則的詳細資訊，請參閱「啟用設定檔和區段至 [目的地」中的步驟7](/help/rtcdp/destinations/activate-destinations.md)。