---
keywords: Experience Platform；計畫模型；資料科學工作區；熱門主題；計畫評分；計畫培訓
solution: Experience Platform
title: 在Data Science Workspace UI中調度模型
type: Tutorial
description: Adobe Experience Platform資料科學工作區允許您在機器學習服務上設定計畫評分和培訓運行。 自動化培訓和評分流程有助於通過跟上資料中的模式來隨著時間的推移而維護和提高服務的效率。
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 在Data Science Workspace UI中調度模型

Adobe Experience Platform [!DNL Data Science Workspace] 允許您在機器學習服務上設定計畫評分和培訓運行。 自動化培訓和評分過程有助於通過跟蹤資料中的模式來保持和提高服務的效率。

本教程介紹如何通過以下步驟在現有服務上配置培訓和評分計畫： [!UICONTROL 服務庫]。 它分為以下主要部分：

- [配置計畫計分](#configure-scheduled-scoring)
- [配置計畫培訓](#configure-scheduled-training)

## 快速入門

要完成本教程，您必須具有訪問 [!DNL Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與系統管理員聯繫。

本教程需要現有服務。 如果您沒有可訪問的服務可以使用，則可以按照本教程建立 [將模型作為服務發佈](./publish-model-service-ui.md)。

## 配置計畫計分 {#configure-scheduled-scoring}

模型評分可以配置為基於計畫的自動化過程。 建立服務後，您可以按照以下步驟配置和應用評分計畫：

在Adobe Experience Platform，選擇 **[!UICONTROL 服務]** 的子菜單。 **[!DNL Service Gallery]**。 查找要計畫計分運行的服務並選擇 **[!UICONTROL 開啟]** 查看 **[!UICONTROL 概述]** 的子菜單。

![](../images/models-recipes/schedule/select_service.png)

「概覽」頁顯示服務的評分資訊。 選擇 **[!UICONTROL 更新計畫]** 連結以配置計分計畫。

![](../images/models-recipes/schedule/update_scoring.png)

為計分計畫配置頻率、開始日期、結束日期、輸入資料集和輸出資料集。 對配置滿意後，選擇 **[!UICONTROL 建立]** 更新服務的計分計畫。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

更新的計分計畫顯示在服務的 **[!UICONTROL 概述]** 的子菜單。

![](../images/models-recipes/schedule/scoring_set.png)

## 配置計畫培訓 {#configure-scheduled-training}

在服務上配置計畫培訓運行可確保機器學習模型更新為最新的資料模式。 每當計畫的培訓運行完成時，將使用生成的培訓模型為服務提供動力，直到下次計畫的培訓運行。

建立服務後，您可以按照以下步驟配置和應用培訓計畫：

在Adobe Experience Platform，選擇 **[!UICONTROL 服務]** 的子菜單。 **[!UICONTROL 服務庫]**。 查找要安排培訓運行的服務並選擇 **[!UICONTROL 開啟]** 查看 **[!UICONTROL 概述]** 的子菜單。

![](../images/models-recipes/schedule/select_service.png)

「概覽」頁顯示服務的培訓資訊。 選擇 **[!UICONTROL 更新計畫]** 連結以配置培訓計畫。

![](../images/models-recipes/schedule/update_training.png)

配置用於培訓計畫的頻率、開始日期、結束日期和輸入資料集。 對配置滿意後，選擇 **[!UICONTROL 建立]** 更新服務的培訓計畫。

![](../images/models-recipes/schedule/set_training_schedule.png)

更新的培訓計畫顯示在服務的 **[!UICONTROL 概述]** 的子菜單。

![](../images/models-recipes/schedule/training_set.png)

## 後續步驟

通過學完本教程，您成功地安排了服務上的自動培訓和評分運行，並完成了 [!DNL Data Science Workspace] 教程UI工作流。 如果您尚未這樣做，請考慮 [重新啟動教程](./create-retails-sales-dataset.md) 並遵循API工作流建立、培訓、評分和發佈模型。
