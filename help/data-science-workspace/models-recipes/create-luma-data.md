---
keywords: Experience Platform;luma Web資料；資料科學工作區；熱門主題；配方；演示資料；demo Web資料；luma資料
solution: Experience Platform
title: 建立Luma Web架構和資料集
type: Tutorial
description: 本教程為您提供了Luma演示傾向模型所需的先決條件和資產。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 建立Luma傾向模型架構和資料集

本教程為您提供所有其他元件所需的必備元件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教程。 完成後，您和您的組織將可以使用以下架構和資料集。

**綱要:**

- Luma Web資料架構
- 傾向模型評分結果模式

**資料集:**

- Luma Web資料集
- 傾向模型訓練資料集
- 傾向模型評分資料集
- 傾向模型評分結果資料集

## 下載資產 {#assets}

下面的教程使用自定義Luma採購傾向模型。 在繼續之前， [下載所需資產](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip資料夾。 此資料夾包含：

- 購買傾向模型筆記本
- 用於將資料接收到訓練和評分資料集（Luma Web資料的子集）的筆記本
- 包含730,000個Luma用戶的Web資料的演示JSON檔案
- 可選的Python 3 EDA（探索性資料分析）筆記本，可用於幫助理解Web資料和模型。

>[!NOTE]
>
> 您可以使用自己的架構和資料進行任何教程。 但是，資產中提供的演示模型不起作用，除非它提供了正確的配置檔案和要求檔案。 此演示傾向模型設計用於處理Luma Web資料。

### 建立Luma Web資料架構並接收資料

要建立模型，必須在平台中有一個資料集，該資料集用於訓練和計分模型。 以下視頻教程 [資料科學工作區課程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 指導您建立Luma架構並接收採購傾向模型使用的資料。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 建立培訓、評分和評分結果資料集

為了運行處方生成器筆記本或使用API對模型進行培訓和評分，您需要指定用於培訓/評分的資料集和方案。 以下視頻教程將指導您設定培訓、評分和評分結果資料集，以及Luma購買傾向模型中使用的評分結果模式。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 後續步驟

按照本教程，您已成功為Luma傾向模型建立了所需的架構和資料集。 現在，您可以繼續下一教程，並使用 [配方生成器筆記本](../jupyterlab/create-a-model.md) 教程。

此外，您還可以使用提供的「探索資料分析」(EDA)筆記本來瀏覽資料。 此筆記本可用於幫助理解Luma資料中的模式、檢查資料健全性，並匯總預測傾向模型的相關資料。 要瞭解有關探索性資料分析的更多資訊，請訪問 [EDA文檔](../jupyterlab/eda-notebook.md)。
