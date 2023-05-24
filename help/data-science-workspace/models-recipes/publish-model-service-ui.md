---
keywords: Experience Platform；發佈模型；資料科學工作區；熱門主題；對服務進行評分
solution: Experience Platform
title: 在Data Science Workspace UI中將模型作為服務發佈
type: Tutorial
description: Adobe Experience Platform資料科學工作區允許您將經過培訓和評估的模型作為服務發佈，使組織內的用戶能夠對資料進行評分，而無需建立自己的模型。
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 在Data Science Workspace UI中將模型作為服務發佈

Adobe Experience Platform資料科學工作區允許您將經過培訓和評估的模型作為服務發佈，使組織內的用戶能夠對資料進行評分，而無需建立自己的模型。

## 快速入門

要完成本教程，您必須具有訪問 [!DNL Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與系統管理員聯繫。

本教程要求現有模型並成功運行培訓。 如果沒有可發佈的模型，請 [在UI中訓練和評估模型](./train-evaluate-model-ui.md) 教程，然後繼續。

如果希望使用Sensei機器學習API發佈模型，請參閱 [API教程](./publish-model-service-api.md)。

## 發佈模型 {#publish-a-model}

在Adobe Experience Platform，選擇 **[!UICONTROL 模型]** 位於左導航列中，然後選擇 **[!UICONTROL 瀏覽]** 的子菜單。 選擇要作為服務發佈的模型的名稱。

![](../images/models-recipes/publish-model/browse_model.png)

選擇 **[!UICONTROL 發佈]** 靠近「模型概述」頁右上角以啟動服務建立過程。

![](../images/models-recipes/publish-model/view_training.png)

為服務輸入所需的名稱，並可選地提供服務說明，選擇 **[!UICONTROL 下一個]** 的子菜單。

![](../images/models-recipes/publish-model/configure_training.png)

列出了針對模型的所有成功培訓。 新服務將從所選培訓運行繼承培訓和評分配置。

![](../images/models-recipes/publish-model/select_training_run.png)

選擇 **[!UICONTROL 完成]** 建立服務並重定向到 **[!UICONTROL 服務庫]** 顯示所有可用服務，包括新建立的服務。

![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服務評分 {#access-a-service}

在Adobe Experience Platform，選擇 **[!UICONTROL 服務]** 的子菜單。 **[!UICONTROL 服務庫]**。 查找要使用的服務並選擇 **[!UICONTROL 開啟]**。

![](../images/models-recipes/publish-model/open_service.png)

在服務概述頁中，選擇 **[!UICONTROL 得分]**。

![](../images/models-recipes/publish-model/score_service.png)

為計分運行選擇適當的輸入資料集，然後選擇 **[!UICONTROL 下一個]**。 系統要求您為評分資料集執行相同步驟。 選擇輸入和輸出資料集後，可以更新配置。

![](../images/models-recipes/publish-model/select_datasets.png)

建立服務時，它繼承預設計分配置。 您可以通過按兩下這些值來查看這些配置並根據需要進行調整。 對配置滿意後，選擇 **[!UICONTROL 完成]** 開始計分。

![](../images/models-recipes/publish-model/scoring_configs.png)

服務 **概述** 頁面，顯示新計分作業及其進度的詳細資訊。 作業完成後， **[!UICONTROL 最近]** 標題 **[!UICONTROL 評分]** 容器已更新。

![](../images/models-recipes/publish-model/pending_scoring.png)

## 後續步驟 {#next-steps}

通過本教程，您已成功將模型發佈為可訪問的服務，並使用新服務通過 [!UICONTROL 服務庫]。 繼續下一教程，瞭解如何 [安排服務上的自動培訓和評分運行](./schedule-models-ui.md)。
