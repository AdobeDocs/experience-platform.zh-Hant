---
keywords: Experience Platform；導入打包的配方；資料科學工作區；熱門主題；配方；ui；建立引擎
solution: Experience Platform
title: 在Data Science Workspace UI中匯入封裝配方
topic: tutorial
type: Tutorial
description: 本教學課程提供如何使用提供的零售銷售範例來設定和匯入封裝方式的見解。 在本教學課程結束時，您將準備好在Adobe Experience Platform資料科學工作區中建立、訓練和評估模型。
translation-type: tm+mt
source-git-commit: 13fa4af388c6f31768a6b7e1da05cb56c5635c9e
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 0%

---


# 在Data Science Workspace UI中匯入封裝的方式

本教學課程提供如何使用提供的零售銷售範例來設定和匯入封裝方式的見解。 在本教學課程結束時，您將準備好在Adobe Experience Platform[!DNL Data Science Workspace]中建立、訓練和評估模型。

## 先決條件

本教學課程需要以Docker影像URL格式封裝的配方。 如需詳細資訊，請參閱[將來源檔案封裝至Recipe](./package-source-files-recipe.md)的教學課程。

## UI工作流程

將封裝配方匯入[!DNL Data Science Workspace]需要特定配方組態，並編譯為單一JavaScript物件注釋(JSON)檔案，此配方組態編譯稱為組態檔。 具有一組特定配置的打包配方稱為配方實例。 一個配方可用於在[!DNL Data Science Workspace]中建立多個配方實例。

用於導入包配方的工作流包括以下步驟：
- [設定方式](#configure)
- [匯入以Docker為基礎的方式- Python](#python)
- [導入基於Docker的配方- R](#r)
- [匯入以Docker為基礎的方式- PySpark](#pyspark)
- [導入基於Docker的配方- Scala](#scala)

### 配置配方{#configure}

[!DNL Data Science Workspace]中的每個配方實例都附帶一組配置，這些配置將配方實例定制為適合特定使用案例。 配置檔案定義使用此配方實例建立的模型的預設培訓和計分行為。

>[!NOTE]
>
>配置檔案是特定於配方和大小寫的。

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
| `tenantId` | 字串 | 此ID可確保您建立的資源具有正確的命名空間，並且包含在IMS組織中。 [請依照此處的](../../xdm/api/getting-started.md#know-your-tenant_id) 步驟尋找您的租用戶ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字串 | 用於訓練模型的輸入模式。 在UI中匯入時保留此空白，在使用API匯入時，以訓練架構ID取代。 |
| `evaluation.labelColumn` | 字串 | 評估視覺化的欄標籤。 |
| `evaluation.metrics` | 字串 | 用於評估模型的評估度量的逗號分隔清單。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字串 | 用於計分模型的輸出方案。 在UI中匯入時保留此空白，在使用API匯入時，以計分SchemaID取代。 |

在本教程中，您可以保留[!DNL Data Science Workspace]參考零售銷售配方的預設配置檔案。

### 導入基於Docker的配方- [!DNL Python] {#python}

首先，導覽並選擇位於[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL Workflows]**。 接著，選擇&#x200B;**Import recipe**&#x200B;並選擇&#x200B;**[!UICONTROL Launch]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會顯示&#x200B;**匯入方式**&#x200B;工作流程的&#x200B;**設定**&#x200B;頁面。 輸入配方的名稱和說明，然後在右上角選擇&#x200B;**[!UICONTROL Next]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[將來源檔案封裝成Recipe](./package-source-files-recipe.md)教學課程中，在使用Python來源檔案建立零售銷售方式時，會提供Docker URL。

在&#x200B;**選擇源**&#x200B;頁面上，將與使用[!DNL Python]源檔案構建的打包配方對應的Docker URL貼上到&#x200B;**[!UICONTROL Source URL]**&#x200B;欄位中。 接著，拖放以匯入所提供的設定檔案，或使用檔案系統&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/python/retail/retail.config.json`找到提供的配置檔案。 在&#x200B;**Runtime**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Python]**，在&#x200B;**Type**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Classification]**。 一旦填寫完所有內容，請選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**管理結構**。

>[!NOTE]
>
> 類型支援&#x200B;**[!UICONTROL Classification]**&#x200B;和&#x200B;**[!UICONTROL Regression]**。 如果您的型號不屬於其中一種類型，請選擇&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接著，在&#x200B;**管理結構**&#x200B;一節下選擇零售銷售輸入和輸出結構描述，這些結構描述是使用[中提供的引導指令碼建立零售銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md)教程中建立的。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;**功能管理**&#x200B;區段下，在架構檢視器中選取您的租用戶識別碼，以展開零售銷售輸入架構。 反白顯示所要的功能，然後在右側的&#x200B;**[!UICONTROL Field Properties]**&#x200B;視窗中選取&#x200B;**[!UICONTROL Input Feature]**&#x200B;或&#x200B;**[!UICONTROL Target Feature]**，以選擇輸入和輸出功能。 在本教學課程中，請將&#x200B;**[!UICONTROL weeklySales]**&#x200B;設為&#x200B;**[!UICONTROL Target Feature]**，並將其他項目設為&#x200B;**[!UICONTROL Input Feature]**。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以查看新配置的配方。

視需要檢閱方式、新增、修改或移除組態。 選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續執行[後續步驟](#next-steps)，瞭解如何使用新建立的零售銷售方式在[!DNL Data Science Workspace]中建立模型。

### 導入基於Docker的配方- R {#r}

首先，導覽並選擇位於[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL Workflows]**。 接著，選擇&#x200B;**Import recipe**&#x200B;並選擇&#x200B;**[!UICONTROL Launch]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會顯示&#x200B;**匯入方式**&#x200B;工作流程的&#x200B;**設定**&#x200B;頁面。 輸入配方的名稱和說明，然後在右上角選擇&#x200B;**[!UICONTROL Next]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[將來源檔案封裝成Recipe](./package-source-files-recipe.md)教學課程中，在使用R來源檔案建立零售銷售方式時，會提供Docker URL。

在&#x200B;**選擇源**&#x200B;頁面上，將與使用R源檔案構建的打包配方對應的Docker URL貼上到&#x200B;**[!UICONTROL Source URL]**&#x200B;欄位中。 接著，拖放以匯入所提供的設定檔案，或使用檔案系統&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`找到提供的配置檔案。 在&#x200B;**Runtime**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL R]**，在&#x200B;**Type**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Classification]**。 一旦填寫完所有內容，請選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**管理結構**。

>[!NOTE]
>
> *打* 字支援 **[!UICONTROL Classification]** 和 **[!UICONTROL Regression]**。如果您的型號不屬於其中一種類型，請選擇&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接著，在&#x200B;**管理結構**&#x200B;一節下選擇零售銷售輸入和輸出結構描述，這些結構描述是使用[中提供的引導指令碼建立零售銷售結構描述和資料集](../models-recipes/create-retails-sales-dataset.md)教程中建立的。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;*功能管理*&#x200B;區段下，在架構檢視器中選取您的租用戶識別碼，以展開零售銷售輸入架構。 反白顯示所要的功能，然後在右側的&#x200B;**[!UICONTROL Field Properties]**&#x200B;視窗中選取&#x200B;**[!UICONTROL Input Feature]**&#x200B;或&#x200B;**[!UICONTROL Target Feature]**，以選擇輸入和輸出功能。 在本教學課程中，請將&#x200B;**[!UICONTROL weeklySales]**&#x200B;設為&#x200B;**[!UICONTROL Target Feature]**，並將其他項目設為&#x200B;**[!UICONTROL Input Feature]**。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以查看新的「已配置」配方。

視需要檢閱方式、新增、修改或移除組態。 選擇&#x200B;**完成**&#x200B;以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續執行[後續步驟](#next-steps)，瞭解如何使用新建立的零售銷售方式在[!DNL Data Science Workspace]中建立模型。

### 匯入以Docker為基礎的方式- PySpark {#pyspark}

首先，導覽並選擇位於[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL Workflows]**。 接著，選擇&#x200B;**Import recipe**&#x200B;並選擇&#x200B;**[!UICONTROL Launch]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會顯示&#x200B;**匯入方式**&#x200B;工作流程的&#x200B;**設定**&#x200B;頁面。 輸入配方的名稱和說明，然後在右上角選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[將來源檔案封裝成Recipe](./package-source-files-recipe.md)教學課程中，使用PySpark來源檔案建立零售銷售方式時，會提供Docker URL。

在&#x200B;**選取來源**&#x200B;頁面上，將與使用PySpark來源檔案建立之封裝方式對應的Docker URL貼入&#x200B;**[!UICONTROL Source URL]**&#x200B;欄位。 接著，拖放以匯入所提供的設定檔案，或使用檔案系統&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`找到提供的配置檔案。 在&#x200B;**Runtime**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL PySpark]**。 在選取PySpark執行時期後，預設對象會自動填入至&#x200B;**[!UICONTROL Docker]**。 接著，在&#x200B;**Type**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Classification]**。 一旦填寫完所有內容，請選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**管理結構**。

>[!NOTE]
>
> *打* 字支援 **[!UICONTROL Classification]** 和 **[!UICONTROL Regression]**。如果您的型號不屬於其中一種類型，請選擇&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下來，使用&#x200B;**管理方案**&#x200B;選擇器選擇零售銷售輸入和輸出方案，使用[中提供的引導指令碼建立方案並建立零售銷售方案和資料集](../models-recipes/create-retails-sales-dataset.md)教程。

![管理結構](../images/models-recipes/import-package-ui/manage-schemas.png)

在&#x200B;**功能管理**&#x200B;區段下，在架構檢視器中選取您的租用戶識別碼，以展開零售銷售輸入架構。 反白顯示所要的功能，然後在右側的&#x200B;**[!UICONTROL Field Properties]**&#x200B;視窗中選取&#x200B;**[!UICONTROL Input Feature]**&#x200B;或&#x200B;**[!UICONTROL Target Feature]**，以選擇輸入和輸出功能。 在本教學課程中，請將&#x200B;**[!UICONTROL weeklySales]**&#x200B;設為&#x200B;**[!UICONTROL Target Feature]**，並將其他項目設為&#x200B;**[!UICONTROL Input Feature]**。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以查看新配置的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱方式、新增、修改或移除組態。 選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續執行[後續步驟](#next-steps)，瞭解如何使用新建立的零售銷售方式在[!DNL Data Science Workspace]中建立模型。

### 導入基於Docker的配方- Scala {#scala}

首先，導覽並選擇位於[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL Workflows]**。 接著，選擇&#x200B;**Import recipe**&#x200B;並選擇&#x200B;**[!UICONTROL Launch]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此時會顯示&#x200B;**匯入方式**&#x200B;工作流程的&#x200B;**設定**&#x200B;頁面。 輸入配方的名稱和說明，然後在右上角選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[將源檔案打包到Recipe](./package-source-files-recipe.md)教程中，在使用Scala([!DNL Spark])源檔案構建零售銷售方式的結束時提供了Docker URL。

在&#x200B;**選擇源**&#x200B;頁面上，將與使用源URL欄位中的Scala源檔案構建的打包配方對應的Docker URL貼上到「源URL」欄位中。 接著，透過拖放方式匯入提供的設定檔案，或使用檔案系統瀏覽器。 可在`experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`找到提供的配置檔案。 在&#x200B;**Runtime**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Spark]**。 選擇[!DNL Spark]運行時後，預設對象將自動填充到&#x200B;**[!UICONTROL Docker]**。 接著，從&#x200B;**Type**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Regression]**。 一旦填寫完所有內容，請選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**管理結構**。

>[!NOTE]
>
> 類型支援&#x200B;**[!UICONTROL Classification]**&#x200B;和&#x200B;**[!UICONTROL Regression]**。 如果您的型號不屬於其中一種類型，請選擇&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下來，使用&#x200B;**管理方案**&#x200B;選擇器選擇零售銷售輸入和輸出方案，使用[中提供的引導指令碼建立方案並建立零售銷售方案和資料集](../models-recipes/create-retails-sales-dataset.md)教程。

![管理結構](../images/models-recipes/import-package-ui/manage-schemas.png)

在&#x200B;**功能管理**&#x200B;區段下，在架構檢視器中選取您的租用戶識別碼，以展開零售銷售輸入架構。 反白顯示所要的功能，然後在右側的&#x200B;**[!UICONTROL Field Properties]**&#x200B;視窗中選取&#x200B;**[!UICONTROL Input Feature]**&#x200B;或&#x200B;**[!UICONTROL Target Feature]**，以選擇輸入和輸出功能。 在本教學課程中，請將&quot;[!UICONTROL weeklySales]&quot;設為&#x200B;**[!UICONTROL Target Feature]**，而將其他項目設為&#x200B;**[!UICONTROL Input Feature]**。 選擇&#x200B;**[!UICONTROL Next]**&#x200B;以查看新配置的配方。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

視需要檢閱方式、新增、修改或移除組態。 選擇&#x200B;**[!UICONTROL Finish]**&#x200B;以建立配方。

![](../images/models-recipes/import-package-ui/recipe_review.png)

繼續執行[後續步驟](#next-steps)，瞭解如何使用新建立的零售銷售方式在[!DNL Data Science Workspace]中建立模型。

## 下一步 {#next-steps}

本教學課程提供有關設定方式並將方式匯入[!DNL Data Science Workspace]的深入資訊。 您現在可以使用新建立的方式建立、訓練和評估模型。

- [在UI中訓練和評估模型](./train-evaluate-model-ui.md)
- [使用API來訓練和評估模型](./train-evaluate-model-api.md)