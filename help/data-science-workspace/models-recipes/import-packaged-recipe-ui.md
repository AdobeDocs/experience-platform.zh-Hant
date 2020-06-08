---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 匯入封裝的方式(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: f2a7300d4ad75e3910abbdf2ecc2946a2dfe553c
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 0%

---


# 匯入封裝的方式(UI)

本教學課程提供如何使用提供的零售銷售範例來設定和匯入封裝方式的見解。 在本教學課程結束時，您將準備好在Adobe Experience Platform資料科學工作區中建立、訓練和評估模型。

## 必要條件

本教學課程需要以Docker影像URL格式封裝的配方。 如需詳細資訊，請參 [閱教學課程，瞭解如何將來源檔案封裝至配方](./package-source-files-recipe.md) 。

## UI工作流程

將封裝的方式匯入Data Science Workspace需要特定的方式設定，並編譯為單一JavaScript物件標籤(JSON)檔案，此方式組態編譯稱為設定 **檔案**。 具有一組特定配置的打包配方稱為配方 **實例**。 在「資料科學工作區」中，可使用一種方式建立許多方式例項。

用於導入包配方的工作流包括以下步驟：
- [設定方式](#configure)
- [匯入以Docker為基礎的方式- Python](#python)
- [導入基於Docker的配方- R](#r)
- [匯入以Docker為基礎的方式- PySpark](#pyspark)
- [導入基於Docker的配方- Scala](#scala)

### 設定方式 {#configure}

「資料科學工作區」中的每個配方實例都隨附一組配置，可根據特定使用案例量身打造配方實例。 配置檔案定義使用此配方實例建立的模型的預設培訓和計分行為。

>[!NOTE] 配置檔案是特定於配方和大小寫的。

以下是顯示零售銷售方式預設訓練和評分行為的範例設定檔案。

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| 參數鍵 | 類型 | 說明 |
| ----- | ----- | ----- |
| `learning_rate` | 數字 | 漸層乘法的標量。 |
| `n_estimators` | 數字 | 隨機森林分類器的林中樹數。 |
| `max_depth` | 數字 | 隨機森林分類器中樹的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字串 | 逗號分隔的輸入模式屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字串 | 逗號分隔的輸出模式屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布林值 | 確定輸入和輸出特徵是否可修改 |
| `tenantId` | 字串 | 此ID可確保您建立的資源具有正確的命名空間，並且包含在IMS組織中。 [請依照此處的步驟](../../xdm/api/getting-started.md#know-your-tenant_id) ，尋找您的租用戶ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字串 | 用於訓練模型的輸入模式。 在UI中匯入時保留此空白，在使用API匯入時，以訓練架構ID取代。 |
| `evaluation.labelColumn` | 字串 | 評估視覺化的欄標籤。 |
| `evaluation.metrics` | 字串 | 用於評估模型的評估度量的逗號分隔清單。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字串 | 用於計分模型的輸出方案。 在UI中匯入時保留此空白，在使用API匯入時，以計分SchemaID取代。 |

在本教學課程中，您可以將「Data Science Workspace參考」中「零售銷售」配方的預設設定檔保留為原樣。

### 匯入以Docker為基礎的方式- Python {#python}

首先，導覽並選 **[!UICONTROL 取]** 「平台UI」左上角的「工作流程」。 接著，選取「匯 *入方式* 」，然後按一 **[!UICONTROL 下「啟動」]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會 *顯示* 「匯入方式 ** 」工作流程的「設定」頁面。 輸入處方的名稱和說明，然後在右 **[!UICONTROL 上角]** 選擇「下一步」。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> 在「將 [來源檔案封裝為配方」教學課程中](./package-source-files-recipe.md) ，使用Python來源檔案建立零售銷售配方時，會提供Docker URL。

在「選擇來源 *」頁面上，將與使用Python來源檔案建立的封裝方式對應的Docker URL貼入「來源* URL **** 」欄位。 接著，透過拖放方式匯入提供的設定檔案，或使用檔案系統瀏 **覽器**。 可在中找到提供的配置檔案 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`。 在「 **[!UICONTROL Runtime]** 」下拉式清單中選取「 *Python* 」，並在「 **[!UICONTROL Type]** ** Drop」中選取「Classification」。 一切填妥後，按一下右 **[!UICONTROL 上角的]** 「下一步」，繼續 *管理結構*。

>[!NOTE]
> *類型&#x200B;*支援&#x200B;**[!UICONTROL 分類]**和&#x200B;**[!UICONTROL 回歸]**。 如果模型未落在其中一種類型下，請選擇「自&#x200B;**[!UICONTROL 訂」]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接著，在「管理結構」一節下選擇「零售銷售」輸入和輸出結構，這些結構是使用建立零售銷售結構和資料集教程中提供的 *引導指令碼建立的*[](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在「功 *能管理* 」區段下，按一下架構檢視器中的租用戶識別碼，以展開「零售銷售」輸入架構。 通過反白顯示所需特徵，並在右側的「欄位屬性」(Field Properties)窗口中選擇「輸入特徵」( **[!UICONTROL Input Feature]** )或「目標特徵」( **[!UICONTROL Target Feature]** )，來選擇輸入和輸 **[!UICONTROL 出特徵]** 。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 設為 **[!UICONTROL Target功能]** ，而將其他項目設為 **[!UICONTROL 輸入功能]**。 按一 **[!UICONTROL 下「下一步]** 」以檢閱新設定的方式。

視需要檢閱方式、新增、修改或移除組態。 按一 **[!UICONTROL 下「完成]** 」以建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

請繼續下 [一步](#next-steps) ，瞭解如何使用新建立的零售銷售方式，在資料科學工作區中建立模型。

### 導入基於Docker的配方- R {#r}

首先，導覽並選 **[!UICONTROL 取]** 「平台UI」左上角的「工作流程」。 接著，選取「匯 *入方式* 」，然後按一 **[!UICONTROL 下「啟動」]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會 *顯示* 「匯入方式 ** 」工作流程的「設定」頁面。 輸入處方的名稱和說明，然後在右 **[!UICONTROL 上角]** 選擇「下一步」。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> 在將來 [源檔案打包到配方教程中](./package-source-files-recipe.md) ，在使用R源檔案構建零售銷售配方的結束處提供了Docker URL。

在「選擇源 *」頁上，將與使用R源檔案構建的打包方式對應的Docker URL貼上到「源URL」* 欄位中 **** 。 接著，透過拖放方式匯入提供的設定檔案，或使用檔案系統瀏 **覽器**。 可在中找到提供的配置檔案 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`。 在「 **[!UICONTROL Runtime]** 」下拉式清單中選取「R *」，在「Type* **[!UICONTROL drop」中選取「Classification]**** 」。 一切填妥後，按一下右 **[!UICONTROL 上角的]** 「下一步」，繼續 *管理結構*。

>[!NOTE]
> *類型&#x200B;*支援&#x200B;**[!UICONTROL 分類]**和&#x200B;**[!UICONTROL 回歸]**。 如果模型未落在其中一種類型下，請選擇「自&#x200B;**[!UICONTROL 訂」]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接著，在「管理結構」一節下選擇「零售銷售」輸入和輸出結構，這些結構是使用建立零售銷售結構和資料集教程中提供的 *引導指令碼建立的*[](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在「功 *能管理* 」區段下，按一下架構檢視器中的租用戶識別碼，以展開「零售銷售」輸入架構。 通過反白顯示所需特徵，並在右側的「欄位屬性」(Field Properties)窗口中選擇「輸入特徵」( **[!UICONTROL Input Feature]** )或「目標特徵」( **[!UICONTROL Target Feature]** )，來選擇輸入和輸 **[!UICONTROL 出特徵]** 。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 設為 **[!UICONTROL Target功能]** ，而將其他項目設為 **[!UICONTROL 輸入功能]**。 按一 **[!UICONTROL 下「下一]** 步」以檢閱新的「已設定」方式。

視需要檢閱方式、新增、修改或移除組態。 按一 **下「完成** 」以建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

請繼續下 [一步](#next-steps) ，瞭解如何使用新建立的零售銷售方式，在資料科學工作區中建立模型。

### 匯入以Docker為基礎的方式- PySpark {#pyspark}

首先，導覽並選 **[!UICONTROL 取]** 「平台UI」左上角的「工作流程」。 接著，選取「匯 *入方式* 」，然後按一 **[!UICONTROL 下「啟動」]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會 *顯示* 「匯入方式 ** 」工作流程的「設定」頁面。 輸入處方的名稱和說明，然後在右上角 **[!UICONTROL 選擇]** 「下一步」以繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> 在將來 [源檔案封裝至配方教學課程中](./package-source-files-recipe.md) ，使用PySpark來源檔案建立零售銷售配方時，會提供Docker URL。

在「選取來源 *」頁面上，將對應於使用PySpark來源檔案建立之封裝方式的Docker URL貼入「來源URL」欄* 位中 **** 。 接著，透過拖放方式匯入提供的設定檔案，或使用檔案系統瀏 **覽器**。 可在中找到提供的配置檔案 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`。 在「 **[!UICONTROL 執行階段]** 」下拉式清單中選 *取PySpark* 。 在選取PySpark執行時期後，預設對象會自動填入 **[!UICONTROL Docker]**。 接著，在「 **[!UICONTROL 類型]** 」下拉式清 *單中選* 取「分類」。 一切填妥後，按一下右 **[!UICONTROL 上角的]** 「下一步」，繼續 *管理結構*。

>[!NOTE]
> *類型&#x200B;*支援&#x200B;**[!UICONTROL 分類]**和&#x200B;**[!UICONTROL 回歸]**。 如果模型未落在其中一種類型下，請選擇「自&#x200B;**[!UICONTROL 訂」]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接著，在「管理結構」一節下選擇「零售銷售」輸入和輸出結構，這些結構是使用建立零售銷售結構和資料集教程中提供的 *引導指令碼建立的*[](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在「功 *能管理* 」區段下，按一下架構檢視器中的租用戶識別碼，以展開「零售銷售」輸入架構。 通過反白顯示所需特徵，並在右側的「欄位屬性」(Field Properties)窗口中選擇「輸入特徵」( **[!UICONTROL Input Feature]** )或「目標特徵」( **[!UICONTROL Target Feature]** )，來選擇輸入和輸 **[!UICONTROL 出特徵]** 。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 設為 **[!UICONTROL Target功能]** ，而將其他項目設為 **[!UICONTROL 輸入功能]**。 按一 **[!UICONTROL 下「下一步]** 」以檢閱新設定的方式。

視需要檢閱方式、新增、修改或移除組態。 按一 **[!UICONTROL 下「完成]** 」以建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

請繼續下 [一步](#next-steps) ，瞭解如何使用新建立的零售銷售方式，在資料科學工作區中建立模型。

### 導入基於Docker的配方- Scala {#scala}

首先，導覽並選 **[!UICONTROL 取]** 「平台UI」左上角的「工作流程」。 接著，選取「匯 *入方式* 」，然後按一 **[!UICONTROL 下「啟動」]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會 *顯示* 「匯入方式 ** 」工作流程的「設定」頁面。 輸入處方的名稱和說明，然後在右上角 **[!UICONTROL 選擇]** 「下一步」以繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> 在「將來 [源檔案封裝至配方」教學課程中](./package-source-files-recipe.md) ，使用Scala(Spark)來源檔案建立零售銷售配方時，會提供Docker URL。

在「選擇源 *」頁上，將與使用「源URL」欄位中的Scala源檔案構建的打包方式對應的Docker URL* 貼上到 ** 。 接著，透過拖放方式匯入提供的設定檔案，或使用檔案系統瀏 **覽器**。 可在中找到提供的配置檔案 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`。 在「 **[!UICONTROL Runtime]** 」下拉式清 *單中選* 取Spark。 在選取Spark執行時期後，預設對象會自動填入 **[!UICONTROL Docker]**。 接著，從「 **[!UICONTROL 類型]** 」下拉式選 *取「回歸* 」。 一切填妥後，按一下右 **[!UICONTROL 上角的]** 「下一步」，繼續 *管理結構*。

>[!NOTE]
> *類型&#x200B;*支援&#x200B;**[!UICONTROL 分類]**和&#x200B;**[!UICONTROL 回歸]**。 如果模型未落在其中一種類型下，請選擇「自&#x200B;**[!UICONTROL 訂」]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接著，在「管理結構」一節下選擇「零售銷售」輸入和輸出結構，這些結構是使用建立零售銷售結構和資料集教程中提供的 *引導指令碼建立的*[](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在「功 *能管理* 」區段下，按一下架構檢視器中的租用戶識別碼，以展開「零售銷售」輸入架構。 通過反白顯示所需特徵，並在右側的「欄位屬性」(Field Properties)窗口中選擇「輸入特徵」( **[!UICONTROL Input Feature]** )或「目標特徵」( **[!UICONTROL Target Feature]** )，來選擇輸入和輸 **[!UICONTROL 出特徵]** 。 在本教學課程中，請將 **[!UICONTROL weeklySales]** 設為 **[!UICONTROL Target功能]** ，而將其他項目設為 **[!UICONTROL 輸入功能]**。 按一 **[!UICONTROL 下「下一步]** 」以檢閱新設定的方式。

視需要檢閱方式、新增、修改或移除組態。 按一 **[!UICONTROL 下「完成]** 」以建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

請繼續下 [一步](#next-steps) ，瞭解如何使用新建立的零售銷售方式，在資料科學工作區中建立模型。

## 下一步 {#next-steps}

本教學課程提供如何設定方式並將其匯入Data Science Workspace的深入資訊。 您現在可以使用新建立的方式建立、訓練和評估模型。

- [在UI中訓練和評估模型](./train-evaluate-model-ui.md)
- [使用API來訓練和評估模型](./train-evaluate-model-api.md)