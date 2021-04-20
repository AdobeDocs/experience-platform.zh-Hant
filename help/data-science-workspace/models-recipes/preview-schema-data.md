---
keywords: Experience Platform；預覽模式資料；資料科學工作區；熱門主題
solution: Experience Platform
title: 預覽零售銷售結構和資料集
topic: tutorial
type: Tutorial
description: 以下文檔概述了在Adobe Experience Platform上預覽模式和資料集。
translation-type: tm+mt
source-git-commit: 5129a75071af680bc54a7f60bb89ce32d3216d09
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 1%

---


# 預覽零售銷售模式和資料集

成功完成[零售銷售模式和dataset](./create-retails-sales-dataset.md)教程中的引導指令碼後。 可在[!DNL Experience Platform]上查看輸出方案和資料集。 要查看方案和資料集，請執行以下步驟：

選擇位於左側導航中的&#x200B;**[!UICONTROL 方案]**&#x200B;頁籤，並查找由引導指令碼建立的輸入方案。 架構的名稱將與上一步驟中在`config.yaml`中定義的名稱相對應。 按一下查看架構詳細資訊及其組成。

![](../images/models-recipes/access-data/schema.PNG)

選擇位於左側導覽中的&#x200B;**[!UICONTROL Datasets]**&#x200B;標籤，並開啟透過選取資料集名稱所建立的輸入資料集。 資料集的名稱與前一步驟中在`config.yaml`中定義的名稱相對應。

![](../images/models-recipes/access-data/dataset.PNG)

選擇位於右上角的&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以預覽資料集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 後續步驟

您現在已使用提供的引導指令碼成功將零售銷售示例資料吸收到[!DNL Experience Platform]中。

要繼續使用收錄的資料：
- [使用Jupyter Notebooks分析資料](../jupyterlab/analyze-your-data.md)
   - 使用[!DNL Data Science Workspace]中的Jupyter Notebooks來存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝至配方](./package-source-files-recipe.md)
   - 請依照本教學課程，瞭解如何將來源檔案封裝在可匯入的方式檔案中，將您自己的模型帶入[!DNL Data Science Workspace]。