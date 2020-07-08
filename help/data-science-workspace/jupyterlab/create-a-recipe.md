---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: 使用Jupyter筆記型電腦建立配方
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 0%

---


# 使用Jupyter筆記型電腦建立配方

本教學課程將涵蓋兩個主要部分。 首先，您將使用中的範本建立機器學習模型 [!DNL JupyterLab Notebook]。 接下來，您將練習將筆記本移至內部的配方工作流 [!DNL JupyterLab] 程，以在內部建立配方 [!DNL Data Science Workspace]。

## 引入的概念：

- **方式：** 配方是Adobe的模型規格術語，是代表特定機器學習、AI演算法或整合演算法、處理邏輯和設定的頂層容器，用來建立並執行已訓練的模型，進而協助解決特定的商業問題。
- **Model:** A model is an instance of a machine learning recipe that is trained using historical data and configurations to solve for a business use case.
- **培訓：** 培訓是學習模式和從標籤資料獲得見解的過程。
- **計分：** 計分是使用訓練好的模型，從資料產生見解的程式。

## 開始使用筆記 [!DNL JupyterLab] 本環境

從頭開始建立配方可在內部完成 [!DNL Data Science Workspace]。 若要開始，請導覽至 [Adobe Experience Platform](https://platform.adobe.com) ，然後按一下左側 **[!UICONTROL 的「筆記型電腦]** 」標籤。 從中選擇「方式產生器」範本，以建立新的筆記本 [!DNL JupyterLab Launcher]。

Recipe Builder  筆記型電腦可讓您在筆記型電腦中執行訓練和計分。 This gives you the flexibility to make changes to their `train()` and `score()` methods in between running experiments on the training and scoring data. 一旦您對訓練和計分的輸出感到滿意，就可以建立配方，以便使用筆記型電腦， [!DNL Data Science Workspace] 將配方功能內建在Recipe Builder筆記型電腦上。

>[!NOTE]
>
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

需求檔案可用來宣告您想要在配方中使用的其他程式庫。 如果存在相依性，可以指定版本號。 若要尋找其他資料庫，請造訪https://anaconda.org。 已在使用的主要程式庫清單包括：

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
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

The same information can be found on [Adobe Experience Platform](https://platform.adobe.com/) under the **[Schema](https://platform.adobe.com/schema)**and**[Datasets](https://platform.adobe.com/dataset/overview)** tabs.

By default, the following configuration parameters are set for you when you access data:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 訓練資料載入器 {#training-data-loader}

訓練資料載入器的目的，是執行個體化用於建立機器學習模型的資料。 Typically, there are two tasks that the training data loader will accomplish:
- Load data from [!DNL Platform]
- 資料準備與功能工程

The following two sections will go over loading data and data preparation.

### Loading data {#loading-data}

This step uses the [pandas dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 您可使用SDK( [!DNL Adobe Experience Platform] )從檔案載入資料，或使用熊貓或功能從外部來源 [!DNL Platform] 載入`platform_sdk``read_csv()``read_json()` 資料。

- [!DNL Platform SDK](#platform-sdk)
- [External sources](#external-sources)

>[!NOTE]
>
>
>In the Recipe Builder notebook, data is loaded via the `platform_sdk` data loader.

### [!DNL Platform] SDK {#platform-sdk}

For an in-depth tutorial on using the `platform_sdk` data loader, please visit the [Platform SDK guide](../authoring/platform-sdk.md). This tutorial provides information on build authentication, basic reading of data, and basic writing of data.

### External sources {#external-sources}

This section shows you how to import a JSON or CSV file to a pandas object. Official documentation from the pandas library can be found here:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 引 `data` 數是CSV檔案的路徑。 This variable was imported from the `configProperties` in the [previous section](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

You can also import from a JSON file. The `data` argument is the path to the CSV file. This variable was imported from the `configProperties` in the [previous section](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Now your data is in the dataframe object and can be analyzed and manipulated in the [next section](#data-preparation-and-feature-engineering).

### From Data Access SDK (Deprecated)

>[!CAUTION]
>
>
> `data_access_sdk_python` 不再建議使用，請參閱「將 [資料存取程式碼轉換為平台SDK](../authoring/platform-sdk.md) 」，以取得有關使用資料載入器 `platform_sdk` 的指南。

Users can load data using the Data Access SDK. The library can be imported at the top of the page by including the line:

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
>
>As mentioned in the [Configuration File section](#configuration-files), the following configuration parameters are set for you when you access data from [!DNL Experience Platform]:
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
- add `week` and `year` columns
- 轉換 `storeType` 為指示符變數
- 轉換 `isHoliday` 為數值變數
- offset `weeklySales` to get future and past sales value
- split data, by date, to `train` and `val` dataset

First, `week` and `year` columns are created and the original `date` column converted to [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). 周值和年值從日期時間對象中提取。

接著， `storeType` 會轉換為代表三種不同商店類型(`A`、 `B`和 `C`)的三欄。 每個值都包含一個布爾值，以狀態 `storeType` 為true。 該 `storeType` 列將被刪除。

Similarly, `weeklySales` changes the `isHoliday` boolean to a numerical representation, one or zero.

This data is split between `train` and `val` dataset.

The `load()` function should complete with the `train` and `val` dataset as the output.

### 計分資料載入器 {#scoring-data-loader}

The procedure to load data for scoring is similar to the loading training data in the `split()` function. We use the Data Access SDK to load data from the `scoringDataSetId` found in our `recipe.conf` file.

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

After loading the data, data preparation and feature engineering is done.

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

Since the purpose of our model is to predict future weekly sales, you will need to create a scoring dataset used to evaluate how well the model&#39;s prediction performs.

This Recipe Builder notebook does this by offsetting our weeklySales 7 days forwards. Notice that there are measurements for 45 stores every week so you can shift the `weeklySales` values 45 datasets forwards into a new column called `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Similarly, you can create a column `weeklySalesLag` by shifted 45 back. Using this you can also calculate the difference in weekly sales and store them in column `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Since you are offsetting the `weeklySales` datapoints 45 datasets forwards and 45 datasets backwards to create new columns, the first and last 45 data points will have NaN values. 您可以使用函式從資料集中移除這些點， `df.dropna()` 此函式可移除所有具有NaN值的列。

```PYTHON
df.dropna(0, inplace=True)
```

計分 `load()` 資料載入器中的函式應以計分資料集作為輸出。

### 管線檔案 {#pipeline-file}

The `pipeline.py` file includes logic for training and scoring.

### 培訓 {#training}

The purpose of training is to create a model using features and labels in your training dataset.

>[!NOTE]
>
> 
>_Features_ refer to the input variable used by the machine learning model to predict the _labels_.

The `train()` function should include the training model and return the trained model. Some examples of different models can be found in the [scikit-learn user guide documentation](https://scikit-learn.org/stable/user_guide.html).

After choosing your training model, you will fit your x and y training dataset to the model and the function will return the trained model. 顯示此情況的範例如下：

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

函 `score()` 數應包含計分演算法並傳回測量，以指出模型執行的成效。 該函 `score()` 數使用計分資料集標籤和訓練的模型來生成一組預測特徵。 These predicted values are then compared with the actual features in the scoring dataset. 在此範例中，函 `score()` 數使用訓練好的模型，使用計分資料集的標籤來預測特徵。 The predicted features are returned.

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

The `evaluator.py` file contains logic for how you wish to evaluate your trained recipe as well as how your training data should be split. In the retail sales example, the logic for loading and preparing the training data will be included. We will go over the two sections below.

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

The example used in the retail sales sample recipe is seen here. Note the use of `DataSetWriter` library to write data to Platform:

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

當您變更筆記型電腦並想要訓練配方時，可以按一下列上方的相關按鈕，在儲存格中建立訓練執行。 Upon clicking the button, a log of commands and outputs from the training script will appear in the notebook (under the `evaluator.py` cell). Conda first installs all the dependencies, then the training is initiated.

請注意，您必須至少執行一次培訓，才能執行計分。 按一下「執 **[!UICONTROL 行計分]** 」按鈕，將對培訓期間產生的已訓練模型評分。 計分指令碼將出現在下方 `datasaver.py`。

為了進行除錯，如果您想查看隱藏的輸出，請將 `debug` 其新增至輸出儲存格的結尾，然後重新執行。

## 建立方式 {#create-recipe}

編輯完配方並滿意培訓／計分輸出後，您可以按右上方導覽中的「建立配方 **** 」，從筆記本建立配方。

![](../images/jupyterlab/create-recipe/create-recipe.png)

After pressing the button, you are prompted to enter a recipe name. This name represents the actual recipe created on [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Once you press **[!UICONTROL Ok]** you will be able to navigate to the new recipe on [Adobe Experience Platform](https://platform.adobe.com/). You can click on the **[!UICONTROL View Recipes]** button to take you to the **[!UICONTROL Recipes]** tab under **[!UICONTROL ML Models]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

一旦程式完成，配方將如下所示：

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - 不要刪除任何檔案單元格
> - 不要編輯 `%%writefile` 檔案儲存格頂端的行
> - Do not create recipes in different notebooks at the same time


## 下一步 {#next-steps}

By completing this tutorial, you have learned how to create a machine learning model in the Recipe Builder notebook. You have also learned how to exercise the notebook to recipe workflow within the notebook to create a recipe within [!DNL Data Science Workspace].

To continue learning how to work with resources within [!DNL Data Science Workspace], please visit the [!DNL Data Science Workspace] recipes and models dropdown.

## 其他資源 {#additional-resources}

The following video is designed to support your understanding of building and deploying models.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


