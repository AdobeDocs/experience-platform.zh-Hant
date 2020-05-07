---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: 為即時機器學習模型評分
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 為即時機器學習模型評分

>[!IMPORTANT]
>目前尚未針對所有使用者提供即時機器學習。 此功能是alpha版，仍在測試中。 本檔案可能會有所變更。

本教學課程將說明如何使用即時機器學習節點來預先處理傳入的資料，並根據您的ONNX模型對其評分。

>[!IMPORTANT]
> - 節點中使用的函式無法序列化。 例如，在熊貓節點中使用的λ函式。
> - 手動部署邊緣後，會有60秒的睡眠。 這可以傳輸至EdgeUtils的score_edge方法。


>[!NOTE]
>為了為用於即時機器學習的模型評分，您必須完成上一堂有關培訓即時機器學 [習模型的教學課程](./training-ml-model.md)

## 建立新筆記本

在Adobe Experience Platform UI中，從Data Science中選 **[!UICONTROL 擇]***Notebooks*。 接著，選 **[!UICONTROL 擇JupyterLab]** ，並為環境載入留出一些時間。

![open JupyterLab](../images/rtml/open-jupyterlab.png)

首先，從JupyterLab啟動 **器中選擇空白的Python 3筆記本** 。

![空白python](../images/rtml/python-blank.png)

## 匯入和發現節點

首先，導入模型的所有必需包。 請確定您計畫用於節點編寫的任何軟體包都已導入。

>[!NOTE]
>您的匯入清單可能會因您建立的模型而異。

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

要查看可用節點清單，請複製並貼上以下示例到筆記本中。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

收到的響應是節點清單。

![注釋清單](../images/rtml/node-list.png)

## 節點製作邊緣計分功能

接下來，您需要定義並製作邊緣計分的節點。 將范 `model_id` 例中的範本ID取代為您在上一個教學課程中完成訓練時所 [收到的模型ID](./training-ml-model.md)。 本例使用Apcots節點導入pd.DataDrame方法或通用的Appotics頂層函式。 映射函式被導入並用於建立兩個節點。 有關可用節點以及如何使用這些節點的詳細資訊，請訪問節 [點參考指南](./node-reference.md)。

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## 建置圖形DSL

在您建立節點後，下一步是將節點連結在一起，以建立圖形。

首先，列出屬於圖形的所有節點。

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

接著，將節點與邊連接。 每個元組都是邊連接。

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

連接節點後，請建立圖形。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## 發佈至邊緣

現在您已建立圖形，可將圖形部署至邊緣。

>[!IMPORTANT]
>不要經常發佈至邊緣，這可能會使邊緣節點過載。 不建議多次發佈相同模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Edge用戶端

發佈至邊緣後，計分由用戶端的POST要求完成。 通常，這可以從需要ML分數的用戶端應用程式完成。 您也可以從郵遞員處完成。 在此，EdgeUtils可用來示範程式。

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

計分完成後，會傳回邊緣URL、裝載和來自邊緣的計分輸出。

![計分完成](../images/rtml/scoring-complete.png)

## 從邊緣刪除已部署的應用程式（可選）

>!![CAUTION]
此儲存格用於刪除已部署的邊緣應用程式。 請勿使用下列儲存格，除非您需要刪除已部署的邊緣應用程式。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 後續步驟

遵循上述教學課程，您已成功測分並部署即時機器學習模型。 如果您想要進一步瞭解可用於製作模型的節點，請造訪節 [點參考指南](./node-reference.md)。



