---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics;create recipe
solution: Experience Platform
title: 使用Jupyter筆記型電腦建立配方
topic: Tutorial
description: 本教學課程將涵蓋兩個主要部分。 首先，您將使用JupyterLab Notebook中的範本建立機器學習模型。 接下來，您將在JupyterLab中練習筆記本至配方工作流程，以便在Data Science Workspace中建立配方。
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '2336'
ht-degree: 0%

---


# 使用Jupyter筆記型電腦建立配方

本教學課程將涵蓋兩個主要部分。 首先，您將使用中的範本建立機器學習模型 [!DNL JupyterLab Notebook]。 接下來，您將練習將筆記本移至內部的配方工作流 [!DNL JupyterLab] 程，以在內部建立配方 [!DNL Data Science Workspace]。

## 引入的概念：

- **方式：** 配方是Adobe的模型規格術語，是代表特定機器學習、AI演算法或整合演算法、處理邏輯和設定的頂層容器，用來建立並執行已訓練的模型，進而協助解決特定的商業問題。
- **型號：** 模型是機器學習方式的實例，使用歷史資料和配置進行訓練，以針對業務使用案例進行解決。
- **培訓：** 培訓是學習模式和從標籤資料獲得見解的過程。
- **計分：** 計分是使用訓練好的模型，從資料產生見解的程式。

## 開始使用筆記 [!DNL JupyterLab] 本環境

從頭開始建立配方可在內部完成 [!DNL Data Science Workspace]。 若要開始，請導覽至 [Adobe Experience Platform](https://platform.adobe.com) ，然後按一下左側 **[!UICONTROL 的「筆記型電腦]** 」標籤。 從中選擇「方式產生器」範本，以建立新的筆記本 [!DNL JupyterLab Launcher]。

Recipe Builder  筆記型電腦可讓您在筆記型電腦中執行訓練和計分。 這可讓您在針對訓練和計分資料執行 `train()` 實驗 `score()` 時，靈活地變更其和方法。 一旦您對訓練和計分的輸出感到滿意，就可以建立配方，以便使用筆記型電腦， [!DNL Data Science Workspace] 將配方功能內建在Recipe Builder筆記型電腦上。

>[!NOTE]
>
>Recipe Builder筆記型電腦支援使用所有檔案格式，但目前「建立方式」功能僅支援 [!DNL Python]。

![](../images/jupyterlab/create-recipe/recipe-builder.png)

當您從啟動器按一下Recipe Builder筆記型電腦時，筆記型電腦就會在標籤中開啟。 筆記本中使用的模板是Python Retail Sales Forecasting Recipe，也可以在此公共儲存庫 [中找到](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

您會注意到，在工具列中有三個額外的動作，即 **[!UICONTROL 訓練]**、 **[!UICONTROL 分數]****[!UICONTROL 和建立方式]**。 這些圖示只會出現在 [!UICONTROL Recipe Builder筆記本中] 。 在筆記型電腦中建立配方後，有關這 [些動作的詳細資訊，請參閱訓練與計分區](#training-and-scoring) 。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 編輯配方檔案

若要編輯配方檔案，請導覽至Jupyter中與檔案路徑對應的儲存格。 例如，如果您想要變更，請 `evaluator.py`尋找 `%%writefile demo-recipe/evaluator.py`。

開始對儲存格進行必要的變更，完成後，只要執行儲存格即可。 命 `%%writefile filename.py` 令將單元格的內容寫入 `filename.py`。 您必須手動為每個具有更改的檔案運行單元格。

>[!NOTE]
>
>如果適用，您應手動執行儲存格。

## 開始使用Recipe Builder筆記型電腦

現在您已瞭解筆記型電腦環境的基 [!DNL JupyterLab] 本功能，可以開始檢視構成機器學習模型配方的檔案。 我們將討論的檔案如下所示：

- [需求檔案](#requirements-file)
- [配置檔案](#configuration-files)
- [訓練資料載入器](#training-data-loader)
- [計分資料載入器](#scoring-data-loader)
- [管線檔案](#pipeline-file)
- [求值器檔案](#evaluator-file)
- [資料保護程式檔案](#data-saver-file)

### 需求檔案 {#requirements-file}

需求檔案可用來宣告您想要在配方中使用的其他程式庫。 如果存在相依性，可以指定版本號。 若要尋找其他資料庫，請造訪https://anaconda.org。 已使用的主要程式庫清單包括：

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您新增的程式庫或特定版本可能與上述程式庫不相容。

### 配置檔案 {#configuration-files}

配置檔案和 `training.conf` 用 `scoring.conf`於指定要用於培訓和計分以及添加超參數的資料集。 培訓和計分有不同的配置。

使用者在執行訓練和計分之前，必須填入下列變數：
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

若要尋找資料集和結構ID，請前往左側導覽列（資料夾圖示下）筆記型電腦中的資料標籤。

![](../images/jupyterlab/create-recipe/datasets.png)

在 [Adobe Experience Platform的「架構」和「資料集](https://platform.adobe.com/) 」標籤下 **[，可找到相](https://platform.adobe.com/schema)** 同的資訊 **[](https://platform.adobe.com/dataset/overview)** 。

預設情況下，在訪問資料時會為您設定以下配置參數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 訓練資料載入器 {#training-data-loader}

訓練資料載入器的目的，是執行個體化用於建立機器學習模型的資料。 通常，培訓資料載入器將完成兩項工作：
- 從 [!DNL Platform]
- 資料準備與功能工程

以下兩節將重新載入資料和資料準備。

### 載入資料 {#loading-data}

這個步驟使用 [熊貓資料框](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)。 您可使用SDK( [!DNL Adobe Experience Platform] )從檔案載入資料，或使用熊貓或功能從外部來源 [!DNL Platform] 載入`platform_sdk``read_csv()``read_json()` 資料。

- [[!DNL平台SDK]](#platform-sdk)
- [外部來源](#external-sources)

>[!NOTE]
>
>在Recipe Builder筆記型電腦中，資料會透過資料載入器 `platform_sdk` 載入。

### [!DNL Platform] SDK {#platform-sdk}

如需有關使用資料載入器的深入教 `platform_sdk` 學課程，請造訪 [Platform SDK指南](../authoring/platform-sdk.md)。 本教學課程提供有關建立驗證、基本資料讀取和基本資料寫入的資訊。

### 外部來源 {#external-sources}

本節將說明如何將JSON或CSV檔案匯入至Apcotes物件。 熊貓圖書館的官方檔案可在這裡找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 引 `data` 數是CSV檔案的路徑。 此變數是從上一節 `configProperties` 中匯 [入的](#configuration-files)。

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案匯入。 引 `data` 數是CSV檔案的路徑。 此變數是從上一節 `configProperties` 中匯 [入的](#configuration-files)。

```PYTHON
df = pd.read_json(data)
```

現在，您的資料已位於dataframe物件中，可在下一節中加以分 [析和處理](#data-preparation-and-feature-engineering)。

### 從資料存取SDK（已過時）

>[!CAUTION]
>
> `data_access_sdk_python` 不再建議使用，請參閱「將 [資料存取程式碼轉換為平台SDK](../authoring/platform-sdk.md) 」，以取得有關使用資料載入器 `platform_sdk` 的指南。

使用者可使用資料存取SDK載入資料。 您可加入下列行，將程式庫匯入頁面頂端：

`from data_access_sdk_python.reader import DataSetReader`

然後，利用 `load()` 該方法從配置()檔案中 `trainingDataSetId` 的集合中獲取訓練資料`recipe.conf`集。

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>如「配置文 [件」部分中所述](#configuration-files)，在從中訪問資料時為您設定以下配置參數 [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


既然您擁有了資料，您就可以從資料準備和功能工程開始。

### 資料準備與功能工程 {#data-preparation-and-feature-engineering}

資料載入後，資料會進行準備，然後分割至資料 `train` 集 `val` 和。 范常式式碼如下：

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

在此範例中，對原始資料集有5項動作：
- 新增 `week` 和欄 `year`
- 轉換 `storeType` 為指示符變數
- 轉換 `isHoliday` 為數值變數
- 抵銷 `weeklySales` 以獲得未來和過去的銷售價值
- 依日期分割資料至 `train` 和資 `val` 料

首先， `week` 建立 `year` 列和列，並將原始列 `date` 轉換為日期時 [!DNL Python] 間 [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)。 周值和年值從日期時間對象中提取。

接著， `storeType` 會轉換為代表三種不同商店類型(`A`、 `B`和 `C`)的三欄。 每個值都包含一個布爾值，以狀態 `storeType` 為true。 該 `storeType` 列將被刪除。

同樣地， `weeklySales` 將布爾值 `isHoliday` 更改為數字表示，一或零。

此資料會在資料集和資 `train` 料集 `val` 之間分割。

函 `load()` 數應以和資料集 `train` 為 `val` 輸出。

### 計分資料載入器 {#scoring-data-loader}

載入計分資料的程式類似於在函式中載入訓練資 `split()` 料。 我們使用Data Access SDK來載入檔案中 `scoringDataSetId` 的資料 `recipe.conf` 。

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

在載入資料後，完成資料準備和特徵工程。

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

由於我們模型的目的是預測未來每週銷售量，因此您需要建立評分資料集來評估模型預測的成效。

此Recipe Builder筆記型電腦可將我們每週7天的銷售額提前抵銷。 請注意，每週有45個商店的測量值，因此您可以將 `weeklySales` 45個資料集的值向前移入新的欄位，稱為 `weeklySalesAhead`。

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

同樣地，您也可以將45位移 `weeklySalesLag` 回建立欄。 使用此功能，您也可以計算每週銷售額的差值，並將它們儲存在欄中 `weeklySalesDiff`。

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

由於您要向前偏移45 `weeklySales` 個資料集，並向後偏移45個資料集以建立新欄，因此前45個和後45個資料點將有NaN值。 您可以使用函式從資料集中移除這些點， `df.dropna()` 此函式可移除所有具有NaN值的列。

```PYTHON
df.dropna(0, inplace=True)
```

計分 `load()` 資料載入器中的函式應以計分資料集作為輸出。

### 管線檔案 {#pipeline-file}

該檔 `pipeline.py` 案包含訓練和計分的邏輯。

### 培訓 {#training}

訓練的目的是使用訓練資料集中的功能和標籤來建立模型。

>[!NOTE]
> 
>_功能_ ，是指機器學習模型用來預測標籤的輸入變 _數_。

功能 `train()` 應包括訓練模型和返回訓練模型。 scikit-learn使用指南文檔中提供 [了一些不同型號的示例](https://scikit-learn.org/stable/user_guide.html)。

在選擇您的訓練模型後，您會將x和y訓練資料集符合模型，而函式會傳回已訓練的模型。 顯示此情況的範例如下：

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

請注意，視您的應用程式而定，函式中會有引數 `GradientBoostingRegressor()` 。 `xTrainingDataset` 應包含您用於訓練的功能，但應 `yTrainingDataset` 包含您的標籤。

### 計分 {#scoring}

函 `score()` 數應包含計分演算法並傳回測量，以指出模型執行的成效。 該函 `score()` 數使用計分資料集標籤和訓練的模型來生成一組預測特徵。 然後，將這些預測值與計分資料集中的實際特徵進行比較。 在此範例中，函 `score()` 數使用訓練好的模型，使用計分資料集的標籤來預測特徵。 會傳回預計的功能。

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### 求值器檔案 {#evaluator-file}

檔 `evaluator.py` 案包含您如何評估訓練方式以及如何分割訓練資料的邏輯。 在零售銷售範例中，將包含載入和準備培訓資料的邏輯。 我們將詳細介紹以下兩節。

### 分割資料集 {#split-the-dataset}

訓練的資料準備階段需要分割資料集以用於訓練和測試。 這 `val` 些資料在訓練後會隱含使用來評估模型。 此程式與計分不同。

本節將顯示首 `split()` 先將資料載入到筆記本中，然後通過刪除資料集中不相關的列來清除資料的函式。 在此之後，您將能夠執行功能工程，即從資料中現有的原始功能建立其他相關功能的程式。 此程式的範例如下，以及說明。

函式 `split()` 如下所示。 參數中提供的資料幀將被拆分為要 `train` 返回 `val` 的和變數。

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 評估訓練好的模型 {#evaluate-the-trained-model}

函式 `evaluate()` 是在模型訓練後執行，並會傳回量度，以指出模型執行的成效。 此函 `evaluate()` 數使用測試資料集標籤和訓練模型來預測一組特徵。 然後，將這些預測值與測試資料集中的實際特徵進行比較。 常見的計分演算法包括：
- [平均絕對百分比誤差(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [平均絕對誤差(MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [均方根誤差](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


零售 `evaluate()` 銷售範例中的函式如下所示：

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

請注意，函式會傳回包 `metric` 含評估度量陣列的物件。 這些量度將用來評估受訓練模型的效能。

### 資料保護程式檔案 {#data-saver-file}

檔案 `datasaver.py` 包含在測試計 `save()` 分時儲存預測的函式。 函 `save()` 數會擷取您的預測，並使用 [!DNL Experience Platform Catalog] API，將資料寫入您 `scoringResultsDataSetId` 在檔案中指定的 `scoring.conf` 位置。

此處顯示零售銷售範例配方中使用的範例。 請注意，使用程 `DataSetWriter` 式庫將資料寫入平台：

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## 訓練與計分 {#training-and-scoring}

當您變更筆記型電腦並想要訓練配方時，可以按一下列上方的相關按鈕，在儲存格中建立訓練執行。 按一下該按鈕後，培訓指令碼中的命令和輸出日誌將顯示在筆記本中(單元格 `evaluator.py` 下)。 Conda首先安裝所有相依項，然後開始培訓。

請注意，您必須至少執行一次培訓，才能執行計分。 按一下「執 **[!UICONTROL 行計分]** 」按鈕，將對培訓期間產生的已訓練模型評分。 計分指令碼將出現在下方 `datasaver.py`。

為了進行除錯，如果您想查看隱藏的輸出，請將 `debug` 其新增至輸出儲存格的結尾，然後重新執行。

## 建立方式 {#create-recipe}

編輯完配方並滿意培訓／計分輸出後，您可以按右上方導覽中的「建立配方 **** 」，從筆記本建立配方。

![](../images/jupyterlab/create-recipe/create-recipe.png)

按下按鈕後，系統會提示您輸入配方名稱。 此名稱代表在上建立的實際方式 [!DNL Platform]。

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

按「確 **[!UICONTROL 定]** 」後，您就可以導覽至 [Adobe Experience Platform上的新配方](https://platform.adobe.com/)。 您可以按一下「檢 **[!UICONTROL 視配方]** 」按鈕，將您帶至「ML模型」下的「配方 **[!UICONTROL 」標籤]****[!UICONTROL 。]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

一旦程式完成，配方將如下所示：

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - 不要刪除任何檔案單元格
> - 不要編輯 `%%writefile` 檔案儲存格頂端的行
> - 不要同時在不同的筆記本中建立配方


## 下一步 {#next-steps}

完成本教學課程後，您就學會如何在Recipe Builder筆記型電腦中建立機器學習模型。 您還學習了如何在筆記型電腦中練習如何將筆記型電腦與配方工作流程結合，以便在其中建立配方 [!DNL Data Science Workspace]。

若要繼續學習如何使用資源，請造 [!DNL Data Science Workspace]訪配方和模 [!DNL Data Science Workspace] 型下拉式清單。

## 其他資源 {#additional-resources}

以下影片旨在協助您瞭解建立和部署模型。

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


