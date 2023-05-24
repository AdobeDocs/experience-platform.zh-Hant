---
keywords: Experience Platform；導入打包的配方；資料科學工作區；熱門主題；配方；ui；建立引擎
solution: Experience Platform
title: 在Data Science工作區UI中導入打包的配方
type: Tutorial
description: 本教程提供了使用所提供的零售銷售示例配置和導入打包處方的方法。 在本教程結束時，您將準備好在Adobe Experience Platform資料科學工作區中建立、培訓和評估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 在Data Science Workspace UI中導入打包的處方

本教程提供了使用所提供的零售銷售示例配置和導入打包處方的方法。 在本教程結束時，您將準備好在Adobe Experience Platform建立、培訓和評估模型 [!DNL Data Science Workspace]。

## 先決條件

本教程要求以Docker影像URL的形式包裝配方。 請參閱有關如何 [將源檔案打包到配方](./package-source-files-recipe.md) 的子菜單。

## UI工作流

將打包的處方導入 [!DNL Data Science Workspace] 需要特定的處方配置，並編譯為單個JavaScript對象表示法(JSON)檔案，此處方配置的編譯稱為配置檔案。 具有特定組配置的包裝配方稱為配方實例。 一個處方可用於在 [!DNL Data Science Workspace]。

導入包處方的工作流包含以下步驟：
- [配置處方](#configure)
- [導入基於Docker的配方 — Python](#python)
- [導入基於Docker的處方 — R](#r)
- [導入基於Docker的配方 — PySpark](#pyspark)
- [導入基於Docker的處方 — Scala](#scala)

### 配置處方 {#configure}

中的每個食譜實例 [!DNL Data Science Workspace] 附帶了一組配置，這些配置將定制配方實例以適應特定的使用案例。 配置檔案定義使用此處方實例建立的模型的預設培訓和評分行為。

>[!NOTE]
>
>配置檔案是處方和案例特定的。

下面是一個示例配置檔案，其中顯示了零售銷售處方的預設培訓和評分行為。

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
| `learning_rate` | 數字 | 漸變乘法的標量。 |
| `n_estimators` | 數字 | 隨機林分類器林中的樹數。 |
| `max_depth` | 數字 | 隨機森林分類器中樹的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字串 | 逗號分隔的輸入架構屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字串 | 以逗號分隔的輸出架構屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布林值 | 確定輸入和輸出特徵是否可修改 |
| `tenantId` | 字串 | 此ID確保您建立的資源與組織中的資源同名並包含在組織中。 [請執行此處的步驟](../../xdm/api/getting-started.md#know-your-tenant_id) 找到您的租戶ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字串 | 用於訓練模型的輸入模式。 在UI中導入時保留此空，在使用API導入時替換為培訓SchemaID。 |
| `evaluation.labelColumn` | 字串 | 用於計算可視化的列標籤。 |
| `evaluation.metrics` | 字串 | 要用於評估模型的評估度量清單，以逗號分隔。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字串 | 用於對模型進行計分的輸出架構。 在UI中導入時保留此空，在使用API導入時替換為記分SchemaID。 |

在本教程中，您可以將零售銷售處方的預設配置檔案保留在 [!DNL Data Science Workspace] 參考他們的方式。

### 導入基於Docker的處方 —  [!DNL Python] {#python}

從導航和選擇開始 **[!UICONTROL 工作流]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入處方** 選擇 **[!UICONTROL 啟動]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 的 **導入處方** 工作流。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方](./package-source-files-recipe.md) 教程，在使用Python源檔案構建零售銷售處方時提供了Docker URL。

一旦你在 **選擇源** 頁，貼上與使用 [!DNL Python] 源檔案 **[!UICONTROL 源URL]** 的子菜單。 接下來，通過拖放導入提供的配置檔案，或使用檔案系統 **瀏覽器**。 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`。 選擇 **[!UICONTROL 蟒]** 的 **運行時** 下降 **[!UICONTROL 分類]** 的 **類型** 下拉。 一旦所有內容都填好，選擇 **[!UICONTROL 下一個]** 在右上角繼續 **管理架構**。

>[!NOTE]
>
> 類型支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**。 如果模型不屬於這些類型之一，請選擇 **[!UICONTROL 自定義]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下來，選擇一節下的零售銷售輸入和輸出方案 **管理架構**，是使用中提供的引導指令碼建立的 [建立零售銷售模式和資料集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 **功能管理** 部分，在架構查看器中選擇租戶標識以展開零售銷售輸入架構。 通過加亮所需特徵並選擇其中一種來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 的子菜單。 在本教程中，請設定 **[!UICONTROL 每週銷售]** 的  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**。 選擇 **[!UICONTROL 下一個]** 查看新配置的配方。

根據需要複查處方、添加、修改或刪除配置。 選擇 **[!UICONTROL 完成]** 建立處方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 瞭解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售處方。

### 導入基於Docker的處方 — R {#r}

從導航和選擇開始 **[!UICONTROL 工作流]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入處方** 選擇 **[!UICONTROL 啟動]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 的 **導入處方** 工作流。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方](./package-source-files-recipe.md) 教程，在使用R源檔案構建零售銷售處方時提供了Docker URL。

一旦你在 **選擇源** 頁面中，貼上與使用R源檔案構建的打包配方對應的Docker URL **[!UICONTROL 源URL]** 的子菜單。 接下來，通過拖放導入提供的配置檔案，或使用檔案系統 **瀏覽器**。 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`。 選擇 **[!UICONTROL R]** 的 **運行時** 下降 **[!UICONTROL 分類]** 的 **類型** 下拉。 一旦所有內容都填好，選擇 **[!UICONTROL 下一個]** 在右上角繼續 **管理架構**。

>[!NOTE]
>
> *類型* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**。 如果模型不屬於這些類型之一，請選擇 **[!UICONTROL 自定義]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下來，選擇一節下的零售銷售輸入和輸出方案 **管理架構**，是使用中提供的引導指令碼建立的 [建立零售銷售模式和資料集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 *功能管理* 部分，在架構查看器中選擇租戶標識以展開零售銷售輸入架構。 通過加亮所需特徵並選擇其中一種來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 的子菜單。 在本教程中，請設定 **[!UICONTROL 每週銷售]** 的  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**。 選擇 **[!UICONTROL 下一個]** 複查新配置的配方。

根據需要複查處方、添加、修改或刪除配置。 選擇 **完成** 建立處方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 瞭解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售處方。

### 導入基於Docker的配方 — PySpark {#pyspark}

從導航和選擇開始 **[!UICONTROL 工作流]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入處方** 選擇 **[!UICONTROL 啟動]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 的 **導入處方** 工作流。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方](./package-source-files-recipe.md) 教程，在使用PySpark源檔案構建零售銷售處方的結束時提供了Docker URL。

一旦你在 **選擇源** 頁，將與使用PySpark源檔案構建的打包配方對應的Docker URL貼上到 **[!UICONTROL 源URL]** 的子菜單。 接下來，通過拖放導入提供的配置檔案，或使用檔案系統 **瀏覽器**。 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`。 選擇 **[!UICONTROL PySpark]** 的 **運行時** 下拉。 選擇PySpark運行時後，預設對象將自動填充到 **[!UICONTROL 多克]**。 下一步，選擇 **[!UICONTROL 分類]** 的 **類型** 下拉。 一旦所有內容都填好，選擇 **[!UICONTROL 下一個]** 在右上角繼續 **管理架構**。

>[!NOTE]
>
> *類型* 支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**。 如果模型不屬於這些類型之一，請選擇 **[!UICONTROL 自定義]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下來，使用 **管理架構** selector ，是使用在 [建立零售銷售模式和資料集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理架構](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架構查看器中選擇租戶標識以展開零售銷售輸入架構。 通過加亮所需特徵並選擇其中一種來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 的子菜單。 在本教程中，請設定 **[!UICONTROL 每週銷售]** 的  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**。 選擇 **[!UICONTROL 下一個]** 查看新配置的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

根據需要複查處方、添加、修改或刪除配置。 選擇 **[!UICONTROL 完成]** 建立處方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 瞭解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售處方。

### 導入基於Docker的處方 — Scala {#scala}

從導航和選擇開始 **[!UICONTROL 工作流]** 位於 [!DNL Platform] UI。 下一步，選擇 **導入處方** 選擇 **[!UICONTROL 啟動]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 的 **導入處方** 工作流。 輸入處方的名稱和說明，然後選擇 **[!UICONTROL 下一個]** 在右上角繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [將源檔案打包到配方](./package-source-files-recipe.md) 教程，在使用Scala構建零售銷售處方時提供了Docker URL([!DNL Spark])源檔案。

一旦你在 **選擇源** 頁，在「源URL」欄位中貼上與使用Scala源檔案生成的打包配方對應的Docker URL。 接下來，通過拖放導入提供的配置檔案，或使用檔案系統瀏覽器。 可在以下位置找到提供的配置檔案： `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`。 選擇 **[!UICONTROL 火花]** 的 **運行時** 下拉。 一旦 [!DNL Spark] 運行時被選中，預設項目將自動填充到 **[!UICONTROL 多克]**。 下一步，選擇 **[!UICONTROL 回歸]** 從 **類型** 下拉。 一旦所有內容都填好，選擇 **[!UICONTROL 下一個]** 在右上角繼續 **管理架構**。

>[!NOTE]
>
> 類型支援 **[!UICONTROL 分類]** 和 **[!UICONTROL 回歸]**。 如果模型不屬於這些類型之一，請選擇 **[!UICONTROL 自定義]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下來，使用 **管理架構** selector ，是使用在 [建立零售銷售模式和資料集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理架構](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架構查看器中選擇租戶標識以展開零售銷售輸入架構。 通過加亮所需特徵並選擇其中一種來選擇輸入和輸出特徵 **[!UICONTROL 輸入功能]** 或 **[!UICONTROL 目標功能]** 在右邊 **[!UICONTROL 欄位屬性]** 的子菜單。 在本教程中，請設定&quot;[!UICONTROL 每週銷售]的  **[!UICONTROL 目標功能]** 其他一切 **[!UICONTROL 輸入功能]**。 選擇 **[!UICONTROL 下一個]** 查看新配置的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

根據需要複查處方、添加、修改或刪除配置。 選擇 **[!UICONTROL 完成]** 建立處方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續 [後續步驟](#next-steps) 瞭解如何在 [!DNL Data Science Workspace] 使用新建立的零售銷售處方。

## 後續步驟 {#next-steps}

本教程提供了有關配置和將處方導入到 [!DNL Data Science Workspace]。 現在，您可以使用新建立的配方建立、訓練和評估模型。

- [在UI中訓練和評估模型](./train-evaluate-model-ui.md)
- [使用API訓練和評估模型](./train-evaluate-model-api.md)
