---
keywords: Experience Platform；逐步介紹；資料科學工作區；熱門主題
solution: Experience Platform
title: Data Science Workspace逐步說明
topic-legacy: Walkthrough
description: 本檔案提供Adobe Experience Platform資料科學工作區的逐步說明。 尤其是資料科學家將透過的一般工作流程，來解決使用機器學習的問題。
exl-id: d814846e-52a9-46c6-831a-3399241959f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 漫步

本檔案提供Adobe Experience Platform[!DNL Data Science Workspace]的逐步解說。 本教學課程概述一般資料科學家的工作流程，以及他們如何運用機器學習來解決問題。

## 先決條件

- 註冊的Adobe ID帳戶
   - Adobe ID帳戶必須已添加到具有訪問Adobe Experience Platform和[!DNL Data Science Workspace]權限的組織。

## 零售使用案例

零售商在保持現有市場競爭力方面面臨許多挑戰。 零售商的主要顧慮之一，是決定產品的最佳價格，並預測銷售趨勢。 借助精確的預測模型，零售商將能夠找到需求與定價政策之間的關係，並做出最佳化定價決策，以實現銷售與收入最大化。

## 資料科學家的解決方案

資料科學家的解決方案是運用零售商提供的豐富歷史資訊，預測未來趨勢並最佳化定價決策。 本逐步介紹使用過去的銷售資料來訓練機器學習模型，並使用模型來預測未來的銷售趨勢。 有了這項功能，您就可以產生深入資訊，協助您進行最佳價格變更。

此概述反映資料科學家在取得資料集和建立模型以預測每週銷售的步驟。 本教學課程在Adobe Experience Platform[!DNL Data Science Workspace]的「Sample Retail Sales Notebook」（零售銷售筆記本）中涵蓋以下各節：

- [設定](#setup)
- [探索資料](#exploring-data)
- [功能工程](#feature-engineering)
- [訓練與驗證](#training-and-verification)

### [!DNL Data Science Workspace]中的筆記型電腦

在Adobe Experience PlatformUI中，從&#x200B;**[!UICONTROL Data Science]**&#x200B;標籤中選擇&#x200B;**[!UICONTROL Notebooks]**，將您帶到[!UICONTROL Notebooks]概述頁面。 在此頁中，選擇[!DNL JupyterLab]頁籤以啟動[!DNL JupyterLab]環境。 [!DNL JupyterLab]的預設著陸頁面為&#x200B;**[!UICONTROL Launcher]**。

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

本教學課程使用[!DNL JupyterLab Notebooks]中的[!DNL Python] 3來顯示如何存取和探索資料。 在「啟動器」頁面中，提供了示例筆記本。 **[!UICONTROL Retail Sales]**&#x200B;示例筆記型電腦用於以下示例。

### 設定 {#setup}

當零售銷售筆記型電腦開啟時，您首先應該載入工作流程所需的程式庫。 下列清單提供後續步驟範例中使用之每個程式庫的簡短說明。

- **不爽**:新增支援大型、多維陣列和矩陣的科學運算庫
- **熊貓**:提供資料結構和操作的資料庫，用於資料操縱和分析
- **matplotlib.pyplot**:繪圖時提供類似MATLAB的體驗的繪圖程式庫
- **西博恩** :基於matplotlib的高層介面資料可視化庫
- **sklearn**:具備分類、回歸、支援向量和叢集演算法的機器學習庫
- **警告**:控制警告訊息的程式庫

### 探索資料{#exploring-data}

#### 載入資料

載入程式庫後，您就可以開始檢視資料。 以下[!DNL Python]代碼使用熊貓&#39; `DataFrame`資料結構和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函式將[!DNL Github]上托管的CSV讀入熊貓資料框：

![](./images/walkthrough/read_csv.png)

熊貓的DataFrame資料結構是一種二維標籤資料結構。 若要快速查看資料的維度，您可使用`df.shape`。 這會傳回表示DataFrame維度的元組：

![](./images/walkthrough/df_shape.png)

最後，您可以預覽資料的外觀。 您可以使用`df.head(n)`來檢視DataFrame的前`n`列：

![](./images/walkthrough/df_head.png)

#### 統計摘要

我們可以利用[!DNL Python's]熊貓庫來獲取每個屬性的資料類型。 下列呼叫的輸出將提供每個欄的項目數和資料類型的相關資訊：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

由於瞭解每欄的資料類型可讓我們瞭解如何處理資料，因此這項資訊十分實用。

現在讓我們來看一下統計摘要。 只會顯示數值資料類型，因此`date`、`storeType`和`isHoliday`將不會輸出：

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

透過此項功能，您可以看到每個特徵有6435個執行個體。 此外，還給出了平均、標準差(std)、最小、最大和四分位數等統計資訊。 這會提供資料的偏差資訊。 在下一節中，您將檢視視覺化，並搭配這項資訊運作，讓我們完全瞭解您的資料。

查看`store`的最小值和最大值，您可以看到有45個唯一儲存資料。 還有`storeTypes`可區分商店的不同。 您可以執行下列動作，以檢視`storeTypes`的分佈：

![](./images/walkthrough/df_groupby.png)

這表示22個商店的`storeType A`、17個商店的`storeType B`和6個商店的`storeType C`。

#### 視覺化資料

既然您已知道資料影格值，您就想要以視覺化來補充，讓項目更清楚、更輕鬆地識別模式。 在將結果傳達給觀眾時，這些圖表也很實用。

#### 一元圖

單變數圖是個別變數的圖形。 用於視覺化資料的通用單變數圖形是方框圖和須條圖。

使用之前的零售資料集，您就可以為45家商店及其每週銷售量產生方塊和須條圖。 該出圖是使用`seaborn.boxplot`函式生成的。

![](./images/walkthrough/box_whisker.png)

用方框和晶須圖顯示資料的分佈。 圖的外線顯示上四分位數和下四分位數，而框跨越四分位數範圍。 框中的行標示中間值。 任何高於上四分位數或下四分位數1.5倍的資料點都會標示為圓。 這些點被認為是離群的。

接下來，您可以隨時繪製每週銷售情況。 您只會顯示第一個商店的輸出。 筆記本中的程式碼會產生6張圖，對應我們資料集中45個商店中的6張。

![](./images/walkthrough/weekly_sales.png)

使用此圖表，您可以比較2年期間的每週銷售額。 隨著時間的推移，銷售高峰和低谷模式很容易被看到。

#### 多變數圖表

多變數圖表可用來查看變數之間的互動。 透過視覺化，資料科學家可以查看變數之間是否有任何關聯或模式。 常用的多變數圖形是關聯矩陣。 利用相關矩陣，利用相關係數量化多變數間的相關性。

使用相同的零售資料集，您可以產生關聯矩陣。

![](./images/walkthrough/correlation_1.png)

請注意中心下方的對角線。 這顯示在比較變數本身時，其具有完全正相關性。 強正相關度將接近1，弱關聯度接近0。 負相關顯示，負系數顯示逆趨勢。

### 功能工程{#feature-engineering}

在本節中，功能工程可用來透過執行下列作業來修改您的零售資料集：

- 新增周和年欄
- 將storeType轉換為指標變數
- 將isHoliday轉換為數值變數
- 預測每週下週的銷售情況

#### 新增周和年欄

日期的目前格式(`2010-02-05`)可讓您很難區分每週的資料。 因此，您應將日期轉換為包含周和年。

![](./images/walkthrough/date_to_week_year.png)

現在，周和日期如下：

![](./images/walkthrough/date_week_year.png)

#### 將storeType轉換為指標變數

接下來，您要將storeType欄轉換為代表每個`storeType`的欄。 有3種商店類型(`A`、`B`、`C`)，您要從中建立3個新欄。 在每個值中設定的值是布爾值，其中設定&#39;1&#39;取決於`storeType`的內容，而其它2列的`0`。

![](./images/walkthrough/storeType.png)

刪除當前`storeType`列。

#### 將isHoliday轉換為數值類型

下一項修改是將`isHoliday`布林值變更為數值表示。

![](./images/walkthrough/isHoliday.png)

#### 預測每週下週的銷售情況

現在，您想要將之前和未來每週銷售額新增至每個資料集。 您可以通過偏移`weeklySales`來執行此操作。 此外，還計算`weeklySales`差。 這是透過減去前一週的`weeklySales`而完成的。`weeklySales`

![](./images/walkthrough/weekly_past_future.png)

由於您正在向前偏移`weeklySales`資料45個資料集，並向後偏移45個資料集以建立新列，因此前45個資料點和前45個資料點具有NaN值。 您可以使用`df.dropna()`函式從資料集中移除這些點，此函式會移除所有具有NaN值的列。

![](./images/walkthrough/dropna.png)

在您進行修改後的資料集摘要如下：

![](./images/walkthrough/df_info_new.png)

### 訓練與驗證{#training-and-verification}

現在，是時候建立一些資料模型，並選擇哪個模型在預測未來銷售時表現最佳。 您將評估下列5種演算法：

- 線性回歸
- 決策樹
- 隨機森林
- 漸層增強功能
- K鄰居

#### 將資料集分割為訓練和測試子集

您需要一種方法來瞭解模型能夠預測值的精確度。 此評估可借由分配部分資料集以用作驗證，而其餘資料則用作訓練資料來完成。 由於`weeklySalesAhead`是`weeklySales`的實際未來值，因此您可使用此值來評估模型在預測值時的準確性。 拆分如下：

![](./images/walkthrough/split_data.png)

您現在有`X_train`和`y_train`來準備模型，並有`X_test`和`y_test`可供稍後評估。

#### 特別檢查算法

在本節中，將所有算法聲明到名為`model`的陣列中。 接著，您重複此陣列，並針對每個演算法，使用`model.fit()`輸入訓練資料，以建立模型`mdl`。 使用此模型，您可以使用`X_test`資料預測`weeklySalesAhead`。

![](./images/walkthrough/training_scoring.png)

對於計分，您會使用預測`weeklySalesAhead`與`y_test`資料中實際值之間的平均百分比差值。 由於您想要將預測與實際結果之間的差異降至最低，因此，「漸層提升回歸」模型是效能最佳的模型。

#### 視覺化預測

最後，您可使用實際的每週銷售值來視覺化您的預測模型。 藍線代表實際數字，綠色代表您使用漸層提升的預測。 下列程式碼會產生6張圖，代表您資料集中45個商店中的6張。 此處僅顯示`Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## 後續步驟

本檔案涵蓋一般資料科學家的工作流程，以解決零售銷售問題。 總結：

- 載入工作流程所需的程式庫。
- 載入程式庫後，您就可以開始使用統計摘要、視覺化和圖形來檢視資料。
- 接著，使用功能工程來修改零售資料集。
- 最後，建立資料模型，並選擇哪個模型在預測未來銷售時表現最佳。

準備好後，請先閱讀[JupyterLab使用手冊](./jupyterlab/overview.md)以快速概述Adobe Experience Platform資料科學工作區中的筆記型電腦。 此外，如果您有興趣瞭解模型和方式，請先閱讀[零售銷售模式和dataset](./models-recipes/create-retails-sales-dataset.md)教學課程。 本教學課程可讓您準備後續的Data Science Workspace教學課程，這些教學課程可在Data Science Workspace [教學課程頁面](../tutorials/data-science-workspace.md)中檢視。
