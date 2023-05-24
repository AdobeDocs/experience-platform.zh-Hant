---
keywords: Experience Platform；預覽模式資料；Data Science Workspace；熱門主題
solution: Experience Platform
title: 預覽零售銷售方案和資料集
type: Tutorial
description: 以下文檔概述了在Adobe Experience Platform上預覽架構和資料集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 預覽零售銷售架構和資料集

從中成功完成引導指令碼後 [零售銷售模式和資料集](./create-retails-sales-dataset.md) 教程。 可以在上查看輸出架構和資料集 [!DNL Experience Platform]。 要查看架構和資料集，請執行以下步驟：

選擇 **[!UICONTROL 架構]** 頁籤，並查找由引導指令碼建立的輸入模式。 架構的名稱將與中定義的 `config.yaml` 從上一步開始。 通過按一下查看架構詳細資訊及其組成。

![](../images/models-recipes/access-data/schema.PNG)

選擇 **[!UICONTROL 資料集]** 頁籤，然後開啟通過選擇資料集名稱建立的輸入資料集。 資料集的名稱與中定義的 `config.yaml` 從上一步開始。

![](../images/models-recipes/access-data/dataset.PNG)

選擇 **[!UICONTROL 預覽資料集]** 位於右上角，可預覽資料集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 後續步驟

您現在已成功將零售銷售示例資料 [!DNL Experience Platform] 使用提供的引導指令碼。

要繼續處理所攝取的資料：
- [使用Jupyter筆記本分析資料](../jupyterlab/analyze-your-data.md)
   - 在中使用Jupyter筆記本 [!DNL Data Science Workspace] 訪問、瀏覽、可視化和瞭解資料。
- [將源檔案打包到配方](./package-source-files-recipe.md)
   - 按照本教程學習如何將您自己的模型引入 [!DNL Data Science Workspace] 將源檔案打包到可導入的配方檔案中。
