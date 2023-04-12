---
keywords: Experience Platform；匯入封裝配方；Data Science Workspace；熱門主題；配方；ui；建立引擎
solution: Experience Platform
title: 在Data Science Workspace UI中匯入封裝方式
type: Tutorial
description: 本教學課程透過提供的零售銷售範例，深入分析如何設定和匯入封裝方式。 在本教學課程結束前，您將準備好在Adobe Experience Platform Data Science Workspace中建立、訓練和評估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 在Data Science Workspace UI中匯入封裝方式

本教學課程透過提供的零售銷售範例，深入分析如何設定和匯入封裝方式。 在本教學課程結束前，您已準備好在Adobe Experience Platform中建立、訓練和評估模型 [!DNL Data Science Workspace].

## 先決條件

本教學課程需要以Docker影像URL形式包裝的配方。 請參閱如何 [將源檔案打包到配方中](./package-source-files-recipe.md) 以取得更多資訊。

## UI工作流程

將打包的配方導入 [!DNL Data Science Workspace] 需要特定方式設定，並編譯為單一JavaScript物件標籤法(JSON)檔案中，此方式設定的編譯稱為設定檔案。 帶有特定配置集的打包配方稱為配方實例。 一個配方可用於建立許多配方實例， [!DNL Data Science Workspace].

匯入套件方式的工作流程包含下列步驟：
- [設定方式](#configure)
- [導入基於Docker的配方 — Python](#python)
- [導入基於Docker的配方 — R](#r)
- [導入基於Docker的配方 — PySpark](#pyspark)
- [導入基於Docker的配方 — Scala](#scala)

### 設定方式 {#configure}

中的每個配方實例 [!DNL Data Science Workspace] 隨附一組設定，可量身打造符合特定使用案例的方式例項。 配置檔案定義使用此配方實例建立的模型的預設培訓和評分行為。

>[!NOTE]
>
>組態檔是方式和案例專屬檔案。

以下是顯示「零售銷售」方式預設培訓和評分行為的範例設定檔案。

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
| `learning_rate` | 數字 | 梯度乘的標量。 |
| `n_estimators` | 數字 | 隨機森林分類器的林中的樹數。 |
| `max_depth` | 數字 | 隨機森林分類器中樹的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字串 | 逗號分隔的輸入架構屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字串 | 逗號分隔的輸出架構屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布林值 | 確定輸入和輸出特徵是否可修改 |
| `tenantId` | 字串 | 此ID可確保您建立的資源與組織命名時間正確，且內容完整。 [請依照此處的步驟操作](../../xdm/api/getting-started.md#know-your-tenant_id) 找到您的租用戶ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字串 | 用於訓練模型的輸入結構。 在UI中匯入時，請保留此空白，在使用API匯入時，請以訓練SchemaID取代。 |
| `evaluation.labelColumn` | 字串 | 評估視覺效果的欄標籤。 |
| `evaluation.metrics` | 字串 | 用於評估模型的評估度量清單（以逗號分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字串 | 用於對模型進行計分的輸出架構。 在UI中匯入時，請將此保留空白，在使用API匯入時，以計分SchemaID取代。 |

在本教學課程中，您可以保留零售銷售方式的預設設定檔案，位於 [!DNL Data Science Workspace] 參考其原樣。

### 導入基於Docker的配方 —  [!DNL Python] {#python}

首先，導覽並選取 **[!UICONTROL 工作流程]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入方式** 選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **導入方式** 工作流程隨即出現。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方中](./package-source-files-recipe.md) 教程，在使用Python源檔案構建零售銷售方式結束時提供了Docker URL。

一旦您加入 **選擇源** 頁面，貼上與使用 [!DNL Python] 源檔案 **[!UICONTROL 源URL]** 欄位。 接下來，拖放以匯入所提供的設定檔案，或使用檔案系統 **瀏覽器**. 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 選擇 **[!UICONTROL Python]** 在 **執行階段** 下拉並 **[!UICONTROL 分類]** 在 **類型** 下拉。 填妥所有內容後，請選取 **[!UICONTROL 下一個]** 在右上角繼續 **管理結構**.

>[!NOTE]
>
> 類型支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果模型不屬於以下類型之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下來，選取區段下的零售銷售輸入和輸出結構 **管理結構**，則會使用中提供的引導指令碼來建立 [建立零售銷售結構和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 **功能管理** 區段中，在結構檢視器中選取「租戶」識別，以展開「零售銷售」輸入結構。 通過突出顯示所需特徵並選擇任一特徵來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 窗口。 在本教學課程中，請設定 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**. 選擇 **[!UICONTROL 下一個]** 來檢閱新設定的方式。

視需要檢閱方式、新增、修改或移除設定。 選擇 **[!UICONTROL 完成]** 來建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 要了解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售方式。

### 導入基於Docker的配方 — R {#r}

首先，導覽並選取 **[!UICONTROL 工作流程]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入方式** 選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **導入方式** 工作流程隨即出現。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方中](./package-source-files-recipe.md) 教學課程中，使用R來源檔案建立零售銷售方式結束時，會提供Docker URL。

一旦您加入 **選擇源** 頁面，將與使用R源檔案建立的封裝方式對應的Docker URL貼到 **[!UICONTROL 源URL]** 欄位。 接下來，拖放以匯入所提供的設定檔案，或使用檔案系統 **瀏覽器**. 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 選擇 **[!UICONTROL R]** 在 **執行階段** 下拉並 **[!UICONTROL 分類]** 在 **類型** 下拉。 填妥所有內容後，請選取 **[!UICONTROL 下一個]** 在右上角繼續 **管理結構**.

>[!NOTE]
>
> *類型* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果模型不屬於以下類型之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下來，選取區段下的零售銷售輸入和輸出結構 **管理結構**，則會使用中提供的引導指令碼來建立 [建立零售銷售結構和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 *功能管理* 區段中，在結構檢視器中選取「租戶」識別，以展開「零售銷售」輸入結構。 通過突出顯示所需特徵並選擇任一特徵來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 窗口。 在本教學課程中，請設定 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**. 選擇 **[!UICONTROL 下一個]** 來檢閱新的已設定方式。

視需要檢閱方式、新增、修改或移除設定。 選擇 **完成** 來建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 要了解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售方式。

### 導入基於Docker的配方 — PySpark {#pyspark}

首先，導覽並選取 **[!UICONTROL 工作流程]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入方式** 選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **導入方式** 工作流程隨即出現。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 來繼續。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方中](./package-source-files-recipe.md) 教學課程中，使用PySpark來源檔案建立零售銷售方式結束時會提供Docker URL。

一旦您加入 **選擇源** 頁面，將與使用PySpark源檔案構建的打包方式對應的Docker URL貼到 **[!UICONTROL 源URL]** 欄位。 接下來，拖放以匯入所提供的設定檔案，或使用檔案系統 **瀏覽器**. 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 選擇 **[!UICONTROL PySpark]** 在 **執行階段** 下拉。 選擇PySpark運行時後，預設工件會自動填充到 **[!UICONTROL Docker]**. 下一步，選擇 **[!UICONTROL 分類]** 在 **類型** 下拉。 填妥所有內容後，請選取 **[!UICONTROL 下一個]** 在右上角繼續 **管理結構**.

>[!NOTE]
>
> *類型* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果模型不屬於以下類型之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下來，使用 **管理結構** 選取器中，結構是使用 [建立零售銷售結構和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![管理結構](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 區段中，在結構檢視器中選取「租戶」識別，以展開「零售銷售」輸入結構。 通過突出顯示所需特徵並選擇任一特徵來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 窗口。 在本教學課程中，請設定 **[!UICONTROL weeklySales]** 作為  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**. 選擇 **[!UICONTROL 下一個]** 來檢閱新設定的方式。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱方式、新增、修改或移除設定。 選擇 **[!UICONTROL 完成]** 來建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 要了解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售方式。

### 導入基於Docker的配方 — Scala {#scala}

首先，導覽並選取 **[!UICONTROL 工作流程]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入方式** 選取 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **設定** 頁面 **導入方式** 工作流程隨即出現。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 來繼續。

![設定工作流程](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方中](./package-source-files-recipe.md) 教學課程中，使用Scala建立零售銷售方式([!DNL Spark])源檔案。

一旦您加入 **選擇源** 頁，在「源URL」欄位中貼上與使用Scala源檔案構建的打包方式對應的Docker URL。 接下來，拖放以匯入提供的設定檔案，或使用檔案系統瀏覽器。 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 選擇 **[!UICONTROL 火花]** 在 **執行階段** 下拉。 一旦 [!DNL Spark] 運行時被選中，預設對象會自動填充到 **[!UICONTROL Docker]**. 下一步，選擇 **[!UICONTROL 回歸]** 從 **類型** 下拉。 填妥所有內容後，請選取 **[!UICONTROL 下一個]** 在右上角繼續 **管理結構**.

>[!NOTE]
>
> 類型支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**. 如果模型不屬於以下類型之一，請選取 **[!UICONTROL 自訂]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下來，使用 **管理結構** 選取器中，結構是使用 [建立零售銷售結構和資料集](../models-recipes/create-retails-sales-dataset.md) 教學課程。

![管理結構](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 區段中，在結構檢視器中選取「租戶」識別，以展開「零售銷售」輸入結構。 通過突出顯示所需特徵並選擇任一特徵來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 窗口。 在本教學課程中，請設定「[!UICONTROL weeklySales]」作為  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**. 選擇 **[!UICONTROL 下一個]** 來檢閱新設定的方式。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱方式、新增、修改或移除設定。 選擇 **[!UICONTROL 完成]** 來建立方式。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 要了解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售方式。

## 後續步驟 {#next-steps}

本教學課程深入分析如何設定及將配方匯入 [!DNL Data Science Workspace]. 您現在可以使用新建立的方式建立、訓練和評估模型。

- [在UI中訓練和評估模型](./train-evaluate-model-ui.md)
- [使用API訓練和評估模型](./train-evaluate-model-api.md)
