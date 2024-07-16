---
keywords: Experience Platform；預覽結構描述資料；資料科學Workspace；熱門主題
solution: Experience Platform
title: 預覽零售銷售結構描述和資料集
type: Tutorial
description: 以下檔案會概述如何在Adobe Experience Platform上預覽結構描述和資料集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# 預覽零售銷售結構描述和資料集

成功完成[零售銷售結構描述和資料集](./create-retails-sales-dataset.md)教學課程中的啟動程式指令碼後。 可以在[!DNL Experience Platform]上檢視輸出結構描述和資料集。 若要檢視結構描述和資料集，請遵循以下步驟：

選取位於左側導覽的&#x200B;**[!UICONTROL 結構描述]**&#x200B;索引標籤，並尋找由啟動程式指令碼建立的輸入結構描述。 結構描述的名稱將對應到上一步驟在`config.yaml`中定義的名稱。 按一下以檢視結構描述詳細資訊及其組成。

![](../images/models-recipes/access-data/schema.PNG)

選取位於左側導覽的&#x200B;**[!UICONTROL 資料集]**&#x200B;索引標籤，並開啟透過選取資料集名稱所建立的輸入資料集。 資料集的名稱對應到上一步驟在`config.yaml`中定義的名稱。

![](../images/models-recipes/access-data/dataset.PNG)

選取位於右上角的&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以預覽資料集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 後續步驟

您現在已使用提供的啟動程式指令碼，成功將零售業樣本資料擷取到[!DNL Experience Platform]。

若要繼續使用內嵌的資料：
- [使用 Jupyter Notebooks 分析您的資料](../jupyterlab/analyze-your-data.md)
   - 在[!DNL Data Science Workspace]中使用Jupyter Notebooks來存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝到配方中](./package-source-files-recipe.md)
   - 按照本教學課程瞭解如何將您自己的模型封裝在可匯入的「配方」檔案中，並帶入[!DNL Data Science Workspace]。
