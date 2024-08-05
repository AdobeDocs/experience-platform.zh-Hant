---
keywords: Experience Platform;開發者指南;數據科學工作環境;熱門話題;實時機器學習;節點參考;
solution: Experience Platform
title: 管理即時機器學習筆記本
description: 以下指南概述了在 Adobe Experience Platform JupyterLab 中版本編號實時機器學習應用程式所需的步驟。
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 0%

---

# 管理即時機器學習筆記本 （Alpha）

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

>[!IMPORTANT]
>
>即時機器學習尚不適用於所有使用者。 此功能處於 Alpha 階段，仍在測試中。 本檔可能隨時變更。

以下指南概述了版本編號實時機器學習應用程式所需的步驟。 使用Adobe Systems提供的 **[!UICONTROL 即時 ML]** Python 筆記本範本，此指南涵蓋培訓模型、創建 DSL、將 DSL 發佈到 Edge 以及對請求進行評分。 當您逐步實作即時機器學習模型時，預計您會修改範本以符合資料集的需求。

## 建立即時機器學習筆記本

在Adobe Experience Platform UI中，從&#x200B;**資料科學**&#x200B;中選取&#x200B;**[!UICONTROL 筆記本]**。 接著，選取&#x200B;**[!UICONTROL JupyterLab]**，讓環境有時間載入。

![開啟JupyterLab](../images/rtml/open-jupyterlab.png)

此時 [!DNL JupyterLab] 將顯示啟動器。 向下捲動至&#x200B;*即時機器學習*&#x200B;並選取&#x200B;**[!UICONTROL 即時ML]**&#x200B;筆記本。 將打開一個範本，其中包含帶有示例資料集的示例筆記本單元格。

![空白蟒蛇](../images/rtml/authoring-notebook.png)

## 匯入和探索節點

首先，匯入模型所需的所有套件。 請確定已匯入您計畫用於節點編寫的任何套件。

>[!NOTE]
>
>您的匯入清單可能會因您想要建立的模型而異。 此清單將隨著時間新增新節點而變更。 如需可用節點的完整清單，請參閱[節點參考指南](./node-reference.md)。

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

下列程式碼儲存格會列印可用節點清單。

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![筆記清單](../images/rtml/node-list.png)

## 訓練實時機器學習模型

使用以下選項之一，您將編寫 [!DNL Python] 代碼來讀取、預處理和分析數據。 下一個，您需要訓練自己的 ML 模型，將其序列化為 ONNX 格式然後將其上傳實時機器學習模型商店。

- [在JupyterLab筆記型電腦中訓練您自己的模型](#training-your-own-model)
- [將您自己預先訓練的ONNX模型上傳到JupyterLab Notebooks](#pre-trained-model-upload)

### 訓練您自己的模型 {#training-your-own-model}

從載入您的訓練資料開始。

>[!NOTE]
>
>在&#x200B;**即時ML**&#x200B;範本中，[汽車保險CSV資料集](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance)是從[!DNL Github]擷取的。

![載入訓練資料](../images/rtml/load_training.png)

如果您想在Adobe Experience Platform內部使用資料集，請取消下面的單元格註釋。 下一個，您需要替換為 `DATASET_ID` 適當的值。

![RTML 資料集](../images/rtml/rtml-dataset.png)

若要訪問筆記本中的[!DNL JupyterLab]資料集，請選擇 導覽左側[!DNL JupyterLab]的“**數據**&#x200B;標籤”。此時 **[!UICONTROL 將顯示數據集]** 和 **[!UICONTROL 架構]** 目錄。 選擇 **[!UICONTROL 數據集]** 並按下滑鼠右鍵，然後從要使用的資料集上的下拉功能表中選擇「 **[!UICONTROL 瀏覽筆記本]** 中的數據」 選項。 筆記本底部將顯示一個可執行代碼條目。 該儲存格包含您的 `dataset_id`.

![資料集訪問許可權](../images/rtml/access-dataset.png)

完成後，右鍵按下並刪除在筆記本底部生成的儲存格。

### 訓練屬性

使用提供的範本，修改 中的任何 `config_properties`培訓屬性。

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### 準備模型

**[!UICONTROL 使用即時 ML]** 範本，您需要分析、預處理、訓練和評估 ML 模型。這是通過應用數據轉換和構建培訓管道來完成的。

**數據轉換**

**[!UICONTROL 需要修改即時 ML]** 範本&#x200B;**資料轉換儲存格**&#x200B;才能使用您自己的資料集。通常，這涉及重命名列、數據統計和數據準備/特徵工程。

>[!NOTE]
>
>為了便於 `[ ... ]`閱讀，以下示例已使用 進行壓縮。 請視圖並展開 *完整代碼單元格的即時 ML* 範本數據轉換部分。

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

運行提供的儲存格以查看範例結果。 從資料集 返回 `carinsurancedataset.csv` 的輸出表將返回您定義的修改。

![數據轉換範例](../images/rtml/table-return.png)

**訓練管道**

下一個需要創建培訓管道。 這看起來與任何其他培訓管道文件類似，除了您需要轉換並生成 ONNX 檔。

使用上一個儲存格中定義的數據轉換，修改範本。 下面突出顯示的以下代碼用於在功能管道中生成 ONNX 檔。 請為完整的管道代碼單元視圖 *即時 ML* 範本。

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

完成培訓管道並通過數據轉換修改數據后，請使用以下單元格運行培訓。

```python
model = train(config_properties, df_final)
```

### 生成和上傳 ONNX 模型

成功完成培訓運行后，需要生成 ONNX 模型，並將已訓練的模型上傳到實時機器學習模型商店。 運行以下單元格后，ONNX 模型將顯示在左側邊欄中，與所有其他筆記本一起顯示。

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>`model_path`更改字串值 （`model.onnx`） 以更改模型的名稱。

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>以下儲存格不可編輯或刪除，需要即時機器學習應用程式才能正常工作。

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX 模型](../images/rtml/onnx-model-rail.png)

### 上傳你自己的預訓練 ONNX 模型 {#pre-trained-model-upload}

使用筆記本中的 [!DNL JupyterLab] 上傳 按鈕，將預先訓練的 ONNX 模型上傳到 [!DNL Data Science Workspace] 筆記本環境。

![上傳圖示](../images/rtml/upload.png)

下一個，請更改`model_path`即時 ML *筆記本中的*&#x200B;字串值以匹配 ONNX 模型名稱。完成後，運行“ *設置模型路徑* ”單元，然後運行 *“將模型上傳到 RTML 模型存儲* ”單元。 成功后，回應中會返回模型位置和模型ID。

![上傳自己的模型](../images/rtml/upload-own-model.png)

## 域特定語言 （DSL） 建立

本部分概述了如何創建 DSL。 您將創作包含任何數據預處理以及 ONNX 節點的節點。 下一個，使用節點和邊創建 DSL 圖。 邊會使用元組型格式(node_1、node_2)連線節點。 圖表不應有週期。

>[!IMPORTANT]
>
>必須使用ONNX節點。 如果沒有ONNX節點，應用程式將會失敗。

### 節點製作

>[!NOTE]
>
> 根據使用的資料型別，您可能會有多個節點。 以下示例僅概述了即時 ML *範本中的*&#x200B;單個節點。如需完整的代碼單元，請視圖 *即時 ML* 範本 *節點創作* 部分。

下面的 Pandas 節點用於 `"import": "map"` 將方法名稱作為字串導入參數，然後將參數輸入為映射函數。 以下範例使用`{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`來執行此操作。 地圖就位后，您可以選擇設定為 `inplace` `True` 或 `False`。 根據您是否要套用轉換，將`inplace`設為`True`或`False`。 根據預設，`"inplace": False`會建立新資料行。 提供新欄名稱的支援已設定為在後續版本中新增。 最後一行`cols`可以是單一資料行名稱或資料行清單。 指定要套用轉換的欄。 在此範例中，指定了`leasing`。 如需有關可用節點及其使用方式的詳細資訊，請瀏覽[節點參考指南](./node-reference.md)。

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

### 建立DSL圖表

建立節點後，下一步就是將節點鏈結在一起，以建立圖形。

開始通過構建陣列出屬於圖形一部分的所有節點。

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

下一個，用邊連接節點。 每個元組都是一個 [!DNL Edge] 連接。

>[!TIP]
>
> 由于節點彼此線性依賴（每個節點都取決於前一個節點的輸出），因此您可以使用簡單的 Python 清單理解來創建連結。 如果節點相依於多個輸入，請新增您自己的連線。

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

節點連線後，即可建置圖形。 下方的儲存格為必要儲存格，無法編輯或刪除。

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

完成之後，會傳回`edge`物件，其中包含每個節點以及與節點對應的引數。

![邊緣傳回](../images/rtml/edge-return.png)

## Publish至Edge （中樞）

>[!NOTE]
>
>實時機器學習臨時部署到 Adobe Experience Platform 中心並由其管理。 有關更多詳細信息，造訪有關實時機器學習體系結構](./home.md#architecture)的[概述部分。

建立 DSL 圖形後，可以將圖形部署到 [!DNL Edge].

>[!IMPORTANT]
>
>不要經常發佈 [!DNL Edge] ，這可能會使 [!DNL Edge] 節點過載。 不建議多次發佈同一模型。

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### 更新 DSL 並重新發布到 Edge（可選）

如果不需要更新 DSL，可以跳到 [評分](#scoring)。

>[!NOTE]
>
>僅當您要更新已發佈到Edge的現有DSL時，才需要以下單元格。

您的模型可能會繼續開發。 您可以使用新模型更新現有服務，而不是建立全新的服務。 您可以定義要更新的節點、指派新的ID，然後將新的DSL重新上傳至[!DNL Edge]。

在下列範例中，節點 0 更新為新 ID。

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![更新節點](../images/rtml/updated-node.png)

更新 節點 ID 后，可以將更新的 DSL 重新發佈到 Edge。

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

您會傳回更新的DSL。

![已更新DSL](../images/rtml/updated-dsl.png)

## 評分 {#scoring}

發佈至[!DNL Edge]後，評分會由使用者端的POST要求完成。 通常可以從需要ML分數的使用者端應用程式完成。 您也可以從Postman執行此作業。 **[!UICONTROL 即時機器學習]**&#x200B;範本使用EdgeUtils來演示此過程。

>[!NOTE]
>
>在開始計分之前，需要少量的處理時間。

```python
# Wait for the app to come up
import time
time.sleep(20)
```

使用在培訓 中使用的相同綱要，生成示例評分數據。 此数据用于版本編號評分数据幀，然後轉換為評分字典。 請視圖 *完整代碼單元的即時 ML* 範本。

![評分數據](../images/rtml/generate-score-data.png)

### 針對邊緣終結點得分

使用即時 ML *範本中的*&#x200B;以下儲存格對服務進行[!DNL Edge]評分。

![得分對抗邊緣](../images/rtml/scoring-edge.png)

評分完成後， [!DNL Edge] 將返回的 [!DNL Edge] URL、有效負載和評分輸出。

## 從 [!DNL Edge]

若要在 上 [!DNL Edge]生成當前部署的應用清單，請運行以下代碼單元。 無法編輯或刪除該儲存格。

```python
services = edge_utils.list_deployed_services()
print(services)
```

返回的回應是已部署服務的陣列。

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

## 刪除已部署的應用或服務 ID （ [!DNL Edge] 可選）

>[!CAUTION]
>
>此單元用於刪除已部署的Edge應用程式。 除非您需要刪除已部署 [!DNL Edge] 的應用程式，否則請勿使用以下單元格。

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## 後續步驟

按照上述教學課程操作，你已成功訓練 ONNX 模型並將其上傳到實時機器學習模型商店。 此外，你已對即時機器學習模型進行評分和部署。 如果要了解有關可用于模型創作的節點的詳細信息，造訪 [節點參考指南](./node-reference.md)。
