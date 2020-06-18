---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 以服務形式發佈模型(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 7dc5075d3101b4780af92897c0381e73a9c5aef0
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 以服務形式發佈模型(UI)

Adobe Experience Platform Data Science Workspace可讓您將經過訓練和評估的模型發佈為服務，讓IMS組織內的使用者可對資料評分，而不需建立自己的模型。

## 快速入門

若要完成本教學課程，您必須擁有存取權 [!DNL Experience Platform]。 如果您無權存取中的IMS組織，請先與您的系 [!DNL Experience Platform]統管理員聯絡，然後再繼續。

本教學課程需要具備成功訓練執行的現有模型。 如果您沒有可發佈的模型，請依照UI教學課程中 [的「訓練」並評估模型](./train-evaluate-model-ui.md) ，然後再繼續。

如果您偏好使用Sensei機器學習API來發佈模型，請參閱 [API教學課程](./publish-model-service-api.md)。

## 發佈模型 {#publish-a-model}

1. 在Adobe Experience Platform中，按一下左側導 **[!UICONTROL 覽欄中的]** 「模型」連結，以列出所有現有的模型。 查找並按一下要作為服務發佈的模型的名稱。
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 按一 **[!UICONTROL 下]** 「模型概述」頁面右上角的「發佈」，以啟動服務建立程式。
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 輸入所需的服務名稱，並選擇性地提供服務說明，完成後按一 **[!UICONTROL 下]** 「下一步」。
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 列出所有成功的「模型」訓練執行。 新服務將繼承所選培訓運行中的培訓和評分配置。
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 按一 **[!UICONTROL 下「完成]** 」以建立服務，並重新導向至「服務收藏館 **** 」以顯示所有可用的服務，包括新建立的服務。
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服務進行分數 {#access-a-service}

1. 在Adobe Experience Platform中，按一下左側導 **[!UICONTROL 覽欄中的]** 「服務」標籤，以存取「服 *務收藏館」*。 尋找您想要使用的服務，然後按一下「分 **[!UICONTROL 數」]**。
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 為計分執行選取適當的輸入資料集，然後按一下「下 **[!UICONTROL 一步]**」。
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 為計分結果選擇適當的輸出資料集，然後按一下「下 **[!UICONTROL 一步]**」。
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 建立服務時，它會繼承預設計分配置。 您可以檢閱這些設定，並視需要按兩下值以調整這些設定。 對配置滿意後，按一下「完 **[!UICONTROL 成]** 」開始計分運行。
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 在「服務」的「 *概述* 」頁面上，會顯示新計分工作及其進度的詳細資料。 作業完成後，「最 **[!UICONTROL 近]** 」計分作業將會更新。
   ![](../images/models-recipes/publish-model/score_pending.png)

## 下一步 {#next-steps}

在本教學課程中，您已成功地將模型發佈為可存取的服務，並透過服務收藏館使用新的服務計 *分資料*。 繼續下一個教學課程，瞭解如何安 [排在服務上執行自動化訓練和計分](./schedule-models-ui.md)。
