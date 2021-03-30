---
keywords: Experience Platform；排程模型；資料科學工作區；熱門主題；排程計分；排程培訓
solution: Experience Platform
title: 在資料科學工作區UI中排程模型
topic: 教學課程
type: 教學課程
description: Adobe Experience Platform資料科學工作區可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分程式有助於透過追蹤資料中的模式，持續維持和改善服務的效率。
translation-type: tm+mt
source-git-commit: 8f5b7018a52d4c5860e03cec3108435ede8815f1
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 在Data Science Workspace UI中排程模型

Adobe Experience Platform[!DNL Data Science Workspace]可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分流程有助於透過追蹤資料中的模式，持續維持並改善服務的效率。

本教學課程將逐步介紹如何在現有服務上透過[!UICONTROL Service Gallery]設定訓練和計分排程的步驟。 它分為以下幾個主要部分：

- [設定排程計分](#configure-scheduled-scoring)
- [設定計畫培訓](#configure-scheduled-training)

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

本教學課程需要現有的服務。 如果您沒有可存取的服務可使用，則可遵循[以服務形式發佈模型的教學課程來建立。](./publish-model-service-ui.md)

## 配置計畫計分{#configure-scheduled-scoring}

模型計分可以配置為以計畫為基礎的自動化流程。 在建立服務後，您可依照下列步驟來設定並套用計分排程：

在Adobe Experience Platform，選擇位於左側導航列中的&#x200B;**[!UICONTROL Services]**&#x200B;頁籤以訪問&#x200B;**[!DNL Service Gallery]**。 查找要計畫計分運行的服務，並選擇&#x200B;**[!UICONTROL Open]**&#x200B;以查看其&#x200B;**[!UICONTROL Overview]**&#x200B;頁。

![](../images/models-recipes/schedule/select_service.png)

「概述」頁面會顯示服務的計分資訊。 選擇&#x200B;**[!UICONTROL Update Schedule]**&#x200B;連結以設定計分排程。

![](../images/models-recipes/schedule/update_scoring.png)

為計分排程設定頻率、開始日期、結束日期、輸入資料集和輸出資料集。 對配置滿意後，選擇&#x200B;**[!UICONTROL Create]**&#x200B;以更新服務的計分計畫。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

您更新的計分排程會顯示在服務的&#x200B;**[!UICONTROL Overview]**&#x200B;頁面中。

![](../images/models-recipes/schedule/scoring_set.png)

## 配置計畫培訓{#configure-scheduled-training}

在服務上設定計畫的訓練執行可確保機器學習模型更新為最新的資料模式。 每當排程的訓練執行完成時，就會使用產生的訓練模型來為服務提供動力，直到下次排程的訓練執行為止。

建立服務後，您可依照下列步驟來設定和套用培訓計畫：

在Adobe Experience Platform，選擇位於左側導航列中的&#x200B;**[!UICONTROL Services]**&#x200B;頁籤以訪問&#x200B;**[!UICONTROL Service Gallery]**。 尋找您要排程培訓執行的服務，並選取&#x200B;**[!UICONTROL Open]**&#x200B;以檢視其&#x200B;**[!UICONTROL Overview]**&#x200B;頁面。

![](../images/models-recipes/schedule/select_service.png)

「概述」頁面會顯示服務的訓練資訊。 選擇&#x200B;**[!UICONTROL Update Schedule]**&#x200B;連結，以設定培訓排程。

![](../images/models-recipes/schedule/update_training.png)

設定培訓計畫使用的頻率、開始日期、結束日期和輸入資料集。 對配置滿意後，選擇&#x200B;**[!UICONTROL Create]**&#x200B;以更新服務的培訓計畫。

![](../images/models-recipes/schedule/set_training_schedule.png)

您更新的培訓計畫會顯示在服務的&#x200B;**[!UICONTROL Overview]**&#x200B;頁面中。

![](../images/models-recipes/schedule/training_set.png)

## 後續步驟

在本教學課程中，您已成功排程在服務上執行自動化訓練和計分，並完成[!DNL Data Science Workspace]教學課程UI工作流程。 如果您尚未這麼做，請考慮[重新啟動教學課程](./create-retails-sales-dataset.md)，並遵循API工作流程來建立、訓練、分數和發佈模型。
