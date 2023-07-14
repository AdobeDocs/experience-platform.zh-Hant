---
keywords: 啟用目的地；啟用資料
title: Activation 總覽
type: Tutorial
description: 瞭解如何針對各種型別的目的地啟用您在Adobe Experience Platform中的對象。
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 1%

---

# Activation 總覽

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

Adobe Experience Platform支援廣泛的目的地。 受眾啟用工作流程因目標而異，取決於其支援的受眾資料型別，以及資料匯出的頻率。

## 啟用方法 {#activation-methods}

在您之後 [設定您的目的地](connect-destination.md)，您可用多種方式啟用對象：

### 從目的地目錄啟用對象

如需從目的地目錄啟用對象至您的目的地的詳細資訊，請參閱下列指南：

* [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
* [將受眾資料啟用至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
* [啟用對象資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從啟動對象 [!UICONTROL 瀏覽] 頁面

請依照下列步驟，從「 」啟用您目的地的資料 **[!UICONTROL 瀏覽]** 頁面。

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 瀏覽]** 標籤。

   ![瀏覽標籤](../assets/ui/activation-overview/browse-tab.png)

1. 尋找您要用來啟用區段的目的地連線，選取 [!UICONTROL 名稱] 欄，然後選取 **[!UICONTROL 啟用對象]**.

   ![啟用受眾按鈕](../assets/ui/activation-overview/activate-segments.png)

1. 根據所選目的地，請遵循以下文章中所述的步驟，從 **[!UICONTROL 選取區段]** 步驟，完成啟動工作流程：

   * [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
   * [將受眾資料啟用至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
   * [啟用對象資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從audiencedetails頁面啟用對象 {#activate-segment-details}

您可以從audiencedetails頁面啟用目的地的對象。 另請參閱 [區段詳細資料](../../segmentation/ui/overview.md#segment-details) 以取得詳細資訊。

根據選取的目的地，請依照下列文章中所述的步驟完成啟動工作流程：

* [啟用受眾資料至串流受眾匯出目的地](activate-segment-streaming-destinations.md)
* [將受眾資料啟用至串流設定檔匯出目的地](activate-streaming-profile-destinations.md)
* [啟用對象資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)
