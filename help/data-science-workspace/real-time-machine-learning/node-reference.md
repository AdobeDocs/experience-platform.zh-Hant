---
keywords: Experience Platform；開發人員指南；資料科學工作區；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 即時機器學習節點參考
topic-legacy: Nodes reference
description: 節點是圖形形成的基礎單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 即時機器學習節點參考(Alpha)

>[!IMPORTANT]
>
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

節點是圖形形成的基礎單元。 每個節點都執行特定任務，並且可以使用連結將它們連結在一起，以形成表示ML管線的圖形。 由節點執行的任務表示對輸入資料的操作，如資料或模式的轉換或機器學習推理。 節點將變換或推斷的值輸出到下一個節點。

以下指南概述即時機器學習支援的節點程式庫。

## 發現要在ML管線中使用的節點

將以下代碼複製到[!DNL Python]筆記本中，以查看所有可用節點。

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

標準節點建立在開放源碼資料科學庫之上，如Pactices和ScikitLearn。

### ModelUpload

ModelUpload節點是內部Adobe節點，它採用model_path，並將模型從本地模型路徑上載到Real-time Machine Learning Blob儲存。

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNode

ONNXode是內部Adobe節點，它使用模型ID提取預先訓練的ONNX模型，並使用它對傳入資料進行分數。

>[!TIP]
>
>以您希望將資料傳送至ONNX模型以分數的相同順序指定欄。

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### 熊貓{#pandas}

下面的熊貓節點，可以匯入任何`pd.DataFrame`方法或任何普通熊貓的頂層功能。 要進一步瞭解熊貓方法，請訪問[熊貓方法文檔](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)。 有關頂級函式的更多資訊，請訪問[Apcots API參考指南，以瞭解一般函式](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html)。

以下節點使用`"import": "map"`將方法名稱作為字串導入參數中，然後將參數作為映射函式輸入。 以下範例使用`{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`執行此動作。 在對應到位後，您可以選擇將`inplace`設為`True`或`False`。 根據是否要就地應用轉換，將`inplace`設定為`True`或`False`。 預設情況下，`"inplace": False`會建立新列。 對提供新欄名稱的支援已設定為在後續版本中新增。 最後一行`cols`可以是單列名稱或列清單。 指定要應用轉換的列。 在此示例中指定`device`。

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

ScikitLearn節點可讓您匯入任何ScikitLearn ML模型或縮放器。 請使用下表，以取得範例中任何值的詳細資訊：

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| 值 | 說明 |
| --- | --- |
| 功能 | 輸入模型特徵（字串清單）。 <br> 例如： `browser`,  `device`,  `login_page`,  `product_page`,  `search_page` |
| 標籤 | 目標欄名稱（字串）。 |
| 模式 | 訓練／測試（字串）。 |
| model_path | 以onnx格式本機儲存模型的路徑。 |
| params.model | 模型的絕對匯入路徑（字串），例如：`sklearn.linear_model.LogisticRegression`。 |
| params.model_params | 模型超參數，請參閱[sklearn API(map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)檔案以取得詳細資訊。 |
| node_instance.process(data_message_from_previous_node) | 方法`process()`從上一個節點獲取DataMsg並應用轉換。 這取決於當前使用的節點。 |

### Split

使用以下節點將資料幀拆分為列並通過傳遞`train_size`或`test_size`進行測試。 這會傳回具有多索引的資料幀。 您可以使用以下示例`msg5.data.xs(“train”)`訪問訓練和測試資料幀。

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## 後續步驟

下一步是建立節點，以用於即時機器學習模型的計分。 如需詳細資訊，請造訪[即時機器學習筆記型電腦使用指南](./rtml-authoring-notebook.md)。
