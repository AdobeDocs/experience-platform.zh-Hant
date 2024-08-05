---
keywords: Experience Platform；開發人員指南；資料科學Workspace；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 即時機器學習節點參考
description: 節點是形成圖形的基本單位。 每個節點會執行特定工作，而且它們可以使用連結連結連結在一起，以形成代表ML管道的圖形。 節點所執行的作業代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 9030a5482d4ea2b54426680cef92b89e68ef5b33
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 即時機器學習節點參考(Alpha)

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 本檔案可能會有所變更。

節點是形成圖形的基本單位。 每個節點會執行特定工作，而且它們可以使用連結連結連結在一起，以形成代表ML管道的圖形。 節點所執行的作業代表對輸入資料的操作，例如資料或結構描述的轉換，或機器學習推斷。 節點會將轉換或推斷的值輸出到下一個節點。

下列指南概述即時機器學習支援的節點程式庫。

## 探索節點以用於ML管道

將下列程式碼複製到[!DNL Python]筆記本以檢視所有可供使用的節點。

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**範例回應**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## 標準節點

標準節點是以Pandas和ScikitLearn等開放原始碼資料科學資料庫為基礎。

### ModelUpload

ModelUpload節點是內部Adobe節點，會接受model_path並將模型從本機模型路徑上傳到Real-time Machine Learning Blob存放區。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode是內部Adobe節點，會擷取模型ID以提取預先訓練的ONNX模型，並使用其對傳入資料進行評分。

>[!TIP]
>
>以您希望資料傳送至ONNX模型評分的相同順序指定欄。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊貓 {#pandas}

下列「熊貓」節點可讓您匯入任何`pd.DataFrame`方法或任何一般熊貓最上層函式。 若要深入瞭解Pandas方法，請瀏覽[Pandas方法檔案](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)。 如需最上層函式的詳細資訊，請造訪[Pandas API參考指南，瞭解一般函式](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)。

下列節點使用`"import": "map"`將方法名稱匯入為引數中的字串，接著將引數輸入為對應函式。 以下範例使用`{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`來執行此操作。 完成地圖設定後，您就可以選擇將`inplace`設為`True`或`False`。 根據您是否要套用轉換，將`inplace`設為`True`或`False`。 根據預設，`"inplace": False`會建立新資料行。 提供新欄名稱的支援已設定為在後續版本中新增。 最後一行`cols`可以是單一資料行名稱或資料行清單。 指定要套用轉換的欄。 在此範例中，指定了`device`。

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

ScikitLearn節點可讓您匯入任何ScikitLearn ML模型或縮放器。 使用下表取得有關範例中使用之任何值的詳細資訊：

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 值 | 說明 |
| --- | --- |
| 功能 | 輸入特徵到模型（字串清單）。 <br>例如： `browser`、`device`、`login_page`、`product_page`、`search_page` |
| 標籤 | 目標欄名稱（字串）。 |
| 模式 | 訓練/測試（字串）。 |
| 模型路徑 | 以文字格式在本機儲存模型的路徑。 |
| params.model | 模型（字串）的絕對匯入路徑，例如： `sklearn.linear_model.LogisticRegression`。 |
| params.model_params | 模型超引數，如需詳細資訊，請參閱[sklearn API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)檔案。 |
| node_instance.process(data_message_from_previous_node) | 方法`process()`從上一個節點取得DataMsg並套用轉換。 這取決於目前使用的節點。 |

### 分割

使用以下節點，透過傳遞`train_size`或`test_size`將您的資料流分割成訓練及測試。 這會傳回具有多索引的資料流。 您可以使用下列範例`msg5.data.xs("train")`存取訓練與測試資料流。

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 後續步驟

下一步是建立節點，以用於對Real-time Machine Learning模型進行評分。 如需詳細資訊，請瀏覽[即時機器學習筆記本使用手冊](./rtml-authoring-notebook.md)。
