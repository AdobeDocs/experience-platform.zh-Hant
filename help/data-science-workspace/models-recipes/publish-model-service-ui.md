---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 以服務形式發佈模型(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 以服務形式發佈模型(UI)

Adobe Experience Platform Data Science Workspace可讓您將經過訓練和評估的模型發佈為服務，讓IMS組織內的使用者可對資料評分，而不需建立自己的模型。

本教學課程將逐步介紹如何以服務形式發佈模型，以及使用服務透過服務收藏館對資料 *評分*。 它分為以下幾個主要部分：

- [發佈模型](#publish-a-model)
- [使用服務進行分數](#access-a-service)

## 快速入門

若要完成本教學課程，您必須擁有Experience Platform的存取權。 如果您無法存取Experience Platform中的IMS組織，請在繼續前先與系統管理員聯絡。

本教學課程需要具備成功訓練執行的現有模型。 如果您沒有可發佈的模型，請依照UI教學課程中 [的「訓練」並評估模型](./train-evaluate-model-ui.md) ，然後再繼續。

如果您偏好使用Sensei機器學習API來發佈模型，請參閱 [API教學課程](./publish-model-service-api.md)。

## 發佈模型 {#publish-a-model}

1. 在Adobe Experience Platform中，按一下左 **[!UICONTROL Models]** 側導覽欄中的連結，以列出所有現有的模型。 查找並按一下要作為服務發佈的模型的名稱。
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 單 **[!UICONTROL Publish]** 擊「模型概述」頁右上角的附近以啟動服務建立過程。
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 輸入所需的服務名稱，並選擇性地提供服務說明，在完成時按 **[!UICONTROL Next]** 一下。
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 列出所有成功的「模型」訓練執行。 新服務將繼承所選培訓運行中的培訓和評分配置。
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 按一 **[!UICONTROL Finish]** 下以建立服務並重新導向至以 **[!UICONTROL Service Gallery]** 顯示所有可用服務，包括新建立的服務。
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服務進行分數 {#access-a-service}

1. 在Adobe Experience Platform中，按一 **[!UICONTROL Services]** 下左側導覽欄中的標籤以存取「服 *務收藏館」*。 尋找您要使用的服務，然後按一下 **[!UICONTROL Score]**。
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 為計分執行選取適當的輸入資料集，然後按一下 **[!UICONTROL Next]**。
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 為計分結果選擇適當的輸出資料集，然後按一下 **[!UICONTROL Next]**。
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 建立服務時，它會繼承預設計分配置。 您可以檢閱這些設定，並視需要按兩下值以調整這些設定。 對配置滿意後，按一下以 **[!UICONTROL Finish]** 開始計分運行。
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 在「服務」的「 *概述* 」頁面上，會顯示新計分工作及其進度的詳細資料。 作業完成後，計 **[!UICONTROL Most Recent]** 分作業將更新。
   ![](../images/models-recipes/publish-model/score_pending.png)

## 下一步 {#next-steps}

在本教學課程中，您已成功地將模型發佈為可存取的服務，並透過服務收藏館使用新的服務計 *分資料*。 繼續下一個教學課程，瞭解如何安 [排在服務上執行自動化訓練和計分](./schedule-models-ui.md)。
