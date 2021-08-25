---
keywords: 啟動目的地；啟動資料
title: Activation 總覽
type: Tutorial
seo-title: Activation overview
description: 了解如何將您在Adobe Experience Platform中擁有的對象資料啟用至各種類型的目的地。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---


# Activation 總覽

Adobe Experience Platform支援多種目的地。 受眾啟動工作流程會根據所支援的受眾資料類型和資料匯出頻率，因目的地而異。

## 啟動方法 {#activation-methods}

在您[設定您的目的地](connect-destination.md)後，您可以透過多種方式啟用對象區段：

### 從目的地目錄啟用對象

如需從目的地目錄啟用對象至您目的地的詳細資訊，請參閱下列指南：

* [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
* [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
* [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從[!UICONTROL Browse]頁面啟動對象

請依照下列步驟，從&#x200B;**[!UICONTROL Browse]**&#x200B;頁面將資料啟用至您的目的地。

1. 前往&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤。

   ![「瀏覽」頁簽](../assets/ui/activation-overview/browse-tab.png)

1. 找到您要用來啟用區段的目標連線，在[!UICONTROL Name]欄中選取三個點，然後選取&#x200B;**[!UICONTROL Activate區段]**。

   ![「啟用區段」按鈕](../assets/ui/activation-overview/activate-segments.png)

1. 根據選取的目的地，請依照下列文章中所述的步驟操作，從&#x200B;**[!UICONTROL 選取區段]**&#x200B;步驟開始，以完成啟動工作流程：

   * [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
   * [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
   * [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)

### 從區段詳細資訊頁面啟用對象 {#activate-segment-details}

您可以從區段詳細資訊頁面啟用區段至目的地。 如需詳細資訊，請參閱[區段詳細資料](../../segmentation/ui/overview.md#segment-details) 。

視選取的目的地而定，請依照下列文章中所述的步驟完成啟動工作流程：

* [對串流區段匯出目的地啟用受眾資料](activate-segment-streaming-destinations.md)
* [對串流設定檔匯出目的地啟用受眾資料](activate-streaming-profile-destinations.md)
* [啟用受眾資料以批次設定檔匯出目的地](activate-batch-profile-destinations.md)