---
keywords: Experience Platform;機器學習模型;數據科學工作環境;熱門話題;創建和發佈模型
solution: Experience Platform
title: 建立和Publish機器學習模型
type: Tutorial
description: 以下指南介紹了創建和發佈機器學習模型所需的步驟。
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# 建立及發佈機器學習模型

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

以下指南介紹了創建和發佈機器學習模型所需的步驟。 每個部分都包含您將執行的操作的說明，以及對執行所述步驟的UI和 API 文件的連結。

## 快速入門

在開始此教學課程之前，必須滿足以下先決條件：

- 存取 [!DNL Adobe Experience Platform]。 如果您無權存取 中的 [!DNL Experience Platform]組織，請在繼續操作前與系統管理員聯繫。

- 所有 Data Science 工作環境 教學課程都使用 Luma 傾向模型。 若要繼續追隨，您必須已建立 [Luma propenstiy 模型架構和數據集](./create-luma-data.md)。

### 探索數據並了解架構

登錄到 [Adobe Experience Platform](https://platform.adobe.com/) 並選擇 **[!UICONTROL 數據集]** 以清單所有現有數據集，然後選擇按讚流覽的資料集。 在這種情況下，您應選擇 **Luma Web 数据** 資料集。

![選取Luma網頁資料集](../images/models-recipes/model-walkthrough/luma-dataset.png)

資料集活動頁面隨即開啟，列出與資料集相關的資訊。 您可以選取右上角附近的&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;來檢查範例記錄。 您也可以檢視所選資料集的結構描述。

![預覽Luma網頁資料](../images/models-recipes/model-walkthrough/preview-dataset.png)

在右側欄中選取結構描述連結。 彈出視窗隨即顯示，選取&#x200B;**[!UICONTROL 結構描述名稱]**&#x200B;下的連結會在新索引標籤中開啟結構描述。

![預覽 Luma 網站数据綱要](../images/models-recipes/model-walkthrough/preview-schema.png)

可以使用提供的探索性數據分析 （EDA） 筆記本進一步瀏覽數據。 此筆記本可用於幫助瞭解 Luma 數據中的模式、檢查數據健全性以及匯總預測傾向模型的相關數據。 要了解有關探索性数据分析的更多信息，造訪 [EDA 文檔](../jupyterlab/eda-notebook.md)。

## 建立亮度傾向方式 {#author-your-model}

[!DNL Data Science Workspace]生命週期的主要元件涉及編寫配方和模型。 Luma傾向模型旨在預測客戶是否有從Luma購買產品的高傾向。

若要建立 Luma 傾向模型，需使用方式產生器範本。 配方是模型的基礎，因為它們包含旨在解決特定問題的機器學習演算法和邏輯。 更重要的是，配方使您能夠在整個組織中民主化機器學習，使其他用戶能夠在不編寫任何代碼的情況下訪問不同用例的模型。

[按照使用 JupyterLab 筆記本](../jupyterlab/create-a-model.md)創建模型教學課程創建 Luma 傾向模型方式，後續教程將使用該模型。

## 從外部源匯入和打包方式（*可選*）

如果要導入和打包方式以用於數據科學工作環境，則必須將源檔打包到存檔檔中。 [按照包源文件進入方式](./package-source-files-recipe.md)教學課程。本教學課程介紹如何將源文件打包到方式中，這是將方式導入數據科學工作環境的先決條件步驟。 教學課程完成後，會在 Azure 容器註冊表中提供 Docker 映射，以及相應的映射URL，換句話說，存檔文件。

此存檔文件可用於在數據科學工作環境中創建方式，方法是使用 UI 工作流程](./import-packaged-recipe-ui.md) 或 [API 工作流程](./import-packaged-recipe-api.md)遵循[方式導入工作流程。

## 訓練和評估模型 {#train-and-evaluate-your-model}

現在，您的數據已準備就緒，方式已準備就緒，您可以進一步創建、訓練和評估機器學習模型。 使用配方生成器時，在將模型打包到方式之前，您應該已經訓練、評分和評估了模型。

數據科學工作環境 UI和 API 允許您將方式發佈為模型。 此外，您可以進一步微調模型的特定方面，例如新增、移除和變更超引數。

### 建立模型

若要瞭解有關使用UI建立模型的詳細資訊，請造訪該訓練，並在Data Science Workspace [UI教學課程](./train-evaluate-model-ui.md)或[API教學課程](./train-evaluate-model-api.md)中評估模型。 本教學課程提供如何建立、訓練及更新超引數以微調模型的範例。

>[!NOTE]
>
> 無法學習超引數，因此必須在執行訓練前指派它們。 調整超引數可能會改變已訓練模型的精確度。 由於模型最佳化是一個反複的過程，因此在達到滿意的評估之前，可能需要多次訓練執行。

## 對模型進行評分 {#score-a-model}

創建和發佈模型的下一步是操作模型，以便對數據湖和即時客戶檔案中的見解進行評分和使用。

數據科學工作環境中的評分可以通過將輸入數據饋送到現有的訓練模型中來實現。 然後，評分結果將作為新批次存儲在指定的輸出資料集中並可供查看。

若要瞭解如何為您的模型評分，請造訪模型[UI教學課程](./score-model-ui.md)或[API教學課程](./score-model-api.md)評分。

## Publish已評分模型即服務

數據科學工作環境允許將經過訓練的模型發佈即服務。 這使組織內的使用者無需創建自己的模型即可對數據進行評分。

若要了解如何發佈模型即服務，請造訪 [UI 教學課程](./publish-model-service-ui.md) 或 [API 教學課程](./publish-model-service-api.md)。

### 安排服務的自動化培訓

將模型發佈為服務后，可以為機器學習服務設置計劃的評分和培訓運行。 自動化培訓和評分過程可以通過跟上數據中的模式來幫助隨著時間的推移保持和提高服務的效率。 [訪問数据科學工作環境 UI](./schedule-models-ui.md)教學課程中的計劃模型。

>[!NOTE]
>
> 您只能從UI排程自動化訓練和評分的模型。

## 後續步驟 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace]提供各種工具和資源，用來建立、評估及運用機器學習模型，以產生資料預測和深入分析。 將機器學習深入分析擷取至啟用[!DNL Profile]的資料集時，該相同資料也會擷取為[!DNL Profile]記錄，然後可以使用[!DNL Adobe Experience Platform Segmentation Service]分段。

在擷取設定檔和時間序列資料時，即時客戶設定檔會透過進行中的串流細分程式，自動決定從區段包含或排除該資料，然後再將其與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算並作出決定，在客戶與您的品牌互動時，向客戶傳遞強化的個人化體驗。

請造訪[使用機器學習深入分析豐富即時客戶設定檔](./enrich-profile.md)的教學課程，瞭解更多有關如何使用機器學習深入分析的資訊。
