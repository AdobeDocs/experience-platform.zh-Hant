---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: 即時機器學習的模型訓練
topic: Training a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---


# 即時機器學習的模型訓練

>[!IMPORTANT]
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

本檔案提供將ONNX模型上傳至Real-time Machine Learning模型商店的教學課程。

使用下列選項之一，您將編寫python代碼以讀取、預處理和分析資料。 接下來，您需要訓練自己的ML模型，將其序列化為ONNX格式，最後將它上傳至Real-time Machine Learning模型商店。 此外，在教學課程結束時，您會獲得一個模型ID，可識別已訓練的模型，以便用於計 [分教學課程](./scoring-ml-model.md)。

* [使用Python筆記本來訓練模型](#training-model-python-notebook)
* [使用您自己的ONNX模型來培訓模型](#train-using-own-onnx-model)
* [使用方式產生器範本來訓練模型](#train-using-recipe-builder)
* [使用Data Science Workplace方式工作流程來訓練模型](#recipe-workflow-train-model)


## 使用Python筆記型電腦訓練模型 {#training-model-python-notebook}

在Adobe Experience Platform UI中，從Data Science中選 **[!UICONTROL 擇]***Notebooks*。 接著，選 **[!UICONTROL 擇JupyterLab]** ，並為環境載入留出一些時間。

![open JupyterLab](../images/rtml/open-jupyterlab.png)

首先，從JupyterLab啟動 **器中選擇空白的Python 3筆記本** 。

![空白python](../images/rtml/python-blank.png)

### 存取資料 {#access-data}

接著，選取您要使用的資料集。 要訪問JupyterLab筆記本中的資料集，請在JupyterLab的左側導航中選 **擇** 「資料」頁籤。 此時將 *顯示Dataset* 和 *Schemas目錄* 。 選擇 **[!UICONTROL 資料集]** ，然後按一下滑鼠右鍵，然後從您要使用的資料集上的下拉式選單中選取「在筆記型電腦中 **[!UICONTROL 探索資料]** 」選項。 可執行的代碼條目出現在您的筆記本中。

![資料集存取](../images/rtml/access-dataset.png)

### 準備您的模型

使用下列範本來分析、預處理、訓練和評估您的ML模型。 如需完整範例，請使用此範本下方提供的螢幕擷取：

```python
from sklearn import svm, metrics
from sklearn.model_selection import train_test_split


data = df[input_columns]
target = df[target_column]
# Create a classifier: a support vector classifier
classifier = svm.SVC(gamma=0.001)

# Split data into train and test subsets
X_train, X_test, y_train, y_test = train_test_split(
    data, target, test_size=0.5, shuffle=False)

# We train the classifier
classifier.fit(X_train, y_train)

# Now do predictions
predicted = classifier.predict(X_test)


print("Classification report for classifier %s:\n%s\n"
      % (classifier, metrics.classification_report(y_test, predicted)))
disp = metrics.plot_confusion_matrix(classifier, X_test, y_test)
disp.figure_.suptitle("Confusion Matrix")
print("Confusion matrix:\n%s" % disp.confusion_matrix)
```

>[!NOTE]
>下列範例使用scikit-learn程式庫，而非從收錄的Adobe Experience Platform資料集載入資料。

![安裝scikit](../images/rtml/install-scikit.png)![訓練範例](../images/rtml/train-example.png)

**輸出**

![scikit的輸出](../images/rtml/train-example-response.png)

### 上傳您的模型

完成上一步驟後，您需要將模型序列化為ONNX格式，並上傳到即時機器學習商店。 這會傳回下 `model_id` 一個教學課程中 [所使用的](#next-steps)。

使用下列範本轉換為ONNX並上傳資料集：

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils
import ModelUpload
from rtml_nodelibs.core.nodefactory
import NodeFactory as nf
from skl2onnx.common.data_types
import FloatTensorType
from skl2onnx
import convert_sklearn

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(classifier, 'ScikitLearnModel', inputs)

model_path = "model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

  ########## Upload the model from model_path to RTML model store ##########
  model = ModelUpload(params = {
    'model_path': model_path
  })

msg_model = model.process(None, 1)

model_id = msg_model.model['model_id']

print("Model ID : ", model_id)
```

**回應**

![模型id](../images/rtml/model-id.png)

收到您的檔案後 `model_id`，請加以複製並繼續下 [一步](#next-steps)。


## 使用您自己的ONNX模型來培訓模型 {#train-using-own-onnx-model}

在Adobe Experience Platform UI中，從Data Science中選 **[!UICONTROL 擇]***Notebooks*。 接著，選 **[!UICONTROL 擇JupyterLab]** ，並為環境載入留出一些時間。

![open JupyterLab](../images/rtml/open-jupyterlab.png)

使用JupyterLab筆記型電腦中的上傳按鈕，將您的ONNX型號上傳到Data Science Workspace筆記型電腦環境。

![上傳圖示](../images/rtml/upload.png)

接著，在JupyterLab啟動程式中，選取Python 3下的空白筆記型電腦圖示，以建立新的空白筆記型電腦。

![空白python](../images/rtml/python-blank.png)

在空白筆記本中，複製並貼上以下內容：

>[!NOTE]
> 請務必提供您上 `model_path` 傳的ONNX模型。

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
 
model_path = <path/to/onnx_model>
########## Upload the model from model_path to RTML model store ##########
model = ModelUpload(params={'model_path': model_path})
 
msg_model = model.process(None, 1)
 
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

執行上述儲存格後，會傳 `model_id` 回儲存格。 複製要在下一個教學課程中使用的 [模型ID](#next-steps)。

## 使用預先建立的方式範本來訓練模型 {#train-using-recipe-builder}

在Adobe Experience Platform UI中，從Data Science中選 **[!UICONTROL 擇]***Notebooks*。 接著，選 **[!UICONTROL 擇JupyterLab]** ，並為環境載入留出一些時間。

![open JupyterLab](../images/rtml/open-jupyterlab.png)

接下來，請依照使用 [Jupyter筆記型電腦教學課程建立配方](../jupyterlab/create-a-recipe.md) 。 完成後，您需要修改pipeline.py檔案以便即時顯示。

>[!NOTE]
>資料科學工作區提供的範本必須修改，以符合您的資料集。

請確定您將模型保存為ONNX格式，並將環境變數設定為 `ONNX_MODEL_PATH`。 以下範例說明如何使用方式產生器範本修改管線檔案。

```python
def train(configProperties, data):

  print("Train Start")

########## Extract fields from configProperties ##########
learning_rate = float(configProperties['learning_rate'])
n_estimators = int(configProperties['n_estimators'])
max_depth = int(configProperties['max_depth'])

########## Fit model ##########
X_train = data.drop('weeklySalesAhead', axis = 1).values
y_train = data['weeklySalesAhead'].values

seed = 1234
model = GradientBoostingRegressor(learning_rate = learning_rate,
  n_estimators = n_estimators,
  max_depth = max_depth,
  random_state = seed)

model.fit(X_train, y_train)

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)

model_path = "retail_sales_model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

print("Train Complete")

return model
```

修改pipeline.py檔案後，執行 **[!UICONTROL Training]** and **[!UICONTROL Scoring]**。 完成後，請選取「建 **[!UICONTROL 立方式]** 」按鈕。

![訓練和計分按鈕](../images/rtml/train-score.png)

此時會出現命名對話框。 輸入處方名稱，然後選擇「確 **[!UICONTROL 定」]**。 出現新對話方塊，提醒您方式建立已開始。 讓您有時間建立配方。

![配方對話框](../images/rtml/recipe-dialog.png)

![配方對話框](../images/rtml/recipe-dialog-confrim.png)

在建立配方後，您可在提供的對話方塊中選取「檢視配方」 **[!UICONTROL ，或導覽至「模型」，然後在左上角的導覽中選取「配方]********** 」，來檢視配方。 此時會顯示依建立日期排序的方式清單。 確認您的新配方在頂端。

![您的食譜](../images/rtml/view-recipe.png)

選取您的方式。 此時將顯示配方概述頁面。 在右上方導覽中，選取「建 **[!UICONTROL 立模型」]**。

![方式概觀](../images/rtml/create-model.png)

接著，選取適當的資料集。 然後按 **[!UICONTROL 一下右上]** 方導覽中的「下一步」。

![選擇資料集](../images/rtml/select-dataset.png)

此時將開啟配置頁。 提供模型名稱並查看預設模型配置。 在建立處方時會應用預設配置。 按兩下設定值，以檢視並修改設定值。 若要提供新的組態，請按一下「上 **[!UICONTROL 傳新設定」]** ，並將包含模型組態的JSON檔案拖曳至瀏覽器視窗。 選擇「 **[!UICONTROL 完成]** 」(Finish)以建立模型。

![配置模型](../images/rtml/configure-model.png)

建立模型後，您必須等待訓練執行完成。 成功的培訓執行完成後，您可以選取培訓執行來檢視其詳細資訊。

選取訓練執行。 選取後，屬性對話方塊會出現在右側。 在此對話框中，選擇「查 **[!UICONTROL 看活動日誌」]**。

![檢視培訓課程](../images/rtml/view-training.png)

此時將 *顯示「查看活動日誌* 」對話框。 選取記錄檔 *的URL* ，以下載記錄檔，並檢視執行的詳細資訊。

![查看日誌](../images/rtml/view-logs.png)

對於失敗的執行，記錄檔特別有用，以檢視出錯之處。 但是，在本例中，您正在查找與 `model-id` 您建立的ONNX模型對應的。 複製模型ID。

>[!NOTE]
>你不用去做計分工作。 下一步將涵蓋即時機器學習邊緣 [計分](#next-steps)。

![尋找模型ID](../images/rtml/find-model-id-logs.png)

## 使用Data Science Workplace方式工作流程來訓練模型 {#recipe-workflow-train-model}

如果您熟悉Docker、git和封裝Python程式碼，這是最佳的使用方法。 使用「資料科學工作區」工作流程，讓您在建立食譜時擁有最大的彈性和自由。 您可以提取基本Docker映像並構建自己的Docker環境、更輕鬆地對配方進行調試、克隆預構建配方以便與任何Data Science Workspace服務一起運行、計畫配方運行等。

### 建立架構

第一步需要您的資料集有資料結構。 您可以透過Adobe Experience Platform UI或Platform API來建立結構。

>[!NOTE]
>如果您已有想要用在Adobe Experience Platform中的資料，請跳過以建 [立Python方式](#create-a-python-recipe)。

* [使用架構編輯器UI教程建立架構](../../xdm/tutorials/create-schema-ui.md)
* [使用架構編輯器API教程建立架構](../../xdm/tutorials/create-schema-api.md)

### 收錄您的資料

接下來，您需要使用您剛建立的架構來內嵌資料。 這可透過使用API或平台UI來完成。

>[!NOTE]
>如果您已有想要用在Adobe Experience Platform中的資料，請跳過以建 [立Python方式](#create-a-python-recipe)。

* [將資料內嵌至Adobe Experience Platform UI教學課程](../../ingestion/tutorials/ingest-batch-data.md)
* [將資料內嵌至Adobe Experience Platform API教學課程](../../ingestion/batch-ingestion/api-overview.md)

### 建立Python配方 {#create-a-python-recipe}

方式建立從封裝來源檔案開始，以建立封存檔案。 來源檔案定義機器學習邏輯和演算法，用以解決手邊的特定問題。 使用以下教程來構建Python Docker映像。

* [將來源檔案封裝至配方](../models-recipes/package-source-files-recipe.md)

要完成下一步，您需要在Azure容器註冊表中擁有Docker影像以及對應的影像URL。 選擇下面的教程連結之一以完成建立Python配方：

* [在UI中匯入封裝的方式](../models-recipes/import-packaged-recipe-ui.md)
* [使用API匯入封裝的方式](../models-recipes/import-packaged-recipe-api.md)

### 建立訓練執行

在Adobe Experience Platform Data Science Workspace中，機器學習模型是透過整合符合模型意圖的現有配方來建立的。 然後，對模型進行訓練和評估，通過微調其相關的超參數來優化其操作效率和效能。

* [在UI中訓練和評估模型](../models-recipes/train-evaluate-model-ui.md)
* [在API中訓練和評估模型](../models-recipes/train-evaluate-model-api.md)

>[!IMPORTANT]
>在配方的pipeline.py檔案中，將模型以ONNX格式保存在中， `model_path` 並將環境變數設定為 `ONNX_MODEL_PATH`。 執行時期會尋找此特定的環境變數。

```python
def train(configProperties, data):
 
    print("Train Start")
 
    ########## Extract fields from configProperties ##########

    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])
 
 
    
    ########## Fit model ##########
    
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values
 
    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)
 
    model.fit(X_train, y_train)
     
    ########## Save sklearn model in ONNX format at model_path ##########
    inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
    model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)
 
    model_path = "retail_sales_model.onnx"
    os.environ["ONNX_MODEL_PATH"] = model_path
 
    with open(model_path, "wb") as f:
        f.write(model_onnx.SerializeToString())
 
    print("Train Complete")
 
    return model
```

建立模型後，您必須等待訓練執行完成。 成功的培訓執行完成後，您可以選取培訓執行以檢視其詳細資訊。 選取訓練執行。 選擇屬性對話框後，將顯示在右側，選擇「查看活 **[!UICONTROL 動日誌」]**。

![檢視培訓課程](../images/rtml/view-training.png)

此時將 *顯示「查看活動日誌* 」對話框。 選取記錄檔 *的URL* ，以下載記錄檔，並檢視執行的詳細資訊。

![查看日誌](../images/rtml/view-logs.png)

對於失敗的執行，記錄檔特別有用，以檢視出錯之處。 但是，在本例中，您正在查找與 `model-id` 您建立的ONNX模型對應的。 複製模型ID。

![尋找模型ID](../images/rtml/find-model-id-logs.png)

您不必在配方中執行計分工作。 下一個教學課程將涵蓋即時機器學習 [邊緣計分](#next-steps)。

## 下一步 {#next-steps}

遵循上述其中一個教學課程，您已成功訓練ONNX模型並將其上傳至Real-time Machine Learning模型商店，並擁有可識別您 `model_id` 模型的程式碼。 繼續下一個教學課程，瞭解如何 [對即時機器學習模型評分](./scoring-ml-model.md)。