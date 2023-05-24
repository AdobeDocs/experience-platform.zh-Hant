---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 即時機器學習節點參考
description: 節點是圖形形成的基本單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，例如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 即時機器學習節點引用(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未提供給所有用戶。 此功能在Alpha中，仍在測試中。 此文檔可能會更改。

節點是圖形形成的基本單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，例如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。

下面的指南概述了支援的Real-time Machine Learning節點庫。

## 發現要在ML管道中使用的節點

將以下代碼複製到 [!DNL Python] 「筆記本」(Notebook)以查看所有可用節點。

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**示例響應**

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

標準節點建立在開放源資料科學庫的基礎上，如Pactis和ScikitLearn。

### 模型上載

ModelUpload節點是一個內部Adobe節點，它採用model_path並將模型從本地模型路徑上載到Real-time Machine Learning Blob儲存區。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### Onnxode

ONNXode是一個內部Adobe節點，它使用模型ID來拉取預訓練的ONNX模型，並使用它對傳入資料進行評分。

>[!TIP]
>
>按希望將資料發送到ONNX模型以計分的相同順序指定列。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊貓 {#pandas}

下面的Pactis節點允許您導入 `pd.DataFrame` 方法或任何一般的熊貓頂級功能。 要瞭解更多關於熊貓方法的資訊，請訪問 [熊貓方法文檔](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)。 有關頂級功能的詳細資訊，請訪問 [Panots API一般功能參考指南](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)。

下面的節點使用 `"import": "map"` 將方法名稱作為字串導入參數，然後將參數作為映射函式輸入。 下面的示例使用 `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`。 在映射到位後，您可以選擇 `inplace` 如 `True` 或 `False`。 設定 `inplace` 如 `True` 或 `False` 基於是否要應用轉換。 預設情況下 `"inplace": False` 建立新列。 對提供新列名的支援設定為在後續版本中添加。 最後一行 `cols` 可以是單列名或列清單。 指定要應用轉換的列。 在此示例中 `device` 。

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

### Scikit學習

ScikitLearn節點允許您導入任何ScikitLearn ML模型或縮放器。 有關示例中使用的任何值的詳細資訊，請使用下表：

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
| 特徵 | 將特徵輸入到模型（字串清單）。 <br> 例如： `browser`。 `device`。 `login_page`。 `product_page`。 `search_page` |
| label | 目標列名（字串）。 |
| 模式 | 火車/test（字串）。 |
| 模型路徑 | 以onnx格式本地保存模型的路徑。 |
| params.model | 模型的絕對導入路徑（字串），例如： `sklearn.linear_model.LogisticRegression`。 |
| params.model_params | 模型超參數，請參閱 [sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) 的子菜單。 |
| node_instance.process(data_message_from_previous_node) | 方法 `process()` 從上一個節點獲取DataMsg並應用轉換。 這取決於當前使用的節點。 |

### Split

使用以下節點通過傳遞將資料幀拆分為列和test `train_size` 或 `test_size`。 這將返回具有多索引的資料幀。 您可以使用以下示例訪問培訓和test資料幀， `msg5.data.xs("train")`。

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 後續步驟

下一步是建立用於對即時機器學習模型打分的節點。 有關詳細資訊，請訪問 [即時機器學習筆記本使用手冊](./rtml-authoring-notebook.md)。
