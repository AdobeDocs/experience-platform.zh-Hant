---
keywords: Experience Platform；開發人員指南；Data Science Workspace；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 即時機器學習節點參考
description: 節點是圖形形成的基本單元。 每個節點執行特定任務，它們可以通過連結連結在一起，以形成表示ML管道的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將轉換或推斷的值輸出到下一個節點。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 即時機器學習節點參考(Alpha)

>[!IMPORTANT]
>
>尚未向所有用戶提供即時機器學習。 此功能為Alpha版，仍在測試中。 本檔案可能會有所變更。

節點是圖形形成的基本單元。 每個節點執行特定任務，它們可以通過連結連結在一起，以形成表示ML管道的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將轉換或推斷的值輸出到下一個節點。

以下指南概述即時機器學習支援的節點程式庫。

## 探索要在ML管道中使用的節點

將下列程式碼複製到 [!DNL Python] 筆記型電腦，查看所有可用的節點。

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

標準節點構建在開放原始碼資料科學庫（如Pancits和ScikitLearn）之上。

### ModelUpload

ModelUpload節點是內部Adobe節點，會取用model_path，並將模型從本地模型路徑上載到即時機器學習Blob儲存。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNode

ONNXode是內部Adobe節點，它使用模型ID提取預先訓練的ONNX模型，並使用它對傳入的資料進行分數。

>[!TIP]
>
>以要將資料發送到ONNX模型以計分的相同順序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊貓 {#pandas}

下面的Pancits節點可讓您導入任何 `pd.DataFrame` 方法或任何普通熊貓的頂層功能。 要了解更多有關Apnicts方法的資訊，請訪問 [熊貓方法檔案](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). 如需頂層功能的詳細資訊，請造訪 [Apactis API一般功能參考指南](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

以下節點使用 `"import": "map"` 在參數中以字串形式導入方法名稱，然後輸入參數作為映射函式。 以下範例是使用 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. 在對應就緒後，您可以選擇設定 `inplace` as `True` 或 `False`. 設定 `inplace` as `True` 或 `False` 根據是否要應用轉換。 依預設 `"inplace": False` 建立新列。 提供新欄名稱的支援已設定為在後續版本中新增。 最後一行 `cols` 可以是單一欄名稱或欄清單。 指定要套用轉換的欄。 在此範例中 `device` 已指定。

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

ScikitLearn節點可讓您匯入任何ScikitLearn ML模型或縮放器。 請使用下表，以取得範例中所使用任何值的詳細資訊：

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
| 功能 | 將特徵輸入到模型（字串清單）。 <br> 例如： `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Target欄名稱（字串）。 |
| 模式 | 訓練/測試（字串）。 |
| model_path | 以onnx格式在本地保存模型的路徑。 |
| params.model | 模型的絕對匯入路徑（字串），例如： `sklearn.linear_model.LogisticRegression`. |
| params.model_params | 模型超參數，請參閱 [sklearn API（地圖/字典）](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 檔案以取得詳細資訊。 |
| node_instance.process(data_message_from_previous_node) | 方法 `process()` 從前一個節點取用DataMsg並套用轉換。 這取決於目前使用的節點。 |

### Split

使用以下節點將資料幀拆分到訓練中，並通過傳遞進行測試 `train_size` 或 `test_size`. 這會傳回具有多索引的資料幀。 您可以使用以下示例訪問訓練和測試資料幀， `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 後續步驟

下一步是建立節點，以用於對即時機器學習模型進行計分。 如需詳細資訊，請造訪 [即時機器學習筆記型電腦使用手冊](./rtml-authoring-notebook.md).
