---
keywords: Experience Platform；luma網路資料；資料科學Workspace；熱門主題；配方；示範資料；示範網路資料；luma資料
solution: Experience Platform
title: 建立Luma網頁結構描述和資料集
type: Tutorial
description: 本教學課程提供Luma示範傾向模型所需的必要條件和資產。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 建立Luma傾向模型結構描述和資料集

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

此教學課程提供您所有其他[!DNL Adobe Experience Platform] [!DNL Data Science Workspace]教學課程所需的先決條件和資產。 完成後，您和您的組織將可以使用以下結構描述和資料集。

**結構描述：**

- Luma Web資料結構
- 傾向模型評分結果結構描述

**資料集：**

- Luma網路資料集
- 傾向性模型訓練資料集
- 傾向模型評分資料集
- 傾向模型評分結果資料集

## 下載資產 {#assets}

以下教學課程使用自訂Luma購買傾向模型。 繼續之前，[下載必要的資產](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) zip資料夾。 此資料夾包含：

- 購買傾向性機型筆記型電腦
- 用來將資料內嵌至訓練和評分資料集（Luma網路資料的子集）的筆記本
- 包含730,000名Luma使用者之網頁資料的示範JSON檔案
- 選購的Python 3 EDA （探索資料分析）筆記型電腦，可用來協助瞭解網路資料和模型。

>[!NOTE]
>
> 您可以將自己的結構和資料用於任何教學課程。 但是，除非提供適當的組態檔和需求檔案，否則資產中提供的示範模型無法運作。 此示範傾向模型旨在搭配Luma網頁資料使用。

### 建立Luma Web資料結構描述並擷取資料

為了建立模型，Platform中必須有資料集，可用來對模型進行訓練和評分。 下列來自[Data Science Workspace課程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw)的影片教學課程，將逐步引導您建立Luma結構描述及擷取購買傾向模型使用的資料。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 建立訓練、評分和評分結果資料集

若要執行配方產生器筆記本或使用API來訓練和評分模型，您必須指定用於訓練/評分的資料集和結構描述。 以下影片教學課程會逐步引導您設定訓練、評分和評分結果資料集，以及Luma購買傾向模型中使用的評分結果結構描述。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 後續步驟

依照本教學課程，您已成功建立Luma傾向模型所需的結構描述和資料集。 您現在已準備好繼續下一個教學課程，並使用[配方產生器筆記本](../jupyterlab/create-a-model.md)教學課程建立模型。

此外，您可以使用提供的探索資料分析(EDA)筆記本來探索資料。 此筆記本可用來協助瞭解Luma資料中的模式、檢查資料健全度，並總結預測傾向模型的相關資料。 若要進一步瞭解探索資料分析，請造訪[EDA檔案](../jupyterlab/eda-notebook.md)。
