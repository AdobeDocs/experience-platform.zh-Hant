---
keywords: Experience Platform；排程模型；Data Science Workspace；熱門主題；排程計分；排程訓練
solution: Experience Platform
title: 在資料科學工作區UI中排程模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分程式有助於透過追蹤資料中的模式，持續維持和改善服務的效率。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# 在Data Science Workspace UI中排程模型

Adobe Experience Platform [!DNL Data Science Workspace]可讓您在機器學習服務上設定計畫的分數和訓練執行。 自動化培訓和計分程式有助於透過追蹤資料中的模式，持續維持和改善服務的效率。

本教學課程將逐步介紹如何在現有服務上透過[!UICONTROL 服務庫]配置培訓與計分排程。 它分為以下幾個主要部分：

- [設定排程計分](#configure-scheduled-scoring)
- [設定計畫培訓](#configure-scheduled-training)

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

本教學課程需要現有服務。 如果您沒有可存取的服務可供使用，則可遵循UI](./publish-model-service-ui.md)教學課程中的「將模型發佈為服務」來建立此服務。[

## 配置計畫計分{#configure-scheduled-scoring}

模型計分可以配置為以計畫為基礎的自動化流程。 建立服務後，您可依照下列步驟設定並套用計分排程：

1. 在Adobe Experience Platform中，按一下左側導覽欄中的&#x200B;**[!UICONTROL Services]**&#x200B;標籤以存取&#x200B;**[!DNL Service Gallery]**。 尋找您要排程計分執行的服務，然後按一下&#x200B;**[!UICONTROL Open]**&#x200B;以檢視其&#x200B;**Overview**頁面。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 「概述」頁面會顯示服務的計分資訊。 按一下&#x200B;**[!UICONTROL 更新計畫]**連結以配置計分計畫。
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 為計分排程設定頻率、開始日期、結束日期、輸入資料集和輸出資料集。 對配置滿意後，按一下&#x200B;**[!UICONTROL 建立]**以更新服務的計分計畫。
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 您更新的計分排程會顯示在服務的&#x200B;**概述**頁面中。
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 配置計畫培訓{#configure-scheduled-training}

設定在服務上執行的計畫訓練可確保機器學習模型已更新為最新的資料模式。 每當排程的訓練執行完成時，產生的訓練模型就會用來為服務提供動力，直到下次排程的訓練執行為止。

建立服務後，您可依照下列步驟設定並套用培訓計畫：

1. 在Adobe Experience Platform中，按一下左側導覽欄中的&#x200B;**[!UICONTROL 服務]**&#x200B;標籤，以存取&#x200B;**[!UICONTROL 服務收藏館]**。 尋找您要排程培訓執行的服務，然後按一下&#x200B;**[!UICONTROL Open]**&#x200B;以檢視其&#x200B;**Overview**頁面。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. 「概述」頁面會顯示服務的訓練資訊。 按一下&#x200B;**[!UICONTROL 更新計畫]**連結以配置培訓計畫。
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 設定培訓計畫使用的頻率、開始日期、結束日期和輸入資料集。 對配置感到滿意後，按一下&#x200B;**[!UICONTROL 建立]**以更新服務的培訓計畫。
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 您更新的培訓計畫會顯示在服務的&#x200B;**概述**頁面中。
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 後續步驟

在本教學課程中，您已成功排程在服務上執行自動化訓練和計分，並完成[!DNL Data Science Workspace]教學課程UI工作流程。 如果您尚未這麼做，請考慮[重新啟動教學課程](./create-retails-sales-dataset.md)，並遵循API工作流程來建立、訓練、分數和發佈模型。
