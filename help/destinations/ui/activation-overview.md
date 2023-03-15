---
keywords: 啟動目的地；啟動資料
title: Activation 總覽
type: Tutorial
description: 了解如何將您在Adobe Experience Platform中擁有的對象資料啟用至各種類型的目的地。
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Activation 總覽

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

Adobe Experience Platform支援多種目的地。 受眾啟動工作流程會根據所支援的受眾資料類型和資料匯出頻率，因目的地而異。

## 啟動方法 {#activation-methods}

在 [設定您的目的地](connect-destination.md)，您可以透過多種方式啟用對象區段：

### 從目的地目錄啟用對象

如需從目的地目錄啟用對象至您目的地的詳細資訊，請參閱下列指南：

* [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
* [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
* [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從 [!UICONTROL 瀏覽] 頁面

請依照下列步驟，從 **[!UICONTROL 瀏覽]** 頁面。

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 瀏覽]** 標籤。

   ![「瀏覽」頁簽](../assets/ui/activation-overview/browse-tab.png)

1. 尋找您要用來啟動區段的目的地連線，選取 [!UICONTROL 名稱] 欄，然後選取 **[!UICONTROL 啟用區段]**.

   ![「啟用區段」按鈕](../assets/ui/activation-overview/activate-segments.png)

1. 請依據選取的目的地，遵循下列文章中所述的步驟，從 **[!UICONTROL 選取區段]** 步驟，以完成啟動工作流程：

   * [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
   * [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
   * [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從區段詳細資訊頁面啟用對象 {#activate-segment-details}

您可以從區段詳細資訊頁面啟用區段至目的地。 請參閱 [區段詳細資料](../../segmentation/ui/overview.md#segment-details) 以取得更多資訊。

視選取的目的地而定，請依照下列文章中所述的步驟完成啟動工作流程：

* [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
* [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
* [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)
