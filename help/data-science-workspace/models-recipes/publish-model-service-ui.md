---
keywords: Experience Platform；發佈模型；資料科學Workspace；熱門主題；為服務評分
solution: Experience Platform
title: 在資料科學Workspace UI中發佈模型作為服務
type: Tutorial
description: Adobe Experience Platform Data Science Workspace可讓您發佈經過訓練及評估的模型即服務，讓組織內的使用者無需建立自己的模型即可對資料評分。
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# 在資料科學工作區 UI 中將模式發佈為服務 {#publish-a-model-as-a-service}

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="將模式發佈為服務"
>abstract=""

Adobe Experience Platform Data Science Workspace可讓您發佈經過訓練及評估的模型即服務，讓組織內的使用者無需建立自己的模型即可對資料評分。

## 快速入門

若要完成本教學課程，您必須有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中組織的存取權，請在繼續之前與您的系統管理員交談。

本教學課程需要現有模型並成功完成訓練回合。 如果您沒有可發佈的模型，請遵循[訓練並在UI](./train-evaluate-model-ui.md)教學課程中評估模型，然後再繼續。

如果您偏好使用Sensei Machine Learning API發佈模型，請參閱[API教學課程](./publish-model-service-api.md)。

## 發佈模型 {#publish-a-model}

在Adobe Experience Platform中，選取位於左側導覽欄中的&#x200B;**[!UICONTROL 模型]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤以列出所有現有模型。 選取您要作為服務發佈的模型名稱。

![](../images/models-recipes/publish-model/browse_model.png)

選取[模型概觀]頁面右上角附近的&#x200B;**[!UICONTROL 發佈]**&#x200B;以開始服務建立程式。

![](../images/models-recipes/publish-model/view_training.png)

輸入所需的服務名稱，並選擇性地提供服務說明，完成後，請選取&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/publish-model/configure_training.png)

列出模型的所有成功訓練回合。 新服務將會從選取的訓練回合繼承訓練和評分設定。

![](../images/models-recipes/publish-model/select_training_run.png)

選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立服務，並重新導向至&#x200B;**[!UICONTROL 服務庫]**&#x200B;以顯示所有可用的服務，包括新建立的服務。

![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服務計分 {#access-a-service}

在Adobe Experience Platform中，選取位於左側導覽欄中的&#x200B;**[!UICONTROL 服務]**&#x200B;索引標籤，以存取&#x200B;**[!UICONTROL 服務庫]**。 尋找您要使用的服務，並選取&#x200B;**[!UICONTROL 開啟]**。

![](../images/models-recipes/publish-model/open_service.png)

在服務概觀頁面中，選取&#x200B;**[!UICONTROL 分數]**。

![](../images/models-recipes/publish-model/score_service.png)

為評分回合選取適當的輸入資料集，然後選取&#x200B;**[!UICONTROL 下一步]**。 系統會要求您對評分資料集執行相同步驟。 選取輸入和輸出資料集後，即可更新設定。

![](../images/models-recipes/publish-model/select_datasets.png)

建立服務時，會繼承預設評分設定。 您可以檢閱這些設定，並視需要按兩下值以調整它們。 在您滿意組態之後，請選取&#x200B;**[!UICONTROL 完成]**&#x200B;以開始評分回合。

![](../images/models-recipes/publish-model/scoring_configs.png)

在服務的&#x200B;**總覽**&#x200B;頁面上，會顯示新評分工作及其進度的詳細資料。 工作完成後，**[!UICONTROL 評分]**&#x200B;容器中的&#x200B;**[!UICONTROL 最近]**&#x200B;標題會更新。

![](../images/models-recipes/publish-model/pending_scoring.png)

## 後續步驟 {#next-steps}

依照此教學課程，您已經成功將模型發佈為可存取的服務，並透過[!UICONTROL 服務庫]使用新服務對資料進行評分。 繼續下一個教學課程，瞭解如何[排程服務](./schedule-models-ui.md)上的自動訓練和評分執行。
