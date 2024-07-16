---
keywords: Experience Platform；機器學習模型；資料科學Workspace；熱門主題；建立和發佈模型
solution: Experience Platform
title: 建立和Publish機器學習模型
type: Tutorial
description: 下列指南說明建立和發佈機器學習模型所需的步驟。
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# 建立及發佈機器學習模型

下列指南說明建立和發佈機器學習模型所需的步驟。 每個區段都包含您要執行操作的說明，以及UI和API檔案的連結，以便執行所述的步驟。

## 快速入門

開始進行本教學課程前，您必須具備下列必要條件：

- 存取[!DNL Adobe Experience Platform]。 如果您沒有[!DNL Experience Platform]中組織的存取權，請在繼續之前與您的系統管理員交談。

- 所有資料科學Workspace教學課程都使用Luma傾向模型。 為了遵循，您必須已建立[Luma傾向模型結構描述和資料集](./create-luma-data.md)。

### 探索資料並瞭解結構描述

登入[Adobe Experience Platform](https://platform.adobe.com/)並選取&#x200B;**[!UICONTROL 資料集]**&#x200B;以列出所有現有的資料集，並選取您要探索的資料集。 在此情況下，您應該選取&#x200B;**Luma網頁資料**&#x200B;資料集。

![選取Luma網頁資料集](../images/models-recipes/model-walkthrough/luma-dataset.png)

資料集活動頁面隨即開啟，列出與資料集相關的資訊。 您可以選取右上角附近的&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;來檢查範例記錄。 您也可以檢視所選資料集的結構描述。

![預覽Luma網頁資料](../images/models-recipes/model-walkthrough/preview-dataset.png)

在右側欄中選取結構描述連結。 彈出視窗隨即顯示，選取&#x200B;**[!UICONTROL 結構描述名稱]**&#x200B;下的連結會在新索引標籤中開啟結構描述。

![預覽luma web資料結構描述](../images/models-recipes/model-walkthrough/preview-schema.png)

您可以使用提供的探索資料分析(EDA)筆記本進一步探索資料。 此筆記型電腦可用來協助瞭解Luma資料中的模式、檢查資料健全度，並總結預測傾向模型的相關資料。 若要進一步瞭解探索資料分析，請造訪[EDA檔案](../jupyterlab/eda-notebook.md)。

## 建立Luma傾向指導方針 {#author-your-model}

[!DNL Data Science Workspace]生命週期的主要元件涉及編寫配方和模型。 Luma傾向模型旨在預測客戶是否有從Luma購買產品的高傾向。

若要建立Luma傾向模型，系統會使用配方產生器範本。 配方是模型的基礎，因為它們包含為解決特定問題而設計的機器學習演演算法和邏輯。 更重要的是，訣竅可讓您將整個組織的機器學習普及化，讓其他使用者無需撰寫任何程式碼即可存取不同使用案例的模型。

依照[使用JupyterLab Notebooks](../jupyterlab/create-a-model.md)教學課程建立模型，以建立用於後續教學課程的Luma傾向模型配方。

## 從外部來源匯入並封裝配方（*選擇性*）

如果您想要匯入並封裝配方以用於Data Science Workspace，您必須將來源檔案封裝到封存檔案中。 請依照[封裝來源檔案到配方](./package-source-files-recipe.md)教學課程中。 本教學課程說明如何將來源檔案封裝到配方中，這是將配方匯入資料科學Workspace的先決條件。 完成教學課程後，系統就會在Azure容器登入中為您提供Docker影像，以及對應的影像URL，亦即封存檔案。

此封存檔案可用於在資料科學Workspace中建立配方，方法是使用[UI工作流程](./import-packaged-recipe-ui.md)或[API工作流程](./import-packaged-recipe-api.md)遵循配方匯入工作流程。

## 訓練和評估模型 {#train-and-evaluate-your-model}

現在您的資料已準備就緒且配方已準備就緒，您能夠進一步建立、訓練及評估您的機器學習模型。 使用配方產生器時，您應該先培訓、評分和評估模型，再將其封裝到配方中。

資料科學Workspace UI和API可讓您以模型形式發佈配方。 此外，您可以進一步微調模型的特定方面，例如新增、移除和變更超引數。

### 建立模型

若要瞭解有關使用UI建立模型的詳細資訊，請造訪該訓練，並在Data Science Workspace [UI教學課程](./train-evaluate-model-ui.md)或[API教學課程](./train-evaluate-model-api.md)中評估模型。 本教學課程提供如何建立、訓練及更新超引數以微調模型的範例。

>[!NOTE]
>
> 無法學習超引數，因此必須在執行訓練前指派它們。 調整超引數可能會改變已訓練模型的精確度。 由於模型最佳化是一個反複的過程，因此在達到滿意的評估之前，可能需要多次訓練執行。

## 為模型評分 {#score-a-model}

建立和發佈模型的下一步是將模型投入運作，以便對Data Lake和即時客戶個人檔案的深入分析評分並加以使用。

將輸入資料饋送至現有的已訓練模型，即可達到資料科學Workspace的評分。 評分結果會儲存於指定的輸出資料集，並可作為新批次檢視。

若要瞭解如何為您的模型評分，請造訪模型[UI教學課程](./score-model-ui.md)或[API教學課程](./score-model-api.md)評分。

## Publish已評分模型即服務

資料科學Workspace可讓您將經過訓練的模型發佈為服務。 這可讓貴組織內的使用者對資料評分，而不需要建立自己的模型。

若要瞭解如何將模型發佈為服務，請造訪[UI教學課程](./publish-model-service-ui.md)或[API教學課程](./publish-model-service-api.md)。

### 排程服務的自動化訓練

將模型發佈為服務後，您就可以為機器學習服務設定已排程的評分和訓練回合。 自動化訓練和評分程式，可隨時掌握資料中的模式，協助維持及改善服務效率。 造訪[在資料科學Workspace UI](./schedule-models-ui.md)教學課程中排程模型。

>[!NOTE]
>
> 您只能從UI排程自動化訓練和評分的模型。

## 後續步驟 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace]提供各種工具和資源，用來建立、評估及運用機器學習模型，以產生資料預測和深入分析。 將機器學習深入分析擷取至啟用[!DNL Profile]的資料集時，該相同資料也會擷取為[!DNL Profile]記錄，然後可以使用[!DNL Adobe Experience Platform Segmentation Service]分段。

在擷取設定檔和時間序列資料時，即時客戶設定檔會透過進行中的串流細分程式，自動決定從區段包含或排除該資料，然後再將其與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算並作出決定，在客戶與您的品牌互動時，向客戶傳遞強化的個人化體驗。

請造訪[使用機器學習深入分析豐富即時客戶設定檔](./enrich-profile.md)的教學課程，瞭解更多有關如何使用機器學習深入分析的資訊。
