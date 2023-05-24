---
keywords: Experience Platform；開發者指南；資料科學工作區；熱門主題；即時機器學習；節點參考；
solution: Experience Platform
title: 管理即時機器學習筆記本
description: 以下指南概述了在Adobe Experience PlatformJupyterLab中構建即時機器學習應用程式所需的步驟。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# 管理即時機器學習筆記本(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未提供給所有用戶。 此功能在Alpha中，仍在測試中。 此文檔可能會更改。

以下指南概述了構建即時機器學習應用程式所需的步驟。 使用提供的Adobe **[!UICONTROL 即時ML]** 本指南介紹了Python筆記本模板，包括培訓模型、建立DSL、將DSL發佈到Edge，以及對請求進行評分。 在實施即時機器學習模型的過程中，希望您修改模板以滿足資料集的需要。

## 建立即時機器學習筆記本

在Adobe Experience PlatformUI中，選擇 **[!UICONTROL 筆記本]** 從 **資料科學**。 下一步，選擇 **[!UICONTROL 朱佩特拉布]** 並給環境載入一段時間。

![開啟JupyterLab](../images/rtml/open-jupyterlab.png)

的 [!DNL JupyterLab] 啟動程式。 向下滾動到 *即時機器學習* 的 **[!UICONTROL 即時ML]** 筆記本。 將開啟一個模板，其中包含帶有示例資料集的示例筆記本單元格。

![空白python](../images/rtml/authoring-notebook.png)

## 導入和發現節點

首先導入模型的所有必需包。 確保導入計畫用於節點創作的任何包。

>[!NOTE]
>
>您的導入清單可能會因您希望建立的模型而有所不同。 隨著新節點的添加，此清單將發生變化。 請參閱 [節點參考指南](./node-reference.md) 的子菜單。

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

以下代碼單元格打印可用節點的清單。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![注釋清單](../images/rtml/node-list.png)

## 即時機器學習模型的訓練

使用以下選項之一，您將編寫 [!DNL Python] 用於讀取、預處理和分析資料的代碼。 接下來，您需要訓練自己的ML模型，將其序列化為ONNX格式，然後將其上傳到Real-time Machine Learning模型儲存。

- [在JupyterLab筆記本中培訓您自己的型號](#training-your-own-model)
- [將您自己預先培訓的ONNX型號上傳到JupyterLab筆記本](#pre-trained-model-upload)

### 培訓您自己的模型 {#training-your-own-model}

首先載入培訓資料。

>[!NOTE]
>
>在 **即時ML** 模板 [車險CSV資料集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) 從 [!DNL Github]。

![載入培訓資料](../images/rtml/load_training.png)

如果希望使用Adobe Experience Platform內的資料集，請取消注釋下面的單元格。 接下來，您需要 `DATASET_ID` 值。

![rtml資料集](../images/rtml/rtml-dataset.png)

訪問資料集 [!DNL JupyterLab] 筆記本，選擇 **資料** 的子菜單。 [!DNL JupyterLab]。 的 **[!UICONTROL 資料集]** 和 **[!UICONTROL 架構]** 的下界。 選擇 **[!UICONTROL 資料集]** ，然後選擇 **[!UICONTROL 在筆記本中瀏覽資料]** 選項。 可執行代碼條目出現在筆記本底部。 這個手機 `dataset_id`。

![資料集訪問](../images/rtml/access-dataset.png)

完成後，按一下右鍵並刪除在筆記本底部生成的單元格。

### 培訓屬性

使用提供的模板，修改中的任何培訓屬性 `config_properties`。

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 準備模型

使用 **[!UICONTROL 即時ML]** 模板，您需要分析、預處理、訓練和評估您的ML模型。 這是通過應用資料轉換和構建培訓管道來完成的。

**資料轉換**

的 **[!UICONTROL 即時ML]** 模板 **資料轉換** 需要修改單元格以使用您自己的資料集。 這通常涉及更名列、資料匯總和資料準備/功能工程。

>[!NOTE]
>
>以下示例已使用 `[ ... ]`。 請查看並展開 *即時ML* 完整代碼單元格的模板資料轉換部分。

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

運行提供的單元格以查看示例結果。 從 `carinsurancedataset.csv` dataset返回您定義的修改。

![資料轉換示例](../images/rtml/table-return.png)

**培訓管道**

接下來，您需要建立培訓管道。 這看起來與任何其他培訓管道檔案類似，但您需要轉換並生成ONNX檔案除外。

使用上一個單元格中定義的資料轉換修改模板。 下面突出顯示的代碼用於在特徵管線中生成ONNX檔案。 請查看 *即時ML* 完整管道代碼單元格的模板。

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

完成培訓管道並通過資料轉換修改資料後，請使用以下單元格運行培訓。

```python
model = train(config_properties, df_final)
```

### 生成並上載ONNX模型

完成成功的培訓運行後，需要生成ONNX模型，並將培訓的模型上載到即時機器學習模型儲存。 運行以下單元格後，您的ONNX型號將與所有其他筆記本一起顯示在左側導軌中。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>更改 `model_path` 字串值`model.onnx`)以更改模型的名稱。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>以下單元格不可編輯或刪除，並且是Real-time Machine Learning應用程式工作所必需的。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX型號](../images/rtml/onnx-model-rail.png)

### 上傳您自己預先培訓的ONNX型號 {#pre-trained-model-upload}

使用位於 [!DNL JupyterLab] 筆記本，將預先培訓的ONNX型號上傳到 [!DNL Data Science Workspace] 筆記本環境。

![上載表徵圖](../images/rtml/upload.png)

接下來，更改 `model_path` 字串值 *即時ML* 筆記本，以匹配ONNX型號名稱。 完成後，運行 *設定模型路徑* 然後運行 *將模型上載到RTML模型儲存* 的子菜單。 成功時，在響應中將返回模型位置和模型ID。

![上傳自己的模型](../images/rtml/upload-own-model.png)

## 域特定語言(DSL)建立

本節概述建立DSL。 您將編寫包含任何資料預處理的節點以及ONNX節點。 然後，使用節點和邊建立DSL圖。 邊使用基於元組的格式(node_1、node_2)連接節點。 圖形不應具有循環。

>[!IMPORTANT]
>
>必須使用ONNX節點。 沒有ONNX節點，應用程式將不成功。

### 節點創作

>[!NOTE]
>
> 您可能會根據所使用的資料類型具有多個節點。 以下示例僅概括了中的單個節點 *即時ML* 的下界。 請查看 *即時ML* 模板 *節點創作* 的子菜單。

下面的熊貓節點使用 `"import": "map"` 將方法名稱作為字串導入參數，然後將參數作為映射函式輸入。 下面的示例使用 `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`。 在映射到位後，您可以選擇 `inplace` 如 `True` 或 `False`。 設定 `inplace` 如 `True` 或 `False` 基於是否要應用轉換。 預設情況下 `"inplace": False` 建立新列。 對提供新列名的支援設定為在後續版本中添加。 最後一行 `cols` 可以是單列名或列清單。 指定要應用轉換的列。 在此示例中 `leasing` 。 有關可用節點以及如何使用它們的詳細資訊，請訪問 [節點參考指南](./node-reference.md)。

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### 構建DSL圖形

建立節點後，下一步是將節點鏈在一起以建立圖。

首先通過構建陣列列出屬於圖形一部分的所有節點。

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

接下來，用邊連接節點。 每個元組是 [!DNL Edge] 連接。

>[!TIP]
>
> 由於節點彼此線性依賴（每個節點都取決於前一個節點的輸出），因此您可以使用簡單的Python清單理解建立連結。 如果節點依賴於多個輸入，請添加您自己的連接。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

連接節點後，生成圖。 下面的單元格是必需的，無法編輯或刪除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成後， `edge` 返回對象，其中包含每個節點以及映射到這些節點的參數。

![邊返回](../images/rtml/edge-return.png)

## 發佈到邊緣（集線器）

>[!NOTE]
>
>即時機器學習暫時部署到Adobe Experience Platform中心並由其管理。 有關其他詳細資訊，請訪問概述部分， [即時機器學習體系結構](./home.md#architecture)。

現在您已建立了DSL圖表，可以將圖表部署到 [!DNL Edge]。

>[!IMPORTANT]
>
>不發佈到 [!DNL Edge] 通常，這會使負載過大 [!DNL Edge] 節點。 建議不要多次發佈同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新DSL並將重新發佈到邊緣（可選）

如果您不需要更新DSL，可跳至 [評分](#scoring)。

>[!NOTE]
>
>僅當您希望更新已發佈到Edge的現有DSL時，才需要以下單元格。

你的模型可能會繼續發展。 與其建立新服務，不如使用新模型更新現有服務。 您可以定義要更新的節點，為其分配新ID，然後將新DSL重新上載到 [!DNL Edge]。

在下例中，節點0將用新ID更新。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![已更新節點](../images/rtml/updated-node.png)

更新節點ID後，可以將更新的DSL重新發佈到邊緣。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

您將返回更新的DSL。

![更新的DSL](../images/rtml/updated-dsl.png)

## 評分 {#scoring}

發佈到 [!DNL Edge]，評分由客戶端的POST請求完成。 通常，這可以從需要ML分數的客戶端應用程式中完成。 你也可以從Postman做。 的 **[!UICONTROL 即時ML]** 模板使用EdgeUtils演示此過程。

>[!NOTE]
>
>在開始計分之前，需要一小段處理時間。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用與訓練中使用的相同模式，生成樣本計分資料。 此資料用於生成計分資料幀，然後轉換為計分字典。 請查看 *即時ML* 的子版本。

![評分資料](../images/rtml/generate-score-data.png)

### 對邊緣端點進行分數

在 *即時ML* 對您進行評分的模板 [!DNL Edge] 服務。

![對邊評分](../images/rtml/scoring-edge.png)

一旦評分完成， [!DNL Edge] URL、負載和來自 [!DNL Edge] 的子菜單。

## 從 [!DNL Edge]

在 [!DNL Edge]，運行以下代碼單元格。 無法編輯或刪除此單元格。

```python
services = edge_utils.list_deployed_services()
print(services)
```

返回的響應是已部署服務的陣列。

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## 從中刪除已部署的應用或服務ID [!DNL Edge] （可選）

>[!CAUTION]
>
>此單元格用於刪除已部署的邊緣應用程式。 除非需要刪除已部署的單元格，否則不要使用以下單元格 [!DNL Edge] 的子菜單。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 後續步驟

按照上面的教程，您已成功培訓ONNX模型並將其上載到Real-time Machine Learning模型儲存。 此外，您還對即時機器學習模型進行了評分並進行了部署。 如果希望瞭解有關可用於模型創作的節點的更多資訊，請訪問 [節點參考指南](./node-reference.md)。
