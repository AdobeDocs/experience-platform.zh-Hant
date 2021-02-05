---
keywords: Experience Platform；預覽模式資料；Data Science Workspace；熱門主題
solution: Experience Platform
title: 預覽零售銷售結構和資料集
topic: tutorial
type: Tutorial
description: 以下檔案概述在Adobe Experience Platform上預覽架構和資料集。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 預覽零售銷售模式和資料集

成功完成[建立零售銷售模式和dataset](./create-retails-sales-dataset.md)教學課程的引導指令碼後。 可在[!DNL Experience Platform]上查看輸出方案和資料集。 要查看方案和資料集，請執行以下步驟：

1. 按一下左側導航列中的&#x200B;**[!UICONTROL 方案]**&#x200B;連結，並查找由引導指令碼建立的輸入方案。 架構的名稱將與上一步驟中在`config.yaml`中定義的名稱相對應。 按一下查看架構詳細資訊及其組成。

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 按一下左側導覽欄中的&#x200B;**[!UICONTROL Dataces]**&#x200B;連結，並開啟透過按一下清單名稱所建立的輸入資料集。 資料集的名稱會與前一步驟中在`config.yaml`中定義的名稱相對應。

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 按一下位於右上方的「預覽資料集」，預覽資料集的子集。****

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 後續步驟

您現在已使用提供的引導指令碼成功將零售銷售示例資料吸收到[!DNL Experience Platform]中。

要繼續使用收錄的資料：
- [使用Jupyter Notebooks分析資料](../jupyterlab/analyze-your-data.md)
   - 使用[!DNL Data Science Workspace]中的Jupyter Notebooks來存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝至配方](./package-source-files-recipe.md)
   - 請依照本教學課程，瞭解如何將來源檔案封裝在可匯入的方式檔案中，將您自己的模型帶入[!DNL Data Science Workspace]。