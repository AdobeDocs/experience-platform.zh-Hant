---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics;schedule scoring;schedule training
solution: Experience Platform
title: 排程模型(UI)
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分程式有助於透過追蹤資料中的模式，持續維持和改善服務的效率。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# 排程模型(UI)

Adobe Experience Platform可 [!DNL Data Science Workspace] 讓您在機器學習服務上設定計畫的分數和訓練執行。 自動化培訓和計分程式有助於透過追蹤資料中的模式，持續維持和改善服務的效率。

本教學課程將逐步介紹如何在現有服務上透過服務收藏館設定培訓與計 **[!UICONTROL 分排程]**。 它分為以下幾個主要部分：

- [設定排程計分](#configure-scheduled-scoring)
- [設定計畫培訓](#configure-scheduled-training)

## 快速入門

若要完成本教學課程，您必須擁有存取權 [!DNL Experience Platform]。 如果您無權存取中的IMS組織，請先與您的系 [!DNL Experience Platform]統管理員聯絡，然後再繼續。

本教學課程需要現有服務。 如果您沒有可存取的服務可供使用，則可遵循UI教學課程中的「將模型發佈為服務」來建立此服務 [](./publish-model-service-ui.md) 。

## 設定排程計分 {#configure-scheduled-scoring}

模型計分可以配置為以計畫為基礎的自動化流程。 建立服務後，您可依照下列步驟設定並套用計分排程：

1. 在Adobe Experience Platform中，按一下左 **[!UICONTROL 側導覽欄]** 中的「服務」標籤以存取 *[!DNL Service Gallery]*。 尋找您要排程計分的服務，然後按一下「開 **[!UICONTROL 啟]** 」以檢視其 *概述頁面* 。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 「概述」頁面會顯示服務的計分資訊。 按一下「 **[!UICONTROL 更新排程]** 」連結，以設定計分排程。
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 為計分排程設定頻率、開始日期、結束日期、輸入資料集和輸出資料集。 一旦您對設定滿意後，按一下「 **[!UICONTROL 建立]** 」以更新服務的計分排程。
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 您更新的計分排程會顯示在「服務」的「概述 *」頁* 。
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 設定計畫培訓 {#configure-scheduled-training}

設定在服務上執行的計畫訓練可確保機器學習模型已更新為最新的資料模式。 每當排程的訓練執行完成時，產生的訓練模型就會用來為服務提供動力，直到下次排程的訓練執行為止。

建立服務後，您可依照下列步驟設定並套用培訓計畫：

1. 在Adobe Experience Platform中，按一下左側導 **[!UICONTROL 覽欄中的]** 「服務」標籤，以存取「服 **[!UICONTROL 務收藏館」]**。 尋找您要排程培訓執行的服務，然後按一下「開 **[!UICONTROL 啟]** 」以檢視其 *概述頁面* 。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 「概述」頁面會顯示服務的訓練資訊。 按一下「 **[!UICONTROL 更新計畫]** 」連結以設定培訓計畫。
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 設定培訓計畫使用的頻率、開始日期、結束日期和輸入資料集。 一旦您對設定滿意後，按一下「 **[!UICONTROL 建立]** 」以更新「服務」的培訓排程。
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 您更新的培訓計畫會顯示在「服務」的「概述 *」頁* 。
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 後續步驟

透過本教學課程，您已成功排程在服務上執行自動化訓練和計分，並完成教學課程UI [!DNL Data Science Workspace] 工作流程。 如果您尚未完成，請考慮重 [新啟動教學課程](./create-retails-sales-dataset.md) ，並遵循API工作流程來建立、訓練、計分和發佈模型。
