---
keywords: Experience Platform；機器學習模型；Data Science Workspace；熱門主題；建立和發佈模型
solution: Experience Platform
title: 建立和發佈機器學習模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace提供使用預先建立的產品建議方式達成目標的方式。 請依照本教學課程，瞭解如何存取和瞭解您的零售資料、建立和最佳化機器學習模型，以及在資料科學工作區中產生見解。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 0%

---


# 建立和發佈機器學習模型

![](../images/models-recipes/model-walkthrough/objective.png)

假裝您擁有線上零售網站。 當您的客戶在零售網站購物時，您想要向他們提供個人化產品建議，以公開您企業提供的各種其他產品。 在您網站的存在期間，您不斷收集客戶資料，並想以某種方式利用這些資料產生個人化產品建議。

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 提供使用預先建立的產品建議方式達成 [目標的方式](../pre-built-recipes/product-recommendations.md)。請依照本教學課程，瞭解如何存取和瞭解您的零售資料、建立和最佳化機器學習模型，以及在[!DNL Data Science Workspace]中產生見解。

本教學課程反映[!DNL Data Science Workspace]的工作流程，並涵蓋建立機器學習模型的下列步驟：

1. [準備資料](#prepare-your-data)
2. [製作您的模型](#author-your-model)
3. [培訓並評估您的模型](#train-and-evaluate-your-model)
4. [實施您的模型](#operationalize-your-model)

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：

* 存取[!DNL Adobe Experience Platform]。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

* 啟用資產。 請連絡您的帳戶代表，為您布建下列項目。
   * 建議方式
   * Recommendations輸入資料集
   * Recommendations輸入結構
   * Recommendations輸出資料集
   * Recommendations輸出結構
   * Golden Data Set postValues
   * 金色資料集架構

* 從[Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs)下載3個必要的[!DNL Jupyter Notebook]檔案，這些檔案將用來示範[!DNL Data Science Workspace]中的[!DNL JupyterLab]工作流程。

* 對本教學課程中使用的下列主要概念有正確認識：
   * [[!DNL Experience Data Model]](../../xdm/home.md):由Adobe領導的標準化工作，為客戶體驗管理定義標 [!DNL Profile] 準架構，例如和ExperienceEvent。
   * 資料集：實際資料的儲存和管理結構。 [XDM架構](../../xdm/schema/field-dictionary.md)的物理實例化實例。
   * 批：資料集由批處理組成。 批是一組在一段時間內收集並作為單個單位一起處理的資料。
   * [!DNL JupyterLab]: [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是專案的開放原始碼Web介面， [!DNL Jupyter] 並緊密整合在 [!DNL Experience Platform]中。

## 準備您的資料{#prepare-your-data}

若要建立機器學習模型，向客戶提供個人化產品建議，您必須分析您網站上先前客戶購買的產品。 本節探討如何將此資料透過[!DNL Adobe Analytics]傳入至[!DNL Platform]，以及如何將該資料轉換為機器學習模型要使用的功能資料集。

### 探索資料並瞭解結構

1. 登入[Adobe Experience Platform](https://platform.adobe.com/)，然後按一下&#x200B;**[!UICONTROL Datasets]**&#x200B;以列出所有現有的資料集，並選取您要探索的資料集。 在此例中，[!DNL Analytics]資料集&#x200B;**Golden Data Set postValues**。
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. 選擇右上方附近的&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以檢查範例記錄，然後按一下&#x200B;**[!UICONTROL 關閉]**。
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. 在右側欄的「架構」下選取連結，以檢視資料集的架構，然後返回資料集詳細資料頁面。」
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

其他資料集已預先填入批次，以供預覽之用。 您可以重複上述步驟來檢視這些資料集。

| 資料集名稱 | 結構 | 說明 |
| ----- | ----- | ----- |
| Golden Data Set postValues | Golden Data Set架構 | [!DNL Analytics] 您網站的來源資料 |
| Recommendations輸入資料集 | Recommendations輸入結構 | 使用特徵管線將[!DNL Analytics]資料轉換為訓練資料集。 此資料用於訓練Product Recommendations機器學習模型。 `itemid` 並對 `userid` 應該客戶購買的產品。 |
| Recommendations輸出資料集 | Recommendations輸出結構 | 儲存計分結果的資料集，會包含每個客戶的建議產品清單。 |

## 製作您的型號{#author-your-model}

[!DNL Data Science Workspace]生命週期的第二個元件涉及編寫配方和模型。 「產品建議方式」旨在利用過去的購買資料和機器學習，大規模產生產品建議。

配方是模型的基礎，因為配方包含機器學習演算法和邏輯，可解決特定問題。 更重要的是，配方可讓您在組織內普及機器學習，讓其他使用者存取不同使用案例的模型，而不需撰寫任何程式碼。

### 探索產品建議方式

1. 在[!DNL Adobe Experience Platform]中，從左側導覽欄導覽至&#x200B;**[!UICONTROL Models]**，然後按一下頂端的&#x200B;**[!UICONTROL Recipes]**，以檢視組織的可用配方清單。
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. 按一下提供的&#x200B;**[!UICONTROL Recommendations Recipe]**名稱，找出並開啟。
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. 在右側邊欄中，按一下「建議輸入結構」，以檢視支援方式的結構。 ****&#x200B;架構欄位&quot;[!UICONTROL itemId]&quot;和&quot;[!UICONTROL userId]&quot;對應於該客戶在特定時間([!UICONTROL timestamp])購買的產品([!UICONTROL interactionType])。 請遵循相同的步驟，檢閱&#x200B;**[!UICONTROL Recommendations輸出結構描述]**的欄位。
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

您現在已檢視「產品建議方式」所需的輸入和輸出結構。 您現在可以繼續下一節，瞭解如何建立、訓練和評估產品建議模型。

## 培訓並評估型號{#train-and-evaluate-your-model}

現在您的資料已備妥，配方已可供使用，您可以建立、訓練和評估機器學習模型。

### 建立模型

「模型」是「方式」的例項，可讓您以規模來訓練和評分資料。

1. 在[!DNL Adobe Experience Platform]中，從左側導覽欄導覽至&#x200B;**[!UICONTROL Models]**，然後按一下頁面頂端的&#x200B;**[!UICONTROL Recipes]**，以顯示您組織的所有可用Recipes清單。
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. 按一下配方名稱，輸入配方的概述頁面，找出並開啟提供的&#x200B;**[!UICONTROL 建議配方]**。 按一下&#x200B;**[!UICONTROL 從中心（如果沒有現有的型號）或從「配方概述」頁面的右上角建立模型]**。
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. 會顯示可用訓練輸入資料集的清單，選擇&#x200B;**[!UICONTROL Recommendations Input Dataset]**，然後按一下&#x200B;**[!UICONTROL Next]**。
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. 提供模型的名稱，例如「產品建議模型」。 列出模型的可用配置，包含模型的預設培訓和計分行為的設定。 由於這些配置是您組織專屬的，因此不需要進行任何更改。 查看配置並按一下&#x200B;**[!UICONTROL 完成]**。
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. 模型現在已建立，而模型的&#x200B;*概述*頁面會顯示在新產生的訓練執行中。 在建立模型時，預設情況下會生成培訓運行。
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

您可以選擇等待培訓執行完成，或在下節中繼續建立新的培訓執行。

### 使用自訂超參數訓練模型

1. 在&#x200B;**模型概述**&#x200B;頁面上，按一下右上角的&#x200B;**[!UICONTROL 訓練]**&#x200B;以建立新的訓練執行。 選擇建立模型時使用的相同輸入資料集，然後按一下&#x200B;**[!UICONTROL Next]**。
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. 此時將顯示&#x200B;**Configuration**&#x200B;頁。 您可以在這裡設定訓練執行的&quot;[!UICONTROL num_recommendations]&quot;值，也稱為Hyperparameter。 訓練和優化的模型將根據訓練運行的結果利用效能最佳的超參數。

   無法學習超參數，因此必須在訓練執行之前先指派超參數。 調整超參數可能會改變訓練模型的精度。 由於模型最佳化是一個反覆的程式，因此在達到滿意的評估之前可能需要執行多次培訓。

   >[!TIP]
   >
   >將&#x200B;**[!UICONTROL num_recommendations]**&#x200B;設為10。

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. 新培訓執行完成後，模型評估圖表上會出現額外的資料點，這可能需要數分鐘。
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### 評估模型

每次訓練執行完成時，您都可以檢視產生的評估量度，以判斷模型執行的成效。

1. 按一下培訓執行，檢視每個已完成培訓執行的評估量度（精確度和召回率）。
2. 探索每個評估量度的資訊。 這些量度越高，模型的執行效果越好。
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. 您可以在右側導軌上查看用於每個培訓執行的資料集、結構和組態參數。
4. 返回「模型」頁面，並透過觀察其評估度量來識別執行成效最佳的培訓。

## 實施您的型號{#operationalize-your-model}

Data Science工作流程的最後一步是將您的模型實際運作，以便從資料儲存區獲得分數和使用見解。

### 分數並產生見解

1. 在產品建議Model *Overview*&#x200B;頁面上，按一下效能最佳的訓練執行名稱，並具有最高的回叫率和精確度值。
2. 在訓練執行詳細資訊頁面的右上方，按一下&#x200B;**[!UICONTROL Score]**。
3. 選擇&#x200B;**[!UICONTROL Recommendations輸入資料集]**&#x200B;作為計分輸入資料集，此資料集與您建立模型並執行其訓練執行時使用的資料集相同。 然後，按一下&#x200B;**[!UICONTROL Next]**。
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. 選擇&#x200B;**[!UICONTROL Recommendations Output Dataset]**作為計分輸出資料集。 計分結果會以批次形式儲存在此資料集中。
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. 檢閱計分設定。 這些參數包含先前選取的輸入和輸出資料集以及適當的結構描述。 按一下&#x200B;**[!UICONTROL 完成]**開始計分運行。 執行可能需要數分鐘才能完成。
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### 檢視獲得的深入資訊

計分執行成功完成後，您就可以預覽結果並檢視產生的見解。

1. 在計分執行頁面上，按一下已完成的計分執行，然後按一下右側導軌上的「預覽計分結果資料集」。****
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. 在預覽表格中，每一列包含特定客戶的產品建議，分別標示為[!UICONTROL recommendations]和[!UICONTROL userId]。 由於範例螢幕擷取畫面中的[!UICONTROL num_recommendations] Hyperparameter已設為10，因此每列建議最多可包含10個產品身分識別，並以數字元號(#)分隔。
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## 下一步 {#next-steps}

做得好，您已成功產生產品建議！

本教學課程將您介紹[!DNL Data Science Workspace]的工作流程，以示範如何透過機器學習將原始資料轉換為有用的資訊。 若要進一步瞭解如何使用[!DNL Data Science Workspace]，請繼續至[上的下一份指南，以建立零售銷售模式和資料集](./create-retails-sales-dataset.md)。