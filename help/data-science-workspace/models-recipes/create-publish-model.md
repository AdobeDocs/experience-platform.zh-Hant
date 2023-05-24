---
keywords: Experience Platform；機器學習模型；資料科學工作區；熱門主題；建立和發佈模型
solution: Experience Platform
title: 建立和發佈機器學習模型
type: Tutorial
description: 以下指南介紹建立和發佈機器學習模型所需的步驟。
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 建立和發佈機器學習模型

以下指南介紹建立和發佈機器學習模型所需的步驟。 每個部分都包含要執行的操作的說明，以及指向UI和API文檔的連結，以執行所述步驟。

## 快速入門

在啟動本教程之前，您必須具備以下先決條件：

- 訪問 [!DNL Adobe Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與系統管理員聯繫。

- 所有Data Science Workspace教程都使用Luma傾向模型。 為了跟進，您必須建立 [Luma丙烯模型模式和資料集](./create-luma-data.md)。

### 瀏覽資料並瞭解架構

登錄到 [Adobe Experience Platform](https://platform.adobe.com/) 選擇 **[!UICONTROL 資料集]** 列出所有現有資料集並選擇要瀏覽的資料集。 在這種情況下，應選擇 **Luma Web資料** 資料集。

![選擇Luma Web資料集](../images/models-recipes/model-walkthrough/luma-dataset.png)

資料集活動頁開啟，列出與您的資料集相關的資訊。 可以選擇 **[!UICONTROL 預覽資料集]** 靠近右上角，檢查樣本記錄。 您還可以查看所選資料集的架構。

![查看Luma Web資料](../images/models-recipes/model-walkthrough/preview-dataset.png)

在右欄中選擇架構連結。 出現跨距，選擇下方的連結 **[!UICONTROL 架構名稱]** 在新頁籤中開啟架構。

![預覽luma web資料架構](../images/models-recipes/model-walkthrough/preview-schema.png)

您可以使用提供的「探索資料分析」(EDA)筆記本進一步瀏覽資料。 此筆記本可用於幫助理解Luma資料中的模式、檢查資料健全性，以及為預測傾向模型匯總相關資料。 要瞭解有關探索性資料分析的更多資訊，請訪問 [EDA文檔](../jupyterlab/eda-notebook.md)。

## 建立Luma傾向處方 {#author-your-model}

主要元件 [!DNL Data Science Workspace] 生命週期涉及創作配方和模型。 Luma傾向模型旨在預測客戶是否具有從Luma購買產品的高傾向。

要建立Luma傾向模型，請使用處方生成器模板。 配方是模型的基礎，因為它們包含機器學習算法和用於解決特定問題的邏輯。 更重要的是，「配方」使您能夠將整個組織的機器學習民主化，使其他用戶能夠訪問一個模型以處理不同的使用案例，而無需編寫任何代碼。

關注 [使用JupyterLab筆記本建立模型](../jupyterlab/create-a-model.md) 教程，用於建立在後續教程中使用的Luma傾向模型配方。

## 從外部源導入和打包處方(*可選*)

如果要導入並打包配方以在Data Science Workspace中使用，則必須將源檔案打包到存檔檔案中。 關注 [將源檔案打包到處方](./package-source-files-recipe.md) 教程。 本教程將介紹如何將源檔案打包到配方中，這是將配方導入到Data Science Workspace的先決條件步驟。 教程完成後，您將在Azure容器註冊表中提供Docker映像，以及相應的映像URL，即存檔檔案。

此存檔檔案可通過遵循處方導入工作流使用 [UI工作流](./import-packaged-recipe-ui.md) 或 [API工作流](./import-packaged-recipe-api.md)。

## 訓練和評估模型 {#train-and-evaluate-your-model}

現在，您的資料已經準備好，而且配方已準備好，您就能夠進一步建立、培訓和評估機器學習模型。 使用處方生成器時，您應該已對模型進行培訓、評分和評估，然後才將其打包到處方中。

Data Science Workspace UI和API允許您將配方作為模型發佈。 此外，還可以進一步微調模型的特定方面，如添加、移除和更改超參數。

### 建立一個模式

要瞭解有關使用UI建立模型的詳細資訊，請訪問培訓並評估資料科學工作區中的模型 [UI教程](./train-evaluate-model-ui.md) 或 [API教程](./train-evaluate-model-api.md)。 本教程提供了一個示例，說明如何建立、訓練和更新超參數以優化模型。

>[!NOTE]
>
> 無法學習超參數，因此必須在進行培訓之前分配超參數。 調整超參數可能會改變訓練模型的精度。 由於優化模型是一個迭代過程，因此在獲得滿意的評價之前可能需要多次訓練運行。

## 對模型評分 {#score-a-model}

建立和發佈模型的下一步是操作模型，以便從資料庫和即時客戶概要檔案中得分和使用洞見。

通過將輸入資料輸入到現有的訓練模型中，可以在資料科學工作區中獲得評分。 然後，將評分結果作為新批儲存在指定的輸出資料集中並可查看。

要瞭解如何對模型進行評分，請訪問模型的評分 [UI教程](./score-model-ui.md) 或 [API教程](./score-model-api.md)。

## 將評分模型發佈為服務

Data Science Workspace允許您將經過培訓的模型作為服務發佈。 這樣，組織內的用戶就可以對資料進行評分，而無需建立自己的模型。

要瞭解如何將模型作為服務發佈，請訪問 [UI教程](./publish-model-service-ui.md) 或 [API教程](./publish-model-service-api.md)。

### 為服務安排自動培訓

在將模型發佈為服務後，可以為機器學習服務設定計畫評分和培訓運行。 自動化培訓和評分過程有助於通過跟蹤資料中的模式來保持和提高服務的效率。 訪問 [在Data Science Workspace UI中調度模型](./schedule-models-ui.md) 教程。

>[!NOTE]
>
> 您只能從UI為自動培訓和評分安排模型。

## 後續步驟 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] 提供工具和資源，以建立、評估和利用機器學習模型來生成資料預測和洞見。 當機器學習的洞察力被植入 [!DNL Profile]-enabled dataset，該資料也被作為 [!DNL Profile] 然後使用 [!DNL Adobe Experience Platform Segmentation Service]。

在接收配置檔案和時間序列資料時，即時客戶配置檔案自動決定通過稱為流分段的持續過程將資料包括或排除在段中，然後將其與現有資料合併並更新聯合視圖。 因此，您可以即時執行計算並做出決策，在客戶與您的品牌進行交互時向客戶提供增強的個性化體驗。

訪問教程 [利用機器學習的洞察力豐富即時客戶概要資訊](./enrich-profile.md) 瞭解有關如何利用機器學習的見解的更多資訊。
