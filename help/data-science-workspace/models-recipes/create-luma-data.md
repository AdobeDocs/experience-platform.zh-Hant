---
keywords: Experience Platform;Luma網站資料；Data Science Workspace；熱門主題；訣竅；示範資料；示範網站資料；Luma資料
solution: Experience Platform
title: 建立Luma Web結構和資料集
type: Tutorial
description: 本教學課程提供Luma示範傾向模型所需的必要條件和資產。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# 建立Luma傾向模型結構和資料集

本教學課程提供所有其他必要條件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教學課程。 完成後，您和IMS組織將能使用下列結構和資料集。

**綱要:**

- Luma網站資料結構
- 傾向模型分數結果結構

**資料集:**

- Luma網頁資料集
- 傾向模型訓練資料集
- 傾向模型計分資料集
- 傾向模型計分結果資料集

## 下載資產 {#assets}

下列教學課程使用自訂Luma購買傾向模型。 在繼續之前， [下載所需資產](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip資料夾。 此資料夾包含：

- 購買傾向模型筆記本
- 用於將資料內嵌至訓練和計分資料集（Luma網路資料的子集）的筆記型電腦
- 包含730,000名Luma使用者Web資料的示範JSON檔案
- 可選的Python 3 EDA（探索資料分析）筆記型電腦，可用於幫助了解Web資料和模型。

>[!NOTE]
>
> 您可以在任何教學課程中使用自己的結構和資料。 不過，資產中提供的示範模型無法運作，除非已提供正確的設定檔案和需求檔案。 此示範傾向模型旨在搭配Luma網頁資料使用。

### 建立Luma Web資料結構並擷取資料

若要建立模型，您必須在Platform中擁有資料集，以便訓練和評分模型。 以下教學課程影片來自 [Data Science Workspace課程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 逐步引導您建立Luma結構，以及擷取購買傾向模型所使用的資料。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 建立培訓、評分和評分結果資料集

若要執行方式產生器筆記型電腦或使用API來訓練和計分模型，您必須指定用於訓練/計分的資料集和結構。 以下影片教學課程會逐步引導您建立訓練、計分和計分結果資料集，以及Luma購買傾向模型中使用的計分結果結構。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 後續步驟

依照本教學課程，您已成功建立Luma傾向模型的必要結構和資料集。 您現在已準備好繼續下一個教學課程，並使用 [配方生成器筆記型電腦](../jupyterlab/create-a-model.md) 教學課程。

此外，您也可以使用提供的探索資料分析(EDA)筆記型電腦來探索資料。 此筆記型電腦可協助您了解Luma資料中的模式、檢查資料的健全度，以及為預測傾向模型總結相關資料。 若要進一步了解探索資料分析，請造訪 [EDA檔案](../jupyterlab/eda-notebook.md).
