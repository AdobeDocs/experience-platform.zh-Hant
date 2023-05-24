---
keywords: Experience Platform;JupyterLab;recipe;notes;Data Science Workspace；熱門主題；建立配方
solution: Experience Platform
title: 使用JupyterLab筆記本建立模型
type: Tutorial
description: 本教程將指導您完成使用JupyterLab筆記本配方生成器模板建立配方所需的步驟。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# 使用JupyterLab筆記本建立模型

本教程將指導您完成使用JupyterLab筆記本配方生成器模板建立模型所需的步驟。

## 引入的概念：

- **配方：** 配方是模型規範的Adobe術語，是表示構建和執行訓練模型所需的特定機器學習、AI算法或算法、處理邏輯和配置的整合的頂級容器。
- **型號：** 模型是使用歷史資料和配置進行訓練以針對業務使用案例解決的機器學習配方的實例。
- **培訓：** 培訓是從標籤資料中學習模式和洞察力的過程。
- **評分：** 評分是使用訓練好的模型從資料生成洞見的過程。

## 下載所需資產 {#assets}

在繼續本教程之前，必須建立所需的架構和資料集。 訪問教程 [建立Luma傾向模型模式和資料集](../models-recipes/create-luma-data.md) 下載所需資產並設定前提條件。

## 開始使用 [!DNL JupyterLab] 筆記本環境

從頭開始建立處方可在 [!DNL Data Science Workspace]。 要開始，請導航到 [Adobe Experience Platform](https://platform.adobe.com) 的 **[!UICONTROL 筆記本]** 按鈕。 要建立新筆記本，請從 [!DNL JupyterLab Launcher]。

的 [!UICONTROL 處方生成器] 筆記本允許您在筆記本內運行培訓和評分運行。 這樣，您就可以靈活地更改 `train()` 和 `score()` 在訓練和打分資料之間進行實驗的方法。 一旦您對培訓和評分的輸出感到滿意，您就可以建立處方，並且使用處方將其發佈為模型以建模功能。

>[!NOTE]
>
>的 [!UICONTROL 處方生成器] 筆記本支援使用所有檔案格式，但當前建立處方功能僅支援 [!DNL Python]。

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

選擇 [!UICONTROL 處方生成器] 從啟動器開啟筆記本時，將在新頁籤中開啟筆記本。

在頂部的新筆記本頁籤中，一個工具欄載入包含三個附加操作 —  **[!UICONTROL 火車]**。 **[!UICONTROL 得分]**, **[!UICONTROL 建立處方]**。 這些表徵圖僅出現在 [!UICONTROL 處方生成器] 筆記本。 提供了有關這些操作的詳細資訊 [在訓練和評分部](#training-and-scoring) 在筆記本里製作食譜。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 開始使用 [!UICONTROL 處方生成器] 筆記本

在提供的資產資料夾中是Luma傾向模型 `propensity_model.ipynb`。 使用JupyterLab中的上載筆記本選項，上載提供的型號並開啟筆記本。

![上載筆記本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教程的其餘部分包括在傾向模型筆記本中預定義的下列檔案：

- [要求檔案](#requirements-file)
- [配置檔案](#configuration-files)
- [培訓資料載入器](#training-data-loader)
- [計分資料載入器](#scoring-data-loader)
- [管道檔案](#pipeline-file)
- [計算器檔案](#evaluator-file)
- [資料保護程式檔案](#data-saver-file)

以下視頻教程介紹了Luma傾向模型筆記本：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 要求檔案 {#requirements-file}

要求檔案用於聲明要在模型中使用的附加庫。 如果存在依賴關係，則可以指定版本號。 要查找其他庫，請訪問 [阿納康達組織](https://anaconda.org)。 要瞭解如何格式化要求檔案，請訪問 [孔達](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually)。 已在使用的主庫清單包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>添加的庫或特定版本可能與上述庫不相容。 此外，如果您選擇手動建立環境檔案， `name` 不允許覆蓋欄位。

對於Luma傾向型筆記本，不需要更新要求。

### 配置檔案 {#configuration-files}

配置檔案， `training.conf` 和 `scoring.conf`，用於指定要用於培訓和評分以及添加超參數的資料集。 培訓和評分有單獨的配置。

要使模型運行培訓，必須提供 `trainingDataSetId`。 `ACP_DSW_TRAINING_XDM_SCHEMA`, `tenantId`。 此外，要進行計分，必須提供 `scoringDataSetId`。 `tenantId`, `scoringResultsDataSetId `。

要查找資料集和架構ID，請轉到資料頁籤 ![「資料」頁籤](../images/jupyterlab/create-recipe/dataset-tab.png) 在左導航欄的筆記本中（資料夾表徵圖下）。 需要提供三個不同的資料集ID。 的 `scoringResultsDataSetId` 用於儲存模型計分結果，並且應為空資料集。 這些資料集以前在 [必需資產](#assets) 的子菜單。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

可在 [Adobe Experience Platform](https://platform.adobe.com/) 下 **[架構](https://platform.adobe.com/schema)** 和 **[資料集](https://platform.adobe.com/dataset/overview)** 頁籤。

競爭後，您的培訓和評分配置應與以下螢幕截圖類似：

![配置](../images/jupyterlab/create-recipe/config.png)

預設情況下，在訓練和計分資料時會為您設定以下配置參數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 瞭解培訓資料載入器 {#training-data-loader}

訓練資料載入器的目的是實例化用於建立機器學習模型的資料。 通常，培訓資料載入器可完成以下兩個任務：

- 從載入資料 [!DNL Platform]
- 資料準備和特徵工程

以下兩節將重新載入資料和準備資料。

### 正在載入資料 {#loading-data}

此步驟使用 [熊貓資料幀](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)。 可以從中的檔案載入資料 [!DNL Adobe Experience Platform] 使用 [!DNL Platform] SDK(`platform_sdk`)，或從外部來源使用熊貓。 `read_csv()` 或 `read_json()` 的子菜單。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部源](#external-sources)

>[!NOTE]
>
>在處方生成器筆記本中，通過 `platform_sdk` 資料載入器。

### [!DNL Platform] SDK {#platform-sdk}

有關使用的深入教程 `platform_sdk` 資料載入器，請訪問 [平台SDK指南](../authoring/platform-sdk.md)。 本教程提供有關生成驗證、基本資料讀取和基本資料寫入的資訊。

### 外部源 {#external-sources}

本節將介紹如何將JSON或CSV檔案導入到pactus對象。 熊貓圖書館的官方檔案如下：
- [讀取_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，這裡是導入CSV檔案的示例。 的 `data` 參數是CSV檔案的路徑。 此變數是從 `configProperties` 的 [上一節](#configuration-files)。

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案導入。 的 `data` 參數是CSV檔案的路徑。 此變數是從 `configProperties` 的 [上一節](#configuration-files)。

```PYTHON
df = pd.read_json(data)
```

現在，您的資料位於資料幀對象中，可以在 [下一部分](#data-preparation-and-feature-engineering)。

## 培訓資料載入器檔案

在本示例中，資料是使用平台SDK載入的。 通過包括以下行，可以在頁面頂部導入庫：

`from platform_sdk.dataset_reader import DatasetReader`

然後，您可以使用 `load()` 一種從訓練資料庫中提取訓練資料的方法 `trainingDataSetId` 在配置中設定(`recipe.conf`)。

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
>如 [「配置檔案」部分](#configuration-files)，當您使用Experience Platform訪問資料時，將為您設定以下配置參數 `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


現在您擁有了資料，您可以從資料準備和功能工程開始。

### 資料準備和特徵工程 {#data-preparation-and-feature-engineering}

資料載入後，需要對資料進行清理和資料準備。 在本示例中，模型的目標是預測客戶是否要訂購產品。 因為模型不查看特定產品，所以您不需要 `productListItems` 因此，該列被刪除。 接下來，刪除僅包含單個值或單個列中兩個值的附加列。 在訓練模型時，只保留有助於預測目標的有用資料非常重要。

![資料準備示例](../images/jupyterlab/create-recipe/data_prep.png)

一旦刪除了任何不必要的資料，就可以開始特徵工程。 此示例使用的演示資料不包含任何會話資訊。 通常，您希望為特定客戶提供有關當前會話和過去會話的資料。 由於缺乏會話資訊，本示例通過旅行標界模擬當前和過去的會話。

![旅行標界](../images/jupyterlab/create-recipe/journey_demarcation.png)

標定完成後，將標籤資料並建立行程。

![標籤資料](../images/jupyterlab/create-recipe/label_data.png)

然後，建立特徵並將其分為過去和現在。 然後，任何不必要的欄都會被刪除，這樣，Luma客戶就可以同時瞭解過去和當前的行程。 這些旅程包含諸如客戶是否購買了物料，以及在購買前所進行的旅程等資訊。

![最後一次](../images/jupyterlab/create-recipe/final_journey.png)

## 計分資料載入器 {#scoring-data-loader}

為評分載入資料的過程類似於載入訓練資料。 仔細看代碼，你可以看到除了 `scoringDataSetId` 的 `dataset_reader`。 這是因為同一Luma資料源用於訓練和評分。

如果您希望使用不同的資料檔案進行培訓和評分，則培訓和評分資料載入器是獨立的。 這允許您執行附加的預處理，如根據需要將培訓資料映射到評分資料。

## 管道檔案 {#pipeline-file}

的 `pipeline.py` 檔案包括用於培訓和評分的邏輯。

培訓的目的是使用培訓資料集中的特徵和標籤建立模型。 選擇培訓模型後，必須將x和y培訓資料集與模型匹配，函式將返回已培訓的模型。

>[!NOTE]
> 
>特徵是指機器學習模型用於預測標籤的輸入變數。

![定時列車](../images/jupyterlab/create-recipe/def_train.png)

的 `score()` 函式應包含計分算法並返回度量，以指示模型執行的成功程度。 的 `score()` 函式使用評分資料集標籤和訓練的模型來生成一組預測特徵。 然後將這些預測值與評分資料集中的實際特徵進行比較。 在此示例中， `score()` 函式使用訓練好的模型來使用評分資料集中的標籤來預測特徵。 返回所預測的特徵。

![def得分](../images/jupyterlab/create-recipe/def_score.png)

## 計算器檔案 {#evaluator-file}

的 `evaluator.py` 檔案包含邏輯，用於您如何評估已培訓的處方以及如何拆分培訓資料。

### 拆分資料集 {#split-the-dataset}

在訓練資料準備階段，需要將資料集進行拆分以用於訓練和測試。 此 `val` 資料在訓練後被隱式地用於評估模型。 此過程與計分分開。

此部分顯示 `split()` 函式，將資料載入到筆記本中，然後通過刪除資料集中不相關的列來清除資料。 從那裡，可以執行特徵工程，該過程是從資料中的現有原始特徵建立附加相關特徵。

![拆分函式](../images/jupyterlab/create-recipe/split.png)

### 評估已訓練的模型 {#evaluate-the-trained-model}

的 `evaluate()` 函式在模型訓練後執行，並返回度量以指示模型執行的成功程度。 的 `evaluate()` 函式使用測試資料集標籤和訓練好的模型來預測一組特徵。 然後將這些預測值與測試資料集中的實際特徵進行比較。 在本示例中，使用的度量 `precision`。 `recall`。 `f1`, `accuracy`。 請注意，函式返回 `metric` 包含評估度量陣列的對象。 這些度量用於評估經過訓練的模型的表現。

![評價](../images/jupyterlab/create-recipe/evaluate.png)

添加 `print(metric)` 允許您查看度量結果。

![度量結果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 資料保護程式檔案 {#data-saver-file}

的 `datasaver.py` 檔案包含 `save()` 函式，用於在測試評分時保存預測。 的 `save()` 函式獲取您的預測和使用 [!DNL Experience Platform Catalog] API，將資料寫入 `scoringResultsDataSetId` 您 `scoring.conf` 的子菜單。 你可以

![資料保護](../images/jupyterlab/create-recipe/data_saver.png)

## 培訓和評分 {#training-and-scoring}

完成對筆記本的更改並想要培訓配方後，您可以選擇條頂部的關聯按鈕，以在單元格中建立培訓運行。 選擇按鈕後，培訓指令碼中的命令和輸出日誌將顯示在筆記本(位於 `evaluator.py` )。 Conda首先安裝所有依賴項，然後開始培訓。

請注意，在運行計分之前，必須至少運行一次培訓。 選擇 **[!UICONTROL 運行計分]** 按鈕將在訓練期間生成的訓練模型上得分。 記分指令碼顯示在 `datasaver.py`。

為了調試目的，如果要查看隱藏輸出，請添加 `debug` 到輸出單元格的末尾，然後重新運行。

![訓練和評分](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 建立處方 {#create-recipe}

編輯完處方並滿足培訓/評分輸出後，您可以通過選擇 **[!UICONTROL 建立處方]** 右上角。

![](../images/jupyterlab/create-recipe/create-recipe.png)

選擇後 **[!UICONTROL 建立處方]**，系統將提示您輸入處方名稱。 此名稱表示建立於 [!DNL Platform]。

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

一旦選擇 **[!UICONTROL 確定]**，處方建立流程將開始。 這可能需要一些時間，並會顯示一個進度條來代替建立處方按鈕。 完成後，您可以選擇 **[!UICONTROL 查看配方]** 按鈕 **[!UICONTROL 食譜]** 頁籤 **[!UICONTROL ML模型]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 不刪除任何檔案單元格
> - 不編輯 `%%writefile` 檔案單元格頂部的行
> - 不要同時在不同筆記本中建立菜譜


## 後續步驟 {#next-steps}

完成本教程後，您將學習如何在 [!UICONTROL 處方生成器] 筆記本。 您還學習了如何將筆記本練習為菜譜工作流。

繼續學習如何在 [!DNL Data Science Workspace]，請訪問 [!DNL Data Science Workspace] 配方和模型下拉清單。