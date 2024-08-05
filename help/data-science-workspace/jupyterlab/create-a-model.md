---
keywords: Experience Platform;JupyterLab;食譜;筆記本;數據科學工作環境;熱門話題;建立方式
solution: Experience Platform
title: 使用JupyterLab Notebooks建立模型
type: Tutorial
description: 本教學課程將逐步引導您完成使用JupyterLab Notebooks配方產生器範本建立配方所需的步驟。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 0%

---

# 使用JupyterLab Notebooks建立模型

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

本教學課程將逐步引導您完成使用JupyterLab Notebooks配方產生器範本建立模型的必要步驟。

## 引入的概念：

- **配方：**&#x200B;配方是模型規格的Adobe術語，是代表特定機器學習、AI演演算法或演演算法組合、處理邏輯以及建立和執行已訓練模型所需設定的頂層容器。
- **模型：**&#x200B;模型是機器學習方法的執行個體，其使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。
- **訓練：**&#x200B;訓練是從標籤資料中學習模式和深入分析的程式。
- **評分：**&#x200B;評分是使用經過訓練的模型，從資料產生深入分析的程式。

## 下載必要的資產 {#assets}

繼續進行本教學課程之前，您必須建立必要的結構和資料集。 造訪有關[建立Luma傾向模型結構描述和資料集](../models-recipes/create-luma-data.md)的教學課程，以下載必要的資產和設定必要條件。

## 開始使用[!DNL JupyterLab]筆記本環境

從頭開始建立配方可以在[!DNL Data Science Workspace]內完成。 若要開始，請導覽至[Adobe Experience Platform](https://platform.adobe.com)，然後選取左側的&#x200B;**[!UICONTROL 筆記本]**&#x200B;索引標籤。 若要建立新的筆記本，請從[!DNL JupyterLab Launcher]選取「配方產生器」範本。

[!UICONTROL 配方產生器]筆記本可讓您在筆記本內執行訓練和評分回合。 這可讓您在執行訓練和評分資料的實驗之間，靈活地變更其`train()`和`score()`方法。 當您對訓練和評分的輸出感到滿意後，就可以建立配方，並使用配方來模型化功能，進而將其發佈為模型。

>[!NOTE]
>
>[!UICONTROL 配方產生器]筆記本支援使用所有檔案格式，但目前建立配方功能僅支援[!DNL Python]。

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

當您從啟動器選取[!UICONTROL 配方產生器]筆記本時，會在新索引標籤中開啟筆記本。

在頂端的新筆記本標籤中，載入包含三個額外動作的工具列 — **[!UICONTROL 訓練]**、**[!UICONTROL 分數]**&#x200B;和&#x200B;**[!UICONTROL 建立配方]**。 這些圖示只會顯示在[!UICONTROL 配方產生器]筆記本中。 在記事本中建置您的配方後，[在訓練與評分割槽段](#training-and-scoring)中提供這些動作的詳細資訊。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## [!UICONTROL 開始使用配方生成器]筆記本

在提供的資產資料夾中為Luma傾向模型`propensity_model.ipynb`。 使用JupyterLab中的上傳筆記本選項，上傳提供的型號並開啟筆記本。

![上傳筆記本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教學課程的其餘部分涵蓋下列在傾向性模型筆記本中預先定義的檔案：

- [需求檔案](#requirements-file)
- [配置檔案](#configuration-files)
- [訓練數據載入程式](#training-data-loader)
- [評分數據載入程式](#scoring-data-loader)
- [管道檔案](#pipeline-file)
- [求值器檔案](#evaluator-file)
- [流量節省程式檔案](#data-saver-file)

以下影片教學課程說明 Luma 傾向模型筆記本：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 需求檔案 {#requirements-file}

需求檔案用於宣告您要在模型中使用的其他程式庫。 如果有相依性，您可以指定版本編號。 若要尋找其他資料庫，請造訪[anaconda.org](https://anaconda.org)。 若要瞭解如何格式化需求檔案，請造訪[Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually)。 已使用的主要程式庫清單包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您添加的庫或特定版本可能與上述資料庫不相容。 此外，如果您選擇手動建立環境檔案，則不允許覆寫`name`欄位。

對於Luma傾向性機型筆記型電腦，不需要更新需求。

### 組態檔 {#configuration-files}

組態檔`training.conf`和`scoring.conf`是用來指定您要用來訓練和評分以及新增超引數的資料集。 培訓和評分有不同的設定。

為了使模型培訓運行，必須提供 `trainingDataSetId`、 `ACP_DSW_TRAINING_XDM_SCHEMA`和 `tenantId`。 此外，對於評分，必須提供 `scoringDataSetId`、 `tenantId`和 `scoringResultsDataSetId `。

若要查找資料集 ID 和綱要 ID，請轉到左側導覽欄（資料夾圖示下）筆記本中的數據標籤 ![“數據標籤](../images/jupyterlab/create-recipe/dataset-tab.png) ”。 需提供三種不同的 資料集 ID。 用於 `scoringResultsDataSetId` 商店模型評分結果，應為空資料集。 這些數據集之前已在必需 [資產](#assets) 步驟中創建。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

可以在Adobe Experience Platform架構和&#x200B;**[數據集**](https://platform.adobe.com/dataset/overview)選項卡下&#x200B;**[找到[相同的資訊。](https://platform.adobe.com/)**](https://platform.adobe.com/schema)

比賽結束后，您的培訓和得分配置應類似於以下螢幕擷圖：

![配置](../images/jupyterlab/create-recipe/config.png)

預設情況下，在訓練和評分數據時會為您設置以下配置參數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 了解訓練數據載入程式 {#training-data-loader}

訓練數據載入程式的目的是實例化用於創建機器學習模型的數據。 通常，訓練資料載入程序會完成兩項任務：

- 正在從[!DNL Platform]載入資料
- 資料準備和功能工程

以下兩節將介紹如何載入數據和準備數據。

### 載入數據 {#loading-data}

此步驟使用 [pandas 數據幀](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)。 可以使用 SDK （`platform_sdk`） 從[!DNL Platform][!DNL Adobe Experience Platform]檔案載入資料，也可以使用 pandas&#39; `read_csv()` or `read_json()` 函數從外部源載入數據。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部來源](#external-sources)

>[!NOTE]
>
>在配方產生器筆記本中，資料是透過`platform_sdk`資料載入器載入。

### [!DNL Platform] SDK {#platform-sdk}

如需有關使用`platform_sdk`資料載入器的深入教學課程，請造訪[Platform SDK指南](../authoring/platform-sdk.md)。 本教學課程提供有關建置驗證、基本讀取資料和基本寫入資料的資訊。

### 外部來源 {#external-sources}

本節說明如何將JSON或CSV檔案匯入熊貓物件。 熊貓資料庫的官方檔案可在以下網址找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 `data`引數是CSV檔案的路徑。 此變數是從[上一節](#configuration-files)中的`configProperties`匯入。

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案匯入。 `data`引數是CSV檔案的路徑。 此變數是從[上一節](#configuration-files)中的`configProperties`匯入。

```PYTHON
df = pd.read_json(data)
```

現在您的資料在資料流物件中，可以在[下一個區段](#data-preparation-and-feature-engineering)中分析和操作。

## 訓練資料載入器檔案

在此範例中，資料是使用Platform SDK載入。 您可以包含行來在頁面頂端匯入程式庫：

`from platform_sdk.dataset_reader import DatasetReader`

然後，您可以使用`load()`方法，從設定(`recipe.conf`)檔案中所設定的`trainingDataSetId`抓取訓練資料集。

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>如[組態檔區段](#configuration-files)中所述，當您使用`client_context = get_client_context(config_properties)`從Experience Platform存取資料時，會為您設定下列組態引數：
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`

現在您有了資料，就可以開始資料準備和功能工程了。

### 資料準備和功能工程 {#data-preparation-and-feature-engineering}

載入資料後，需要清理資料並做好資料準備。 在此範例中，模型的目標是預測客戶是否會訂購產品。 因為模型未檢視特定產品，所以您不需要`productListItems`，因此會捨棄該欄。 接著，會捨棄只包含單一值或單一欄中兩個值的其他欄。 培訓模型時，請務必僅保留有助於預測目標的有用數據。

![資料準備的範例](../images/jupyterlab/create-recipe/data_prep.png)

一旦您刪除了任何不必要的資料，就可以開始特徵工程。 用於此範例的示範資料不包含任何工作階段資訊。 通常情況下，您會想要取得特定客戶目前和過去工作階段的資料。 由於缺少工作階段資訊，此範例改為透過歷程分界來模擬目前和過去的工作階段。

![歷程分界](../images/jupyterlab/create-recipe/journey_demarcation.png)

劃界完成後，將標記數據並創建歷程。

![為資料加上標籤](../images/jupyterlab/create-recipe/label_data.png)

接著會建立特徵，並分成過去和現在。 接著，所有不必要的欄都會被捨棄，留下Luma客戶的過去和目前歷程。 這些歷程包含一些資訊，例如客戶是否購買了一個專案，以及他們購買之前所經歷的歷程。

![目前的最終訓練](../images/jupyterlab/create-recipe/final_journey.png)

## 評分資料載入器 {#scoring-data-loader}

載入資料以進行評分的程式與載入訓練資料類似。 仔細檢視程式碼，您會發現除了`dataset_reader`中的`scoringDataSetId`以外，其他所有專案都相同。 這是因為訓練和評分都使用相同的Luma資料來源。

如果您想要使用不同的資料檔案進行訓練和評分，訓練和評分資料載入器是分開的。 這可讓您執行其他預先處理，例如視需要將您的訓練資料對應至您的評分資料。

## 管道檔案 {#pipeline-file}

`pipeline.py`檔案包含訓練和評分的邏輯。

培訓的目的是使用培訓 資料集中的特徵和標註創建模型。 選擇訓練模型後，您必須將x和y訓練資料集調整為適合模型，此函式會傳回經過訓練的模型。

>[!NOTE]
> 
>功能是指機器學習模型用來預測標籤的輸入變數。

![def列車](../images/jupyterlab/create-recipe/def_train.png)

`score()`函式應包含評分演演算法，並傳回測量以指出模型執行的成功程度。 `score()`函式使用評分資料集標籤和訓練的模型來產生一組預測功能。 然後，將這些預測值與評分資料集中的實際功能進行比較。 在此示例中，該 `score()` 函數使用經過訓練的模型，使用評分資料集中的標籤來預測特徵。 將返回預測要素。

![定義分數](../images/jupyterlab/create-recipe/def_score.png)

## 求值器檔案 {#evaluator-file}

該文件 `evaluator.py` 包含您希望如何評估已訓練方式以及如何拆分訓練資料的邏輯。

### 拆分資料集 {#split-the-dataset}

培訓 的數據準備階段需要拆分要用於培訓和測試的資料集。 此 `val` 數據在訓練模型后隱式用於評估模型。 此過程與評分分開。

本部分顯示將數據 `split()` 載入到筆記本，然後通過刪除資料集中不相關的列來清理數據的函數。 從那裡，您可以執行特徵工程，這是從數據中的現有原始特徵創建其他相關特徵的過程。

![分體功能](../images/jupyterlab/create-recipe/split.png)

### 評估經過訓練的模型 {#evaluate-the-trained-model}

`evaluate()`函式會在模型訓練後執行，並傳回量度以指出模型執行的成功程度。 `evaluate()`函式使用測試資料集標籤和訓練好的模型來預測一組功能。 然後將這些預測值與測試資料集中的實際特徵進行比較。 在這裡範例中，使用的量度為 `precision`、 `recall`、 `f1`和 `accuracy`。 請注意，該函數返回一個 `metric` 包含評估指標數位的物件。 這些指標用於評估經過訓練的模型的性能。

![評價](../images/jupyterlab/create-recipe/evaluate.png)

新增 `print(metric)` 可讓您視圖量度結果。

![個量度結果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 資料儲存器檔案 {#data-saver-file}

`datasaver.py`檔案包含`save()`函式，用來在測試評分時儲存您的預測。 `save()`函式接受您的預測，並使用[!DNL Experience Platform Catalog] API，將資料寫入您在`scoring.conf`檔案中指定的`scoringResultsDataSetId`。 您可以

![資料儲存器](../images/jupyterlab/create-recipe/data_saver.png)

## 訓練和評分 {#training-and-scoring}

當您完成筆記本的變更並想要訓練您的配方時，您可以選取列頂端的關聯按鈕，以在儲存格中建立訓練回合。 選取按鈕後，訓練指令碼的命令和輸出記錄會顯示在記事本中（在`evaluator.py`儲存格下）。 Conda會先安裝所有相依性，然後開始培訓。

請注意，您必須至少執行一次訓練，才能執行評分。 選取&#x200B;**[!UICONTROL 執行評分]**&#x200B;按鈕將會在訓練期間產生的已訓練模型上評分。 評分指令碼會顯示在`datasaver.py`下方。

為了偵錯，如果您想要檢視隱藏的輸出，請將`debug`新增到輸出儲存格的結尾並重新執行。

![訓練與分數](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 建立配方 {#create-recipe}

當您編輯完配方並滿意訓練/評分輸出時，您可以選取右上方的&#x200B;**[!UICONTROL 建立配方]**，從筆記本建立配方。

![](../images/jupyterlab/create-recipe/create-recipe.png)

選取&#x200B;**[!UICONTROL 建立配方]**&#x200B;後，系統會提示您輸入配方名稱。 此名稱代表在[!DNL Platform]上建立的實際配方。

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

選擇「 **[!UICONTROL 確定]**」後，方式創建過程將開始。 這可能需要一些時間，並且會顯示進度列來取代建立配方按鈕。 完成後，您可以選取&#x200B;**[!UICONTROL 檢視配方]**&#x200B;按鈕，帶您進入&#x200B;**[!UICONTROL ML模型]**&#x200B;下的&#x200B;**[!UICONTROL 配方]**&#x200B;標籤

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 請勿刪除任何檔案儲存格
> - 不要編輯檔案儲存格頂端的`%%writefile`行
> - 不要同時在不同筆記型電腦中建立配方

## 後續步驟 {#next-steps}

完成此教學課程後，您已瞭解如何在[!UICONTROL 配方產生器]筆記本中建立機器學習模型。 您也已瞭解如何練習將筆記本設為配方工作流程。

若要繼續瞭解如何使用[!DNL Data Science Workspace]中的資源，請造訪[!DNL Data Science Workspace]配方和模型下拉式清單。