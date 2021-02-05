---
keywords: Experience Platform；發佈模型；Data Science Workspace；熱門主題；為服務評分
solution: Experience Platform
title: 在資料科學工作區UI中以服務形式發佈模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace可讓您將經過訓練和評估的模型發佈為服務，讓IMS組織內的使用者可對資料評分，而不需建立自己的模型。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# 在Data Science Workspace UI中以服務形式發佈模型

Adobe Experience Platform Data Science Workspace可讓您將經過訓練和評估的模型發佈為服務，讓IMS組織內的使用者可對資料評分，而不需建立自己的模型。

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

本教學課程需要具備成功訓練執行的現有模型。 如果您沒有可發佈的模型，請依照UI](./train-evaluate-model-ui.md)教學課程中的[訓練並評估模型，然後再繼續。

如果您偏好使用Sensei機器學習API來發佈模型，請參閱[API教學課程](./publish-model-service-api.md)。

## 發佈型號{#publish-a-model}

1. 在Adobe Experience Platform中，按一下左側導覽欄中的&#x200B;**[!UICONTROL Models]**連結，以列出所有現有的模型。 查找並按一下要作為服務發佈的模型的名稱。
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 按一下「模型概述」頁右上角的&#x200B;**[!UICONTROL Publish]**以啟動服務建立過程。
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 輸入所需的服務名稱並選擇性地提供服務說明，完成後，按一下「下一步」。****
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 列出所有成功的「模型」訓練執行。 新服務將繼承所選培訓運行中的培訓和評分配置。
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以建立服務並重定向至&#x200B;**[!UICONTROL 服務庫]**以顯示所有可用服務，包括新建立的服務。
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服務{#access-a-service}得分

1. 在Adobe Experience Platform中，按一下左側導覽欄中的&#x200B;**[!UICONTROL 服務]**&#x200B;標籤，以存取&#x200B;**[!UICONTROL 服務收藏館]**。 尋找您想要使用的服務，然後按一下&#x200B;**[!UICONTROL Score]**。
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 為計分執行選擇適當的輸入資料集，然後按一下&#x200B;**[!UICONTROL Next]**。
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 為計分結果選擇適當的輸出資料集，然後按一下&#x200B;**[!UICONTROL Next]**。
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 建立服務時，它會繼承預設計分配置。 您可以檢閱這些設定，並視需要按兩下值以調整這些設定。 對配置滿意後，按一下&#x200B;**[!UICONTROL 完成]**開始計分運行。
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 在服務的&#x200B;**概述**&#x200B;頁面上，會顯示新計分工作及其進度的詳細資料。 作業完成後，**[!UICONTROL Scoring]**&#x200B;容器內的&#x200B;**[!UICONTROL 最近]**標題將會更新。
   ![](../images/models-recipes/publish-model/score_pending.png)

## 下一步 {#next-steps}

在本教學課程中，您已成功將模型發佈為可存取的服務，並透過[!UICONTROL 服務收藏館]使用新服務計分資料。 繼續下一個教學課程，瞭解如何[安排在服務](./schedule-models-ui.md)上執行自動培訓和計分。
