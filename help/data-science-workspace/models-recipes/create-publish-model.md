---
keywords: Experience Platform；機器學習模型；Data Science Workspace；熱門主題；建立和發佈模型
solution: Experience Platform
title: 建立和發佈機器學習模型
type: Tutorial
description: 以下指南說明建立和發佈機器學習模型所需的步驟。
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 建立並發佈機器學習模型

以下指南說明建立和發佈機器學習模型所需的步驟。 每個區段都包含您要執行之作業的說明，以及UI和API檔案的連結，以執行所述步驟。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：

- 存取 [!DNL Adobe Experience Platform]. 如果您無權存取 [!DNL Experience Platform]，請在繼續操作之前與系統管理員聯繫。

- 所有Data Science Workspace教學課程都使用Luma傾向模型。 若要繼續操作，您必須已建立 [Luma傾向模型結構與資料集](./create-luma-data.md).

### 探索資料並了解結構

登入 [Adobe Experience Platform](https://platform.adobe.com/) 選取 **[!UICONTROL 資料集]** 列出所有現有資料集，並選取您要探索的資料集。 在此情況下，您應選取 **Luma網站資料** 資料集。

![選取Luma網路資料集](../images/models-recipes/model-walkthrough/luma-dataset.png)

資料集活動頁面隨即開啟，列出與資料集相關的資訊。 您可以選取 **[!UICONTROL 預覽資料集]** 靠近右上角以檢查範例記錄。 您也可以檢視所選資料集的結構。

![預覽Luma網站資料](../images/models-recipes/model-walkthrough/preview-dataset.png)

在右側邊欄中選取架構連結。 隨即顯示彈出視窗，選取下方的連結 **[!UICONTROL 方案名稱]** 在新索引標籤中開啟架構。

![預覽luma web資料結構](../images/models-recipes/model-walkthrough/preview-schema.png)

您可以使用提供的探索資料分析(EDA)筆記型電腦進一步探索資料。 此筆記型電腦可協助您了解Luma資料中的模式、檢查資料的健全度，以及為預測傾向模型匯總相關資料。 若要進一步了解探索資料分析，請造訪 [EDA檔案](../jupyterlab/eda-notebook.md).

## 建立Luma傾向方式 {#author-your-model}

的主要元件 [!DNL Data Science Workspace] 生命週期涉及製作方式和模型。 Luma傾向模型旨在針對客戶是否有向Luma購買產品的高傾向產生預測。

若要建立Luma傾向模型，會使用方式產生器範本。 方式是模型的基礎，因為方式包含機器學習演算法和邏輯，專為解決特定問題而設計。 更重要的是，訣竅可讓您將整個組織的機器學習大眾化，讓其他使用者能存取不同使用案例的模型，而不需編寫任何程式碼。

關注 [使用JupyterLab Notebooks建立模型](../jupyterlab/create-a-model.md) 建立Luma傾向模型配方的教學課程，此方法用於後續的教學課程。

## 從外部來源匯入和封裝方式(*可選*)

如果您想要匯入並封裝方式以在Data Science Workspace中使用，則必須將來源檔案封裝至封存檔案。 關注 [將源檔案打包到配方中](./package-source-files-recipe.md) 教學課程。 本教學課程說明如何將來源檔案封裝至方式，這是將方式匯入至Data Science Workspace的先決條件步驟。 教學課程完成後，您會在Azure容器註冊表中獲得Docker影像，以及對應的影像URL，換句話說，即封存檔案。

此封存檔案可依照方式匯入工作流程，使用 [UI工作流程](./import-packaged-recipe-ui.md) 或 [API工作流程](./import-packaged-recipe-api.md).

## 訓練和評估模型 {#train-and-evaluate-your-model}

現在，您的資料已準備就緒，配方已準備就緒，您可以進一步建立、訓練和評估機器學習模型。 使用方式產生器時，您應先訓練、評分和評估模型，再將其包裝成方式。

Data Science Workspace UI和API可讓您以模型形式發佈方式。 此外，還可以進一步微調模型的特定方面，如添加、刪除和更改超參數。

### 建立一個模式

若要進一步了解如何使用UI建立模型，請前往Data Science Workspace中的訓練並評估模型 [UI教學課程](./train-evaluate-model-ui.md) 或 [API教學課程](./train-evaluate-model-api.md). 本教學課程提供如何建立、訓練和更新超參數以微調模型的範例。

>[!NOTE]
>
> 無法學習超參數，因此必須在培訓運行之前分配超參數。 調整超參數可能會改變訓練模型的準確度。 由於優化模型是一個迭代過程，因此在獲得滿意的評估之前可能需要多次訓練運行。

## 對模型評分 {#score-a-model}

建立和發佈模型的下一步是運作您的模型，以便對資料湖和即時客戶設定檔的分析評分並加以使用。

將輸入資料饋送至現有的訓練模型，即可在Data Science Workspace中進行計分。 然後會儲存計分結果，並以新批次形式在指定的輸出資料集中檢視。

若要了解如何為模型評分，請造訪模型分數 [UI教學課程](./score-model-ui.md) 或 [API教學課程](./score-model-api.md).

## 發佈計分模型作為服務

Data Science Workspace可讓您將訓練好的模型發佈為服務。 這可讓您組織內的使用者對資料評分，而無須建立自己的模型。

若要了解如何以服務形式發佈模型，請造訪 [UI教學課程](./publish-model-service-ui.md) 或 [API教學課程](./publish-model-service-api.md).

### 為服務安排自動培訓

將模型發佈為服務後，您就可以為機器學習服務設定計畫的分數和培訓運行。 自動化培訓和計分流程有助於通過跟上資料中的模式，在時間內維護和提高服務的效率。 造訪 [在Data Science Workspace UI中排程模型](./schedule-models-ui.md) 教學課程。

>[!NOTE]
>
> 您只能從UI排程模型以進行自動化訓練和計分。

## 後續步驟 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] 提供工具和資源，用於建立、評估及運用機器學習模型，以產生資料預測和深入分析。 將機器學習深入分析擷取至 [!DNL Profile]啟用資料集，相同資料也會擷取為 [!DNL Profile] 然後可以使用 [!DNL Adobe Experience Platform Segmentation Service].

內嵌設定檔和時間序列資料時，即時客戶設定檔會自動決定，先透過稱為串流分段的持續程式，將該資料納入或排除區段，再與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算，並做出決策，在客戶與您的品牌互動時，向客戶提供增強的個人化體驗。

請造訪 [透過機器學習深入分析擴充即時客戶設定檔](./enrich-profile.md) 深入了解如何運用機器學習的深入分析。
