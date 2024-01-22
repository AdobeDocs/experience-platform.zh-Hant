---
title: 對目的地啟用潛在客戶對象
type: Tutorial
description: 瞭解如何對目的地啟用潛在客戶對象
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 16%

---

# 啟用潛在客戶對象

>[!AVAILABILITY]
>
>已購買Real-Time CDP Prime和Ultimate套件的客戶可使用此功能。 如需詳細資訊，請聯絡您的Adobe代表。

本文會說明匯出所需的工作流程 [潛在客戶對象](/help/segmentation/ui/prospect-audience.md) 從Adobe Experience Platform前往您偏好的目的地。

## 支援的目的地 {#supported-destinations}

前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。 使用 **[!UICONTROL 資料型別]** 篩選並選取 **[!UICONTROL 潛在客戶]** 檢視支援啟動潛在客戶對象的目的地。 目前，匯出潛在客戶對象僅適用於雲端儲存目的地。

![支援潛在客戶對象的目的地。](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## 先決條件 {#prerequisites}

* 您必須先內嵌 [潛在客戶設定檔](/help/profile/ui/prospect-profile.md) 和建立 [潛在客戶對象](/help/segmentation/ui/prospect-audience.md) 才能啟用至下游目的地。
* 若要將潛在客戶對象啟用至目的地，您必須已成功連線至目的地。 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。 閱讀UI教學課程，位於 [連線到目的地](./connect-destination.md) 以取得詳細資訊。

### 必要權限 {#permissions}

若要啟用潛在客戶對象，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 啟用目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

為確保您擁有啟動潛在客戶對象的必要許可權，請瀏覽目的地目錄。 如果目的地有 **[!UICONTROL 啟動]** 控制項，則表示您擁有適當的許可權。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![反白顯示目錄控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. 選取 **[!UICONTROL 啟動]** 位於對應您要匯出資料集之目的地的卡片上。

>[!TIP]
>
>可匯出設定檔對象的目的地會在卡片的右上角顯示圖示，類似於下面醒目提示的目的地，或者，您可以使用資料型別篩選器來僅顯示可匯出潛在客戶對象的目的地，例如 [顯示在頁面較高的位置](#supported-destinations).

![可匯出醒目提示之設定檔對象的Amazon S3目標頁面。](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. 選取 **[!UICONTROL 資料型別潛在客戶]**，然後選取您要匯出資料集的目的地連線 **[!UICONTROL 下一個]**.

>[!TIP]
> 
>如果您想要設定新目的地以啟用潛在客戶對象，請選取「 」 **[!UICONTROL 設定新目的地]** 以觸發 [連線到目的地](/help/destinations/ui/connect-destination.md) 工作流程。

![強調具有潛在客戶控制項的目的地啟用工作流程。](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. 繼續下一節至 [選取您的設定檔對象](#select-profile-audiences) 以匯出。

## 選取您的潛在客戶對象 {#select-prospect-audiences}

使用潛在客戶對象名稱左側的核取方塊，選取您要匯出至目的地的對象，然後選取「 」 **[!UICONTROL 下一個]**. 請注意，此檢視只會顯示潛在客戶對象，不會顯示其他對象。

![資料集匯出工作流程顯示「選取對象」步驟，您可在此選取要匯出的潛在客戶對象。](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## 排程和後續步驟

如需匯出潛在客戶受眾的其餘啟動工作流程，請閱讀將資料啟動至檔案型目的地的教學課程。 繼續從 [排程對象匯出步驟](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>請注意，在排程步驟中，啟動潛在客戶對象的工作流程僅允許您 [匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). 不支援增量檔案匯出。

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* [使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* 使用 Real-Time CDP 的協力廠商資料支援，透過資料合作夥伴的潛在客戶設定檔來[擴大您的設定檔庫，並與其互動以獲取或接觸新客戶。](/help/rtcdp/partner-data/prospecting.md)
* [利用合作夥伴輔助識別，不需要使用者驗證或之前使用您的品牌的紀錄，即可在造訪期間提供個人化的現場體驗](/help/rtcdp/partner-data/onsite-personalization.md)。
