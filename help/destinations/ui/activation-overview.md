---
keywords: 啟用目的地；啟用資料
title: Activation 總覽
type: Tutorial
description: 瞭解如何在Adobe Experience Platform中將您的對象啟動至各種型別的目的地。
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: afcb5f80edaa4d68ba167123feb2ba9060469243
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Activation 總覽

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

Adobe Experience Platform支援廣泛的目的地。 受眾啟用工作流程會因支援的受眾資料型別以及資料匯出頻率而因目的地而異。

## 啟用方法 {#activation-methods}

在您之後 [設定您的目的地](connect-destination.md)，您可用多種方式啟用對象：

### 從目的地目錄啟用對象

如需從目的地目錄啟用對象至您的目的地的詳細資訊，請參閱下列指南：

* [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
* [啟用受眾資料至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
* [啟用對象資料至批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從啟用對象 [!UICONTROL 瀏覽] 頁面

請依照下列步驟，從「 」啟用您目的地的資料 **[!UICONTROL 瀏覽]** 頁面。

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 瀏覽]** 標籤。

   ![瀏覽標籤](../assets/ui/activation-overview/browse-tab.png)

1. 尋找要用來啟用區段的目的地連線，選取 [!UICONTROL 名稱] 欄，然後選取 **[!UICONTROL 啟用對象]**.

   ![啟用受眾按鈕](../assets/ui/activation-overview/activate-segments.png)

1. 請根據所選目的地，遵循下列文章中所述的步驟，從 **[!UICONTROL 選取區段]** 步驟，若要完成啟動工作流程：

   * [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
   * [啟用受眾資料至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
   * [啟用對象資料至批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從對象詳細資訊頁面啟用對象 {#activate-audience-details}

您可以從對象詳細資訊頁面啟用目的地的對象。 另請參閱 [對象詳細資料](../../segmentation/ui/overview.md#audience-details) 以取得詳細資訊。

視選取的目標而定，請遵循下列文章中所述的步驟以完成啟動工作流程：

* [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
* [啟用受眾資料至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
* [啟用對象資料至批次設定檔匯出目的地](activate-batch-profile-destinations.md)
