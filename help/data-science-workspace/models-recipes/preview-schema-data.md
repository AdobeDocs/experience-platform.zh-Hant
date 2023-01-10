---
keywords: Experience Platform；預覽結構資料；Data Science Workspace；熱門主題
solution: Experience Platform
title: 預覽零售銷售結構和資料集
type: Tutorial
description: 下列檔案概述在Adobe Experience Platform上預覽結構和資料集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 預覽零售銷售結構和資料集

成功完成引導指令碼後，從 [零售銷售結構和資料集](./create-retails-sales-dataset.md) 教學課程。 可在 [!DNL Experience Platform]. 若要檢視結構和資料集，請遵循下列步驟：

選取 **[!UICONTROL 結構]** 頁簽（位於左側導航中），並查找由引導指令碼建立的輸入架構。 架構的名稱將對應於 `config.yaml` 從上一步開始。 按一下即可檢視結構詳細資訊及其組成。

![](../images/models-recipes/access-data/schema.PNG)

選取 **[!UICONTROL 資料集]** 標籤，並開啟透過選取資料集名稱所建立的輸入資料集。 資料集的名稱與 `config.yaml` 從上一步開始。

![](../images/models-recipes/access-data/dataset.PNG)

選擇 **[!UICONTROL 預覽資料集]** 位於右上角，可預覽資料集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 後續步驟

您現在已成功將零售銷售範例資料擷取至 [!DNL Experience Platform] 使用提供的引導指令碼。

若要繼續使用擷取的資料：
- [使用Jupyter Notebooks分析資料](../jupyterlab/analyze-your-data.md)
   - 在中使用Jupyter Notebooks [!DNL Data Science Workspace] 存取、探索、視覺化和了解您的資料。
- [將源檔案打包到配方中](./package-source-files-recipe.md)
   - 請依照本教學課程，了解如何將您自己的模型帶入 [!DNL Data Science Workspace] 將源檔案打包成可導入的方式檔案。
