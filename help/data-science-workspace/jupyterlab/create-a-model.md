---
keywords: Experience Platform;JupyterLab；配方；筆記型電腦；Data Science Workspace；熱門主題；建立配方
solution: Experience Platform
title: 使用JupyterLab Notebooks建立模型
type: Tutorial
description: 本教學課程會逐步引導您使用JupyterLab筆記型電腦配方產生器範本，建立配方所需的步驟。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# 使用JupyterLab Notebooks建立模型

本教學課程會逐步引導您使用JupyterLab筆記型電腦方式產生器範本，建立模型的必要步驟。

## 引入的概念：

- **方式：** 配方是模型規範的Adobe術語，是代表特定機器學習、AI演算法或整合演算法、處理邏輯和設定的頂層容器，是建立和執行訓練模型所需的處理邏輯和配置。
- **模型：** 模型是機器學習方式的例項，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。
- **培訓：** 培訓是學習模式和從標籤資料中洞察資訊的過程。
- **分數：** 計分是使用經過訓練的模型，從資料產生深入分析的程式。

## 下載所需資產 {#assets}

繼續本教學課程之前，您必須先建立必要的結構描述和資料集。 請造訪 [建立Luma傾向模型結構和資料集](../models-recipes/create-luma-data.md) 下載所需資產並設定先決條件。

## 開始使用 [!DNL JupyterLab] 筆記型環境

您可在中從草稿開始建立方式 [!DNL Data Science Workspace]. 若要開始，請導覽至 [Adobe Experience Platform](https://platform.adobe.com) ，然後選取 **[!UICONTROL 筆記本]** 標籤。 要建立新筆記本，請從 [!DNL JupyterLab Launcher].

此 [!UICONTROL 方式產生器] 筆記型電腦可讓您在筆記本內運行培訓和計分運行。 這可讓您靈活變更 `train()` 和 `score()` 在訓練和計分資料上執行實驗之間的方法。 一旦您滿意訓練和計分的輸出，就可以建立配方，並進一步以模型形式發佈，使用配方來模型化功能。

>[!NOTE]
>
>此 [!UICONTROL 方式產生器] 筆記型電腦支援使用所有檔案格式，但當前建立方式功能僅支援 [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

選取 [!UICONTROL 方式產生器] 從啟動器開啟筆記本時，筆記本會在新頁簽中開啟。

在頂部的新筆記本頁簽中，工具欄載入包含三個附加操作 —  **[!UICONTROL 火車]**, **[!UICONTROL 分數]**，和 **[!UICONTROL 建立方式]**. 這些圖示只會顯示在 [!UICONTROL 方式產生器] 筆記本。 提供這些動作的詳細資訊 [在訓練和評分科](#training-and-scoring) 在筆記本中建立食譜之後。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 開始使用 [!UICONTROL 方式產生器] 筆記本

在提供的資產資料夾中，是Luma傾向模型 `propensity_model.ipynb`. 在JupyterLab中使用上載筆記本選項，上傳提供的型號並開啟筆記本。

![上傳筆記本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教學課程的其餘部分涵蓋在傾向模型筆記本中預先定義的下列檔案：

- [需求檔案](#requirements-file)
- [組態檔](#configuration-files)
- [訓練資料載入器](#training-data-loader)
- [計分資料載入器](#scoring-data-loader)
- [管線檔案](#pipeline-file)
- [求值器檔案](#evaluator-file)
- [資料保護程式檔案](#data-saver-file)

以下影片教學課程說明Luma傾向模型筆記型電腦：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 需求檔案 {#requirements-file}

要求檔案用於聲明要在模型中使用的附加庫。 如果有相依性，則可指定版本編號。 若要尋找其他程式庫，請造訪 [anaconda.org](https://anaconda.org). 若要了解如何設定需求檔案的格式，請造訪 [孔達](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). 已使用的主要程式庫清單包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您新增的程式庫或特定版本可能與上述程式庫不相容。 此外，如果您選擇手動建立環境檔案，則 `name` 不允許覆蓋欄位。

對於Luma傾向模型筆記型電腦，不需要更新要求。

### 組態檔 {#configuration-files}

組態檔， `training.conf` 和 `scoring.conf`，可用來指定您要用於訓練和計分以及新增超參數的資料集。 培訓和評分有不同的設定。

為了讓模型執行訓練，您必須提供 `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`，和 `tenantId`. 此外，為了進行計分，您必須提供 `scoringDataSetId`, `tenantId`，和 `scoringResultsDataSetId `.

若要尋找資料集和結構ID，請前往「資料」標籤 ![資料標籤](../images/jupyterlab/create-recipe/dataset-tab.png) 在筆記型電腦中（在資料夾表徵圖下）。 需要提供三個不同的資料集ID。 此 `scoringResultsDataSetId` 可用來儲存模型計分結果，且應為空資料集。 這些資料集是先前在 [必要資產](#assets) 步驟。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

可在 [Adobe Experience Platform](https://platform.adobe.com/) 在 **[結構](https://platform.adobe.com/schema)** 和 **[資料集](https://platform.adobe.com/dataset/overview)** 頁簽。

競爭之後，您的訓練和分數設定看起來應類似於下列螢幕截圖：

![配置](../images/jupyterlab/create-recipe/config.png)

依預設，當您訓練及對資料計分時，會為您設定下列設定參數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 了解訓練資料載入器 {#training-data-loader}

訓練資料載入器的目的是將用於建立機器學習模型的資料實例化。 訓練資料載入器通常會完成兩項任務：

- 從載入資料 [!DNL Platform]
- 資料準備與特徵工程

以下兩節將重複載入資料和資料準備。

### 載入資料 {#loading-data}

此步驟使用 [熊貓資料流](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 資料可從 [!DNL Adobe Experience Platform] 使用 [!DNL Platform] SDK(`platform_sdk`)，或從外部來源使用熊貓。 `read_csv()` 或 `read_json()` 函式。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部來源](#external-sources)

>[!NOTE]
>
>在方式產生器筆記型電腦中，資料會透過 `platform_sdk` 資料載入器。

### [!DNL Platform] SDK {#platform-sdk}

如需使用 `platform_sdk` 資料載入器，請造訪 [Platform SDK指南](../authoring/platform-sdk.md). 本教學課程提供有關建置驗證、資料基本讀取和資料基本寫入的資訊。

### 外部來源 {#external-sources}

本節說明如何將JSON或CSV檔案匯入Apcontis物件。 熊貓圖書館的官方檔案可在此找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 此 `data` 引數是CSV檔案的路徑。 此變數是從 `configProperties` 在 [上一節](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案匯入。 此 `data` 引數是CSV檔案的路徑。 此變數是從 `configProperties` 在 [上一節](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

現在，您的資料位於dataframe物件中，可在 [下一節](#data-preparation-and-feature-engineering).

## 訓練資料載入器檔案

在此範例中，資料是使用Platform SDK載入。 您可以加入行，將程式庫匯入頁面頂端：

`from platform_sdk.dataset_reader import DatasetReader`

然後，您就可以使用 `load()` 從 `trainingDataSetId` 如設定(`recipe.conf`)檔案。

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
>如 [配置檔案部分](#configuration-files)，當您使用從Experience Platform存取資料時，會為您設定下列設定參數 `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


現在有了資料，您就可以開始進行資料準備和功能工程。

### 資料準備與特徵工程 {#data-preparation-and-feature-engineering}

資料載入後，需要清理資料並進行資料準備。 在此範例中，模型的目標是預測客戶是否要訂購產品。 由於模型未查看特定產品，因此您不需要 `productListItems` 因此，欄會被捨棄。 接著，會捨棄僅包含單一值或單一欄中兩個值的其他欄。 在訓練模型時，請務必僅保留有助於預測目標的有用資料。

![資料準備範例](../images/jupyterlab/create-recipe/data_prep.png)

刪除任何不必要的資料後，您就可以開始進行功能工程。 此範例使用的示範資料不包含任何工作階段資訊。 通常，您會想要擁有特定客戶目前和過去工作階段的資料。 由於缺乏工作階段資訊，此範例會透過歷程標界來模擬目前和過去的工作階段。

![歷程分界](../images/jupyterlab/create-recipe/journey_demarcation.png)

標界完成後，會標示資料並建立歷程。

![為資料加上標籤](../images/jupyterlab/create-recipe/label_data.png)

接著，將特徵建立並分為過去和現在。 之後，系統會捨棄任何不必要的欄，讓您同時了解Luma客戶的過去和目前歷程。 這些歷程包含相關資訊，例如客戶是否購買了項目，以及他們在購買前所經歷的歷程。

![最後的訓練](../images/jupyterlab/create-recipe/final_journey.png)

## 計分資料載入器 {#scoring-data-loader}

載入資料以進行計分的程式與載入訓練資料類似。 仔細檢視程式碼，您就會看到除了 `scoringDataSetId` 在 `dataset_reader`. 這是因為訓練和計分都使用相同的Luma資料來源。

如果您想要使用不同的資料檔案進行訓練和計分，則訓練和計分資料載入器會分開。 這可讓您執行其他預先處理，例如視需要將訓練資料對應至您的分數資料。

## 管線檔案 {#pipeline-file}

此 `pipeline.py` 檔案包含訓練和計分的邏輯。

訓練的目的是使用訓練資料集中的功能和標籤來建立模型。 選取訓練模型後，您必須將x和y訓練資料集符合模型，而函式會傳回訓練的模型。

>[!NOTE]
> 
>功能是指機器學習模型用來預測標籤的輸入變數。

![def列車](../images/jupyterlab/create-recipe/def_train.png)

此 `score()` 函式應包含計分演算法並傳回測量，以指出模型執行的成功程度。 此 `score()` 函式使用計分資料集標籤和訓練的模型來產生一組預測特徵。 然後，會將這些預測值與計分資料集中的實際特徵進行比較。 在此範例中， `score()` 函式會使用經過訓練的模型，使用計分資料集的標籤來預測功能。 會傳回預計特徵。

![def分數](../images/jupyterlab/create-recipe/def_score.png)

## 求值器檔案 {#evaluator-file}

此 `evaluator.py` 檔案包含您如何評估受訓方式的邏輯，以及如何分割訓練資料。

### 分割資料集 {#split-the-dataset}

訓練的資料準備階段需要分割要用於訓練和測試的資料集。 此 `val` 資料在訓練後被隱式用於評估模型。 此程式與計分不同。

本節顯示 `split()` 函式，可將資料載入筆記本中，然後移除資料集中不相關的欄，以清除資料。 從那裡，您可以執行特徵工程，即從資料中的現有原始特徵建立其他相關特徵的過程。

![拆分函式](../images/jupyterlab/create-recipe/split.png)

### 評估已訓練的模型 {#evaluate-the-trained-model}

此 `evaluate()` 函式會在模型訓練後執行，並傳回量度以指出模型執行的成功程度。 此 `evaluate()` 函式會使用測試資料集標籤和訓練的模型來預測一組功能。 然後，會將這些預測值與測試資料集中的實際功能進行比較。 在此範例中，使用的量度為 `precision`, `recall`, `f1`，和 `accuracy`. 請注意，函式會傳回 `metric` 包含評估度量陣列的物件。 這些量度可用來評估訓練後模型的成效。

![評估](../images/jupyterlab/create-recipe/evaluate.png)

新增 `print(metric)` 可讓您檢視量度結果。

![量度結果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 資料保護程式檔案 {#data-saver-file}

此 `datasaver.py` 檔案包含 `save()` 函式和，可在測試計分時儲存您的預測。 此 `save()` 函式會擷取您的預測，並使用 [!DNL Experience Platform Catalog] API會將資料寫入 `scoringResultsDataSetId` 在 `scoring.conf` 檔案。 您可以

![資料保護程式](../images/jupyterlab/create-recipe/data_saver.png)

## 訓練和評分 {#training-and-scoring}

完成對筆記本的更改並想要培訓配方時，您可以選擇欄頂部的相關按鈕，以在單元格中建立培訓運行。 選擇按鈕後，來自培訓指令碼的命令和輸出日誌將出現在筆記本中(位於 `evaluator.py` 儲存格)。 Conda首先安裝所有依賴項，然後啟動培訓。

請注意，必須至少運行一次培訓才能運行計分。 選取 **[!UICONTROL 運行計分]** 按鈕會在訓練期間產生的訓練模型上評分。 計分指令碼顯示在 `datasaver.py`.

為偵錯之用，如果您想查看隱藏的輸出，請新增 `debug` 到輸出單元格的結尾，然後重新運行。

![訓練和分數](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 建立方式 {#create-recipe}

完成編輯配方並滿足培訓/評分輸出後，您可以通過選擇 **[!UICONTROL 建立方式]** 在右上角。

![](../images/jupyterlab/create-recipe/create-recipe.png)

選取後 **[!UICONTROL 建立方式]**，系統會提示您輸入方式名稱。 此名稱代表建立於的實際方式 [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

選取 **[!UICONTROL 確定]**，方式建立程式就會開始。 這可能需要一些時間，而且會顯示進度列來取代建立方式按鈕。 完成後，您可以選取 **[!UICONTROL 檢視方式]** 按鈕 **[!UICONTROL 訣竅]** 標籤 **[!UICONTROL ML模型]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 請勿刪除任何檔案儲存格
> - 請勿編輯 `%%writefile` 行（位於檔案單元格的頂部）
> - 請勿同時在不同的筆記型電腦中建立配方


## 後續步驟 {#next-steps}

完成本教學課程後，您已學習如何在 [!UICONTROL 方式產生器] 筆記本。 您還學習了如何練習筆記型電腦以指導工作流程。

繼續學習如何在內使用資源 [!DNL Data Science Workspace]，請造訪 [!DNL Data Science Workspace] 方式和模型下拉式清單。