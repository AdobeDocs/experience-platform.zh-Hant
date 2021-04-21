---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace；熱門主題；建立配方
solution: Experience Platform
title: 使用Jupyter Notebooks建立配方
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將涵蓋兩個主要部分。 首先，您將使用JupyterLab Notebook中的範本建立機器學習模型。 接下來，您將在JupyterLab中練習筆記本至配方工作流程，以便在Data Science Workspace中建立配方。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用Jupyter Notebooks建立配方

本教學課程將涵蓋兩個主要部分。 首先，您將使用[!DNL JupyterLab Notebook]中的範本建立機器學習模型。 接下來，您將在[!DNL JupyterLab]內練習將筆記本應用於配方工作流，以在[!DNL Data Science Workspace]內建立配方。

## 引入的概念：

- **配方：** 配方是模型規格的Adobe術語，是代表特定機器學習、AI演算法或整合演算法、處理邏輯和設定的頂層容器，用來建立並執行已訓練的模型，進而協助解決特定的商業問題。
- **模型：** 模型是機器學習方式的例項，使用歷史資料和組態進行訓練，以解決商業使用案例。
- **訓練：** 訓練是學習模式和從標籤資料獲得見解的過程。
- **計分：** 計分是使用訓練好的模型從資料產生見解的程式。

## 開始使用[!DNL JupyterLab]筆記本環境

您可在[!DNL Data Science Workspace]中從頭建立配方。 若要開始，請導覽至[Adobe Experience Platform](https://platform.adobe.com)，然後按一下左側的&#x200B;**[!UICONTROL Notebooks]**&#x200B;標籤。 從[!DNL JupyterLab Launcher]中選擇「方式產生器」範本，以建立新筆記型電腦。

[!UICONTROL Recipe Builder]筆記型電腦允許您在筆記本內運行培訓和計分。 這可讓您在訓練和計分資料上執行實驗之間，靈活地變更其`train()`和`score()`方法。 一旦您對培訓和計分的輸出感到滿意，您就可以使用筆記型電腦建立用於[!DNL Data Science Workspace]的配方，以便將配方功能內建在Recipe Builder筆記型電腦上。

>[!NOTE]
>
>Recipe Builder筆記型電腦支援使用所有檔案格式，但目前「建立方式」功能僅支援[!DNL Python]。

![](../images/jupyterlab/create-recipe/recipe_builder.png)

當您從啟動器按一下Recipe Builder筆記型電腦時，就會在標籤中開啟筆記型電腦。 筆記本中使用的模板是Python Retail Sales Forecasting Recipe，該方式也可在[此公共儲存庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)中找到

您會注意到，在工具列中有三個額外的動作，即- **[!UICONTROL Train]**、**[!UICONTROL Score]**&#x200B;和&#x200B;**[!UICONTROL Create Recipe]**。 這些表徵圖僅出現在[!UICONTROL Recipe Builder]筆記本中。 在筆記型電腦中建立配方後，有關這些動作的詳細資訊，請參閱訓練與計分區段](#training-and-scoring)。[

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 編輯配方檔案

若要編輯配方檔案，請導覽至Jupyter中與檔案路徑對應的儲存格。 例如，如果要對`evaluator.py`進行更改，請查找`%%writefile demo-recipe/evaluator.py`。

開始對儲存格進行必要的變更，完成後，只要執行儲存格即可。 `%%writefile filename.py`命令會將單元格的內容寫入`filename.py`。 您必須手動為每個具有更改的檔案運行單元格。

>[!NOTE]
>
>如果適用，您應手動執行儲存格。

## 開始使用Recipe Builder筆記型電腦

現在，您已瞭解[!DNL JupyterLab]筆記型電腦環境的基本功能，可以開始查看構成機器學習模型配方的檔案。 我們將討論的檔案如下所示：

- [需求檔案](#requirements-file)
- [配置檔案](#configuration-files)
- [訓練資料載入器](#training-data-loader)
- [計分資料載入器](#scoring-data-loader)
- [管線檔案](#pipeline-file)
- [求值器檔案](#evaluator-file)
- [資料保護程式檔案](#data-saver-file)

### 需求檔案{#requirements-file}

需求檔案可用來宣告您想要在配方中使用的其他程式庫。 如果存在相依性，可以指定版本號。 若要尋找其他程式庫，請造訪[anaconda.org](https://anaconda.org)。 要瞭解如何格式化要求檔案，請訪問[Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually)。 已使用的主要程式庫清單包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您新增的程式庫或特定版本可能與上述程式庫不相容。 此外，如果您選擇手動建立環境檔案，則不允許覆蓋`name`欄位。

### 配置檔案{#configuration-files}

配置檔案`training.conf`和`scoring.conf`用於指定要用於培訓和計分以及添加超參數的資料集。 培訓和計分有不同的配置。

使用者在執行訓練和計分之前，必須填入下列變數：
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

要查找資料集和方案ID，請轉到左側導航欄（資料夾表徵圖下）筆記本內的資料頁籤![資料頁籤](../images/jupyterlab/create-recipe/dataset-tab.png)。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

在&#x200B;**[Schema](https://platform.adobe.com/schema)**&#x200B;和&#x200B;**[Datasets](https://platform.adobe.com/dataset/overview)**&#x200B;標籤下的[Adobe Experience Platform](https://platform.adobe.com/)上可以找到相同的資訊。

預設情況下，在訪問資料時會為您設定以下配置參數：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 訓練資料載入器{#training-data-loader}

訓練資料載入器的目的，是執行個體化用於建立機器學習模型的資料。 通常，培訓資料載入器將完成兩項工作：
- 從[!DNL Platform]載入資料
- 資料準備與功能工程

以下兩節將重新載入資料和資料準備。

### 正在載入資料{#loading-data}

此步驟使用[pactices資料框](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)。 可使用[!DNL Platform] SDK(`platform_sdk`)從[!DNL Adobe Experience Platform]的檔案載入資料，或使用`read_csv()`或`read_json()`函式從外部來源載入資料。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部來源](#external-sources)

>[!NOTE]
>
>在Recipe Builder筆記型電腦中，資料會透過`platform_sdk`資料載入器載入。

### [!DNL Platform] SDK {#platform-sdk}

有關使用`platform_sdk`資料載入器的深入教學課程，請造訪[平台SDK指南](../authoring/platform-sdk.md)。 本教學課程提供有關建立驗證、基本資料讀取和基本資料寫入的資訊。

### 外部源{#external-sources}

本節將說明如何將JSON或CSV檔案匯入至Apcotes物件。 熊貓圖書館的官方檔案可在這裡找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是匯入CSV檔案的範例。 `data`引數是CSV檔案的路徑。 此變數是從[上一節](#configuration-files)的`configProperties`匯入。

```PYTHON
df = pd.read_csv(data)
```

您也可以從JSON檔案匯入。 `data`引數是CSV檔案的路徑。 此變數是從[上一節](#configuration-files)的`configProperties`匯入。

```PYTHON
df = pd.read_json(data)
```

現在，您的資料位於資料幀對象中，可以在[下一節](#data-preparation-and-feature-engineering)中分析和處理。

### 從平台SDK

您可以使用平台SDK載入資料。 您可加入下列行，將程式庫匯入頁面頂端：

`from platform_sdk.dataset_reader import DatasetReader`

然後，我們使用`load()`方法從`trainingDataSetId`擷取訓練資料集，如我們的設定(`recipe.conf`)檔案中所設定。

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    
    dataset_reader = DatasetReader(client_context, config_properties['trainingDataSetId'])
    
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

>[!NOTE]
>
>如[配置檔案部分](#configuration-files)中所述，當您使用`client_context`從Experience Platform訪問資料時，將為您設定以下配置參數：
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


既然您擁有了資料，您就可以從資料準備和功能工程開始。

### 資料準備與功能工程{#data-preparation-and-feature-engineering}

載入資料後，會準備資料，然後分割至`train`和`val`資料集。 范常式式碼如下：

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
- 添加`week`和`year`列
- 將`storeType`轉換為指示符變數
- 將`isHoliday`轉換為數值變數
- 偏移`weeklySales`以獲得將來和過去的銷售值
- 按日期將資料拆分為`train`和`val`資料集

首先，建立`week`和`year`列，並將原始`date`列轉換為[!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)。 周值和年值從日期時間對象中提取。

接著，將`storeType`轉換為代表三種不同商店類型的三欄（`A`、`B`和`C`）。 每個值都包含一個布爾值，其狀態`storeType`為true。 將刪除`storeType`列。

同樣地，`weeklySales`將`isHoliday`布林值變更為數值表示法，一或零。

此資料會在`train`和`val`資料集之間分割。

`load()`函式應以`train`和`val`資料集作為輸出。

### 計分資料載入器{#scoring-data-loader}

載入計分資料的程式與`split()`函式中載入訓練資料的程式類似。 我們使用Data Access SDK從`recipe.conf`檔案中的`scoringDataSetId`載入資料。

```PYTHON
def load(config_properties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    client_context = get_client_context(config_properties)

    dataset_reader = DatasetReader(client_context, config_properties['scoringDataSetId'])
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

在載入資料後，完成資料準備和特徵工程。

```PYTHON
    #########################################
    # Data Preparation/Feature Engineering
    #########################################
    if '_id' in dataframe.columns:
        #Rename columns to strip tenantId
        dataframe = dataframe.rename(columns = lambda x : str(x)[str(x).find('.')+1:])
        #Drop id, eventType and timestamp
        dataframe.drop(['_id', 'eventType', 'timestamp'], axis=1, inplace=True)

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

    print("Scoring Data Load Finish")

    return dataframe
```

由於我們模型的目的是預測未來每週銷售量，因此您需要建立評分資料集來評估模型預測的成效。

此Recipe Builder筆記型電腦可將我們每週7天的銷售額提前抵銷。 請注意，每週有45個商店的測量值，因此您可以將45個資料集的`weeklySales`值向前移入名為`weeklySalesAhead`的新欄。

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

同樣地，您也可以通過向後移45來建立`weeklySalesLag`列。 使用此功能，您也可以計算每週銷售額的差值，並將它們儲存在`weeklySalesDiff`欄中。

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

由於您正在向前偏移`weeklySales`資料點45個資料集，並向後偏移45個資料集以建立新列，因此前45個和後45個資料點將具有NaN值。 您可以使用`df.dropna()`函式從我們的資料集中移除這些點，此函式會移除所有具有NaN值的列。

```PYTHON
df.dropna(0, inplace=True)
```

計分資料載入器中的`load()`函式應以計分資料集作為輸出。

### 管線檔案{#pipeline-file}

`pipeline.py`檔案包含訓練和計分的邏輯。

### 培訓 {#training}

訓練的目的是使用訓練資料集中的功能和標籤來建立模型。

>[!NOTE]
> 
>功能是指機器學習模型用來預測標籤的輸入變數。

`train()`函式應包含訓練模型並傳回訓練模型。 有關不同型號的一些示例，請參見[scikit-learn使用手冊文檔](https://scikit-learn.org/stable/user_guide.html)。

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

請注意，根據您的應用程式，您的`GradientBoostingRegressor()`函式中會有引數。 `xTrainingDataset` 應包含您用於訓練的功能，但應 `yTrainingDataset` 包含您的標籤。

### 計分{#scoring}

`score()`函式應包含計分演算法並傳回測量，以指出模型執行的成功程度。 `score()`函式使用計分資料集標籤和訓練的模型來產生一組預測特徵。 然後，將這些預測值與計分資料集中的實際特徵進行比較。 在此範例中，`score()`函式使用訓練好的模型，使用計分資料集的標籤來預測功能。 會傳回預計的功能。

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

### 求值器檔案{#evaluator-file}

`evaluator.py`檔案包含您如何評估訓練方式以及如何分割訓練資料的邏輯。 在零售銷售範例中，將包含載入和準備培訓資料的邏輯。 我們將詳細介紹以下兩節。

### 分割資料集{#split-the-dataset}

訓練的資料準備階段需要分割資料集以用於訓練和測試。 此`val`資料將隱式用於模型訓練後評估。 此程式與計分不同。

本節將顯示`split()`函式，該函式將首先將資料載入到筆記本中，然後通過刪除資料集中不相關的列來清除資料。 在此之後，您將能夠執行功能工程，即從資料中現有的原始功能建立其他相關功能的程式。 此程式的範例如下，以及說明。

`split()`函式如下所示。 參數中提供的資料幀將被拆分為要返回的`train`和`val`變數。

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 評估已培訓的型號{#evaluate-the-trained-model}

`evaluate()`函式在模型訓練後執行，並會傳回量度，指出模型執行的成功程度。 `evaluate()`函式使用測試資料集標籤和「訓練的」模型來預測一組功能。 然後，將這些預測值與測試資料集中的實際特徵進行比較。 常見的計分演算法包括：
- [平均絕對百分比誤差(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [平均絕對誤差(MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [均方根誤差](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


零售銷售範例中的`evaluate()`函式如下所示：

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

請注意，函式會傳回包含評估度量陣列的`metric`物件。 這些量度將用來評估受訓練模型的效能。

### 資料保護程式檔案{#data-saver-file}

`datasaver.py`檔案包含`save()`函式，可在測試計分時儲存您的預測。 `save()`函式將採用您的預測，並使用[!DNL Experience Platform Catalog] API，將資料寫入您在`scoring.conf`檔案中指定的`scoringResultsDataSetId`。

此處顯示零售銷售範例配方中使用的範例。 請注意，使用`DataSetWriter`庫將資料寫入平台：

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

## 訓練與計分{#training-and-scoring}

當您變更筆記型電腦並想要訓練配方時，可以按一下列上方的相關按鈕，在儲存格中建立訓練執行。 按一下該按鈕後，培訓指令碼的命令和輸出日誌將顯示在筆記本中（位於`evaluator.py`單元格下）。 Conda首先安裝所有相依項，然後開始培訓。

請注意，您必須至少執行一次培訓，才能執行計分。 按一下&#x200B;**[!UICONTROL Run Scoring]**&#x200B;按鈕將對培訓期間生成的已培訓模型進行分數。 計分指令碼將顯示在`datasaver.py`下。

為進行除錯，如果您想查看隱藏的輸出，請將`debug`新增至輸出儲存格的結尾，然後重新執行。

## 建立方式{#create-recipe}

編輯完配方並滿意培訓／計分輸出後，可以通過按右上角導航中的&#x200B;**[!UICONTROL Create Recipe]**&#x200B;從筆記本建立配方。

![](../images/jupyterlab/create-recipe/create-recipe.png)

按下按鈕後，系統會提示您輸入配方名稱。 此名稱代表在[!DNL Platform]上建立的實際方式。

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

按&#x200B;**[!UICONTROL Ok]**&#x200B;後，您就可以瀏覽至[Adobe Experience Platform](https://platform.adobe.com/)上的新配方。 您可以按一下&#x200B;**[!UICONTROL View Recipes]**&#x200B;按鈕，將您帶至&#x200B;**[!UICONTROL ML Models]**&#x200B;下方的&#x200B;**[!UICONTROL Recipes]**&#x200B;標籤

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

一旦程式完成，配方將如下所示：

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - 不要刪除任何檔案單元格
> - 不要編輯檔案單元格頂部的`%%writefile`行
> - 不要同時在不同的筆記本中建立配方


## 下一步 {#next-steps}

完成本教學課程後，您就學會如何在Recipe Builder筆記型電腦中建立機器學習模型。 您還學習了如何在筆記本中練習如何將筆記型電腦與配方工作流程結合，以便在[!DNL Data Science Workspace]中建立配方。

若要繼續學習如何使用[!DNL Data Science Workspace]內的資源，請造訪[!DNL Data Science Workspace]配方和模型下拉式清單。

## 其他資源 {#additional-resources}

以下影片旨在協助您瞭解建立和部署模型。

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)
