---
keywords: Experience Platform；首頁；熱門主題；dsw;DSW
solution: Experience Platform
title: 資料科學工作區教學課程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform資料科學工作區使用機器學習和人工智慧從您的資料中建立見解。 Data Science Workspace整合至Adobe Experience Platform，可協助您跨Adobe解決方案使用內容和資料資產進行預測。
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 教學課程

Adobe Experience Platform[!DNL Data Science Workspace]使用機器學習和人工智慧從您的資料中建立見解。 [!DNL Data Science Workspace]已整合至Adobe Experience Platform，可協助您跨Adobe解決方案使用內容和資料資產進行預測。 所有技能等級的資料科學家都擁有複雜、簡單易用的工具，可支援快速開發、訓練和調整機器學習方式- AI技術的所有優點，而不需複雜。

若要進一步瞭解，請先閱讀[資料科學工作區概觀](../data-science-workspace/home.md)。

## [!DNL Sensei Machine Learning] API

[!DNL Sensei Machine Learning] API為資料科學家提供機制，以組織和管理機器學習服務，從演算法上線到實驗，再到服務部署。

**目前提供下列API開發人員指南：**
- [引擎](../data-science-workspace/api/engines.md) -瞭解如何查找註冊表、 [!DNL Docker] 建立引擎、建立功能管線引擎、擷取引擎的資訊、更新引擎以及刪除引擎。
- [MLInstances（方式）](../data-science-workspace/api/mlinstances.md) -瞭解如何建立MLInstance、擷取MLInstance的資訊、更新MLInstance，以及刪除MLInstance。
- [實驗](../data-science-workspace/api/experiments.md) -瞭解如何建立實驗、擷取實驗或實驗執行資訊、更新實驗及刪除實驗。
- [模型](../data-science-workspace/api/models.md) -瞭解如何註冊自己的模型、擷取模型的資訊、更新模型、刪除模型、建立模型的新轉碼，以及擷取轉碼模型的詳細資訊。
- [MLServices](../data-science-workspace/api/mlservices.md)  —— 瞭解如何建立MLService、擷取MLService的資訊、更新MLService，以及刪除MLService。
- [前瞻分析](../data-science-workspace/api/insights.md) -瞭解如何擷取前瞻分析的資訊、新增模型前瞻分析，以及擷取演算法的預設度量清單。

若要進一步瞭解並取得使用Sensei Machine Learning API執行CRUD作業所需的值，請造訪[快速入門手冊](../data-science-workspace/api/getting-started.md)。

## 如何使用[!DNL JupyterLab]筆記本

[!DNL JupyterLab] 是網路使用者介面， [!DNL Project Jupyter] 與Adobe Experience Platform緊密整合。它為資料科學家提供互動式開發環境，以便與[!DNL Jupyter Notebooks]、程式碼和資料搭配使用。 本檔案概述[!DNL JupyterLab]及其功能，以及執行常見動作的指示。

**本指南將幫助您：**
- 訪問並瞭解[!DNL JupyterLab]介面。
- 瞭解[!DNL JupyterLab]中的代碼單元格和可用內核。
- 瞭解[!DNL Python]/R中的GPU和記憶體伺服器組態。

如需詳細資訊，請造訪[JupyterLab使用指南](../data-science-workspace/jupyterlab/overview.md)。

## JupyterLab筆記型電腦中的資料存取

Data Science Workspace中的JupyterLab目前支援[!DNL Python]、R、PySpark和Scala的筆記型電腦。 每個支援的內核都提供內置功能，允許您從筆記本內的資料集中讀取平台資料。 但是，對分頁資料的支援僅限於[!DNL Python]和R筆記本。 本指南重點介紹如何使用JupyterLab筆記型電腦訪問資料。

**本指南將幫助您：**
- 使用Python、R、PySpark或Scala筆記型電腦讀取、寫入和查詢平台資料。
- 瞭解每種筆記本類型的讀取限制。

如需詳細資訊，請造訪[JupyterLab筆記型電腦資料存取開發人員指南](../data-science-workspace/jupyterlab/access-notebook-data.md)

## 封裝用於[!DNL Docker]配方製作的來源檔案

[!DNL Docker]影像可讓您封裝應用程式並包含其所需的所有部件。 這包括一個軟體包中的所有庫和其他相關性。 內建的[!DNL Docker]影像會在配方建立工作流程中使用提供給您的憑證推送至[!DNL Azure Container Registry]。

**本教學課程將協助您：**
- 下載建立方式的必要先決條件。
- 瞭解以[!DNL Docker]為基礎的模型製作。
- 建立[!DNL Python]、R、PySpark或Scala([!DNL Spark])的[!DNL Docker]影像。
- 取得[!DNL Docker]來源檔案URL。

若要進一步瞭解，請依照[封裝來源檔案至配方教學課程](../data-science-workspace/models-recipes/package-source-files-recipe.md)。

## 匯入方式

>[!NOTE]
>
>本教學課程要求您具有[!DNL Docker]來源檔案URL。 如果您沒有[!DNL Docker]來源檔案URL，請造訪[將來源檔案封裝成配方教學課程](../data-science-workspace/models-recipes/package-source-files-recipe.md)。

匯入方式教學課程提供如何設定和匯入封裝方式的深入資訊。 在本教學課程結束時，您可以在Adobe Experience Platform[!DNL Data Science Workspace]中建立、訓練和評估模型。

**本教學課程將協助您：**
- 為方式建立一組設定。
- 匯入[!DNL Python]、R、PySpark或Scala([!DNL Spark])的[!DNL Docker]基礎配方。

若要進一步瞭解，請依照匯入封裝方式[UI教學課程](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md)或[API教學課程](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)進行。

## 訓練和評估模型

在Adobe Experience Platform[!DNL Data Science Workspace]中，機器學習模型是通過結合適合模型意圖的現有配方來建立的。 然後，對模型進行訓練和評估，通過微調其相關的超參數來優化其操作效率和效能。 方式可重複使用，這表示您可以使用單一方式，針對特定目的建立並量身打造多個模型。

**本教學課程將協助您：**
- 建立新模型。
- 為模型建立訓練執行。
- 評估您的模型訓練執行。

若要開始，請依照訓練並評估模型[API教學課程](../data-science-workspace/models-recipes/train-evaluate-model-api.md)或[UI教學課程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

## 使用Model Insights框架優化模型

模型洞察框架為資料科學家提供了Adobe Experience Platform[!DNL Data Science Workspace]的工具，以便快速、明智地選擇基於實驗的最佳機器學習模型。 該框架將提高機器學習工作流程的速度和效率，並改善資料科學家的使用便利性。 這是透過為每個機器學習演算法類型提供預設範本來協助模型調整來完成。 最終結果使資料科學家和公民資料科學家能夠為其最終客戶做出更好的模型優化決策。

**本教學課程將協助您：**
- 設定方式代碼。
- 定義自訂量度。
- 使用預先建立的評估度量和視覺化圖表。

要開始，請遵循[優化模型](../data-science-workspace/models-recipes/optimize-model.md)的教程。

## 對模型評分

將輸入資料輸入到現有的訓練模型中，可以在Adobe Experience Platform獲得[!DNL Data Science Workspace]評分。 然後，將計分結果儲存並作為新批在指定的輸出資料集中查看。

**本教學課程將協助您：**
- 建立新的計分執行。
- 檢視您的計分結果。

若要開始，請依照[模型API教學課程](../data-science-workspace/models-recipes/score-model-api.md)或[UI教學課程](../data-science-workspace/models-recipes/score-model-ui.md)的分數進行。

## 將模型發佈為服務

Adobe Experience Platform[!DNL Data Science Workspace]可讓您將模型發佈為服務，讓IMS組織內的使用者可對資料進行分數，而不需建立自己的模型。 這可以使用[!DNL Platform]使用者介面或[!DNL Sensei Machine Learning] API來完成。

**本教學課程將協助您：**
- 將模型發佈為服務。
- 使用透過[!DNL Platform] [!UICONTROL Service Gallery]的服務對資料進行分數。

若要開始，請依照[API教學課程](../data-science-workspace/models-recipes/publish-model-service-api.md)或[UI教學課程](../data-science-workspace/models-recipes/publish-model-service-ui.md)的形式發佈模型。

## 排程模型的訓練和計分

Adobe Experience Platform[!DNL Data Science Workspace]可讓您在機器學習服務上設定排程的分數和訓練執行。 自動化培訓和計分流程有助於透過追蹤資料中的模式，持續維持並改善服務的效率。

**本教學課程將協助您：**
- 設定排程計分
- 設定計畫培訓

若要開始，請依照[排程模型UI教學課程](../data-science-workspace/models-recipes/schedule-models-ui.md)。

## 建立特徵管線

>[!NOTE]
>
>目前，功能管道僅能透過API使用。

Adobe Experience Platform允許您通過[!DNL Sensei Machine Learning Framework Runtime]構建和建立定制特徵管線，以大規模執行特徵工程。

**本指南將幫助您：**
- 實作功能管線類。
- 使用API建立功能管線引擎。

若要進一步瞭解，請造訪[建立功能管線](../data-science-workspace/authoring/feature-pipeline.md)的教學課程。

## 建立[!DNL Real-Time Machine Learning]應用程式(alpha)

在集線器和[!DNL Edge]上結合流暢的運算，可大幅降低傳統上為相關且回應速度快的個人化體驗提供動力時的延遲。 因此，[!DNL Real-time Machine Learning]為同步決策提供極低延遲的推論。 例如轉換個人化網頁內容、呈現選件，以及折扣以減少客戶流失，同時提高網站商店的轉換率。

**本指南將幫助您：**
- 瞭解[!DNL Real-time Machine Learning]架構。
- 瞭解[!DNL Real-time Machine Learning]工作流程。
- 瞭解[!DNL Real-time Machine Learning]的目前功能。
- 提供建立您自己的[!DNL Real-time Machine Learning model]的後續步驟。

若要進一步瞭解，請造訪[即時機器學習概觀](../data-science-workspace/real-time-machine-learning/home.md)。
