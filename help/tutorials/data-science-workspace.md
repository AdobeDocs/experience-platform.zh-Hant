---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料科學工作區教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---


# 資料科學工作區教學課程

Adobe Experience Platform Data Science Workspace運用機器學習和人工智慧，從您的資料建立見解。 Data Science Workspace整合至Adobe Experience Platform，可協助您透過Adobe解決方案使用內容和資料資產進行預測。 所有技能等級的資料科學家都擁有複雜、簡單易用的工具，可支援快速開發、訓練和調整機器學習方式- AI技術的所有優點，而不需複雜。

若要進一步瞭解，請先閱讀資料科學工 [作區概觀](../data-science-workspace/home.md)。

## Sensei Machine Learning API

Sensei機器學習API為資料科學家提供機制，以組織和管理機器學習服務，從演算法上線到實驗，再到服務部署。

**目前提供下列API開發人員指南：**
- [引擎](../data-science-workspace/api/engines.md) -瞭解如何查找Docker註冊表、建立引擎、建立功能管線引擎、擷取引擎的資訊、更新引擎以及刪除引擎。
- [MLInstances（方式）](../data-science-workspace/api/mlinstances.md) -瞭解如何建立MLInstance、擷取MLInstance的資訊、更新MLInstance，以及刪除MLInstance。
- [實驗](../data-science-workspace/api/experiments.md) -瞭解如何建立實驗、擷取實驗或實驗執行資訊、更新實驗及刪除實驗。
- [模型](../data-science-workspace/api/models.md) -瞭解如何註冊自己的模型、擷取模型的資訊、更新模型、刪除模型、建立模型的新轉碼，以及擷取轉碼模型的詳細資訊。
- [MLServices](../data-science-workspace/api/mlservices.md) —— 瞭解如何建立MLService、擷取MLService的資訊、更新MLService，以及刪除MLService。
- [前瞻分析](../data-science-workspace/api/insights.md) -瞭解如何擷取前瞻分析的資訊、新增模型前瞻分析，以及擷取演算法的預設度量清單。

若要進一步瞭解並取得使用Sensei Machine Learning API執行CRUD作業所需的值，請造訪快速入 [門指南](../data-science-workspace/api/getting-started.md)。

## 如何使用JupyterLab筆記本

[!DNL JupyterLab] 是Web使用者介面，可 [!DNL Project Jupyter] 與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。 本檔案提供執行常 [!DNL JupyterLab] 見動作的概觀及功能說明。

**本指南將幫助您：**
- 存取並瞭解介 [!DNL JupyterLab] 面。
- 瞭解程式碼儲存格和內部的可用內核 [!DNL JupyterLab]。
- 瞭解Python/R中的GPU和記憶體伺服器組態。
- 使用筆記型電 [!DNL Platform] 腦讀取和查詢資料。
- 瞭解筆記型電腦的資料限制。

若要進一步瞭解，請造訪 [JupyterLab使用指南](../data-science-workspace/jupyterlab/overview.md)。

## 封裝Docker配方製作的來源檔案

Docker映像允許您使用應用程式所需的所有部件來封裝應用程式。 這包括一個軟體包中的所有庫和其他相關性。 內建的Docker影像會使用在方式建立工作流程期間提供給您的認證，推送至Azure容器註冊表。

**本教學課程將協助您：**
- 下載建立方式的必要先決條件。
- 瞭解以Docker為基礎的模型製作。
- 建立適用於Python、R、PySpark或Scala(Spark)的Docker影像。
- 獲取Docker源檔案URL。

若要進一步瞭解，請依照套件 [來源檔案，進入配方教學課程](../data-science-workspace/models-recipes/package-source-files-recipe.md)。

## 匯入方式

>[!NOTE]
>本教學課程要求您具有Docker源檔案URL。 如果您 [沒有Docker來源檔案URL](../data-science-workspace/models-recipes/package-source-files-recipe.md) ，請造訪套件來源檔案至配方教學課程。

匯入方式教學課程提供如何設定和匯入封裝方式的深入資訊。 在本教學課程結束時，您可以在Adobe Experience Platform資料科學工作區中建立、訓練和評估模型。

**本教學課程將協助您：**
- 為方式建立一組設定。
- 匯入Python、R、PySpark或Scala(Spark)的Docker配方。

若要進一步瞭解，請依照匯入封裝的方式 [UI教學課程](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) 或 [API教學課程](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)。

## 訓練和評估模型

在Adobe Experience Platform Data Science Workspace中，機器學習模型是透過整合符合模型意圖的現有配方來建立的。 然後，對模型進行訓練和評估，通過微調其相關的超參數來優化其操作效率和效能。 方式可重複使用，這表示您可以使用單一方式，針對特定目的建立並量身打造多個模型。

**本教學課程將協助您：**
- 建立新模型。
- 為模型建立訓練執行。
- 評估您的模型訓練執行。

若要開始，請依照訓練和評估模型 [API教學課程](../data-science-workspace/models-recipes/train-evaluate-model-api.md) 或 [UI教學課程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

## 使用Model Insights框架優化模型

模型洞察框架為資料科學家提供Adobe Experience Platform Data Science Workspace中的工具，讓他們快速且知情地選擇以實驗為基礎的最佳機器學習模型。 該框架將提高機器學習工作流程的速度和效率，並改善資料科學家的使用便利性。 這是透過為每個機器學習演算法類型提供預設範本來協助模型調整來完成。 最終結果使資料科學家和公民資料科學家能夠為其最終客戶做出更好的模型優化決策。

**本教學課程將協助您：**
- 設定方式代碼。
- 定義自訂量度。
- 使用預先建立的評估度量和視覺化圖表。

若要開始，請依照最佳化模型 [的教學課程](../data-science-workspace/models-recipes/optimize-model.md)。

## 對模型評分

在Adobe Experience Platform Data Science Workspace中，將輸入資料輸入現有的訓練模型，即可獲得分數。 然後，將計分結果儲存並作為新批在指定的輸出資料集中查看。

**本教學課程將協助您：**
- 建立新的計分執行。
- 檢視您的計分結果。

若要開始，請依照模型 [API教學課程或](../data-science-workspace/models-recipes/score-model-api.md)[UI教學課程的分數](../data-science-workspace/models-recipes/score-model-ui.md)。

## 將模型發佈為服務

Adobe Experience Platform Data Science Workspace可讓您將模型發佈為服務，讓IMS組織中的使用者可對資料評分，而不需建立自己的模型。 您可使用使用者介 [!DNL Platform] 面或Sensei Machine Learning API來完成此作業。

**本教學課程將協助您：**
- 將模型發佈為服務。
- 透過服務收藏館使用服務對資料 [!DNL Platform] 評分。

若要開始，請依照發佈模型為服務 [API教學課程](../data-science-workspace/models-recipes/publish-model-service-api.md) 或 [UI教學課程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

## 排程模型的訓練和計分

Adobe Experience Platform Data Science Workspace可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分流程有助於透過追蹤資料中的模式，持續維持並改善服務的效率。

**本教學課程將協助您：**
- 設定排程計分
- 設定計畫培訓

若要開始，請依照排 [程模型UI教學課程](../data-science-workspace/models-recipes/schedule-models-ui.md)。

## 建立特徵管線

>[!NOTE]
>目前，功能管道僅能透過API使用。

Adobe Experience Platform可讓您透過Sensei機器學習架構執行階段，建立並建立自訂功能管道，以大規模執行功能工程。

**本指南將幫助您：**
- 實作功能管線類。
- 使用API建立功能管線引擎。

若要進一步瞭解，請造訪建立功 [能管道的教學課程](../data-science-workspace/authoring/feature-pipeline.md)。

## 建立即時機器學習應用程式(alpha)

在Hub和Thab上結合流暢的運算，可大幅 [!DNL Edge] 降低傳統上為超個人化體驗提供相關與回應的延遲。 因此，即時機器學習為同步決策提供極低的延遲。 例如轉換個人化網頁內容、呈現選件，以及折扣以減少客戶流失，同時提高網站商店的轉換率。

**本指南將幫助您：**
- 瞭解即時機器學習架構。
- 瞭解即時機器學習工作流程。
- 瞭解即時機器學習的目前功能。
- 提供建立您自己的即時機器學習模型的後續步驟。

若要進一步瞭解，請造 [訪即時機器學習總覽](../data-science-workspace/real-time-machine-learning/home.md)。