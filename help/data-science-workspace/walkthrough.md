---
keywords: Experience Platform；逐步說明；Data Science Workspace；熱門主題
solution: Experience Platform
title: Data Science Workspace逐步說明
topic-legacy: Walkthrough
description: 本檔案提供Adobe Experience Platform Data Science Workspace的逐步說明。 具體來說，資料科學家將通過的一般工作流程來解決使用機器學習的問題。
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 逐步

本檔案提供Adobe Experience Platform [!DNL Data Science Workspace]的逐步說明。 本教學課程概述一般資料科學家工作流程，以及他們如何使用機器學習來處理和解決問題。

## 先決條件

- 已註冊的Adobe ID帳戶
   - Adobe ID帳戶必須已新增至可存取Adobe Experience Platform和[!DNL Data Science Workspace]的組織。

## 零售使用案例

在當前市場中，零售商面臨著保持競爭力的許多挑戰。 零售商的主要顧慮之一是決定產品的最佳定價，並預測銷售趨勢。 透過精確的預測模型，零售商將能夠找出需求與定價政策之間的關係，並做出最佳化的定價決策，以最大化銷售和收入。

## 資料科學家的解決方案

資料科學家的解決方案是利用零售商提供的豐富歷史資訊，預測未來趨勢並優化定價決策。 本逐步說明使用過去的銷售資料來訓練機器學習模型，並使用模型來預測未來的銷售趨勢。 借此，您可以產生深入分析，協助進行最佳定價變更。

此概覽反映資料科學家取得資料集和建立模型以預測每週銷售的步驟。 本教學課程涵蓋Adobe Experience Platform [!DNL Data Science Workspace]上「零售銷售筆記型電腦範例」的以下章節：

- [設定](#setup)
- [探索資料](#exploring-data)
- [特徵工程](#feature-engineering)
- [培訓與驗證](#training-and-verification)

### [!DNL Data Science Workspace]中的筆記本

在Adobe Experience Platform UI中，從&#x200B;**[!UICONTROL Data Science]**&#x200B;標籤內選擇&#x200B;**[!UICONTROL Netobooks]**，將您帶到[!UICONTROL Netobooks]概覽頁面。 在此頁面中，選擇[!DNL JupyterLab]標籤以啟動您的[!DNL JupyterLab]環境。 [!DNL JupyterLab]的預設登錄頁是&#x200B;**[!UICONTROL Launcher]**。

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

本教學課程使用[!DNL JupyterLab Notebooks]中的[!DNL Python] 3來顯示如何存取和探索資料。 在「啟動器」頁面中提供了示例筆記本。 下面提供的示例使用&#x200B;**[!UICONTROL 零售銷售]**&#x200B;示例筆記本。

### 設定 {#setup}

開啟零售銷售筆記型電腦後，您首先應該載入工作流程所需的程式庫。 下列清單提供後續步驟範例中使用之每個程式庫的簡短說明。

- **不貼心**:添加對大型、多維陣列和矩陣支援的科學計算庫
- **熊貓**:提供資料結構和用於資料操作和分析操作的庫
- **matplotlib.pyplot**:提供類似MATLAB的繪圖體驗的繪圖庫
- **西博恩** :基於matplotlib的高層介面資料可視化庫
- **sklearn**:具有分類、回歸、支援向量和叢集演算法的機器學習程式庫
- **警告**:控制警告訊息的程式庫

### 探索資料{#exploring-data}

#### 載入資料

載入程式庫後，您就可以開始查看資料。 以下[!DNL Python]代碼使用熊貓&#39; `DataFrame`資料結構和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函式將[!DNL Github]上托管的CSV讀入熊貓資料幀：

![](./images/walkthrough/read_csv.png)

Pancits的DataFrame資料結構是二維標籤資料結構。 若要快速查看資料的維度，可使用`df.shape`。 這會傳回代表DataFrame維度的元組：

![](./images/walkthrough/df_shape.png)

最後，您可以預覽資料的外觀。 您可以使用`df.head(n)`來檢視DataFrame的前`n`列：

![](./images/walkthrough/df_head.png)

#### 統計摘要

我們可以利用[!DNL Python's]庫獲取每個屬性的資料類型。 以下呼叫的輸出會提供每個欄的項目數和資料類型的相關資訊：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

此資訊很實用，因為知道每欄的資料類型有助於我們了解如何處理資料。

現在來看看統計摘要。 只會顯示數值資料類型，因此不會輸出`date`、`storeType`和`isHoliday`:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

透過此，您可以看到每個特性有6435個例項。 此外，還給出了平均值、標準差(std)、最小值、最大值和四分位數等統計資訊。 這可提供資料偏差的資訊。 在下一節中，您將檢視視覺效果，其可搭配此資訊使我們完全了解您的資料。

查看`store`的最小值和最大值，您可以看到資料代表有45個不重複儲存區。 還有`storeTypes`可區分商店。 您可以執行下列操作，查看`storeTypes`的分佈：

![](./images/walkthrough/df_groupby.png)

這表示22個商店為`storeType A` , 17個為`storeType B`,6個為`storeType C`。

#### 視覺化資料

現在您知道資料框架值了，想要以視覺效果來補充，讓項目更清楚、更輕鬆地識別模式。 這些圖表在將結果傳達給對象時也很實用。

#### 單變數圖

單變數圖表是個別變數的圖。 用來視覺化資料的通用單變數圖表為方框圖和晶須圖。

使用之前的零售資料集，您可以為45家商店及其每週銷售分別產生盒子和須條圖。 繪圖使用`seaborn.boxplot`函式生成。

![](./images/walkthrough/box_whisker.png)

用盒和須狀圖來顯示資料的分佈。 當框跨越四分位數範圍時，繪圖的外線顯示上下四分位數。 方塊中的線標示中位數。 任何資料點若超過上四分位數或下四分位數的1.5倍，則會標示為圓。 這些點被視為離群點。

接下來，您可以用時間來繪製每週銷售情況。 您只會顯示第一個商店的輸出。 筆記型電腦中的程式碼會產生6個圖，對應於資料集中45個存放區中的6個。

![](./images/walkthrough/weekly_sales.png)

使用此圖表，您可以比較2年期間的每週銷售。 隨著時間的推移，銷售高峰和低谷模式很容易出現。

#### 多變數圖

多變數圖表可用來查看變數之間的互動。 透過視覺化，資料科學家可以查看變數之間是否有任何關聯或模式。 常用的多變數圖表是關聯矩陣。 利用相關矩陣，用相關係數量化多個變數之間的依賴性。

使用相同的零售資料集，即可產生關聯矩陣。

![](./images/walkthrough/correlation_1.png)

注意中間的對角線。 這表示在比較變數本身時，其具有完全正相關性。 強正相關性的幅度將接近1，而弱相關性將接近0。 負相關顯示，負系數顯示逆趨勢。

### 特徵工程{#feature-engineering}

在本節中，功能工程可透過執行下列操作，以修改您的零售資料集：

- 新增周與年欄
- 將storeType轉換為指示器變數
- 將isHoliday轉換為數值變數
- 預測每週銷售

#### 新增周與年欄

日期的目前格式(`2010-02-05`)可能會讓您難以區分每週的資料。 因此，您應將日期轉換為包含周和年。

![](./images/walkthrough/date_to_week_year.png)

現在的周與日期如下：

![](./images/walkthrough/date_week_year.png)

#### 將storeType轉換為指示器變數

接下來，要將storeType列轉換為代表每個`storeType`的列。 有3種儲存類型(`A`、`B`、`C`)，您要從中建立3個新列。 在每個欄中設定的值是布林值，其中設定&#39;1&#39;取決於`storeType`的值，而其他2欄的`0`的值。

![](./images/walkthrough/storeType.png)

刪除當前`storeType`列。

#### 將isHoliday轉換為數值類型

下次修改是將`isHoliday`布林值變更為數值表示。

![](./images/walkthrough/isHoliday.png)

#### 預測每週銷售

現在，您想要將先前和未來的每週銷售額新增至每個資料集。 您可以抵消`weeklySales`來執行此操作。 此外，還計算了`weeklySales`差。 若要這麼做，請以前一週的`weeklySales`減去`weeklySales`。

![](./images/walkthrough/weekly_past_future.png)

由於您正在向前偏移`weeklySales`資料45個資料集，向後偏移45個資料集以建立新欄，因此前45個資料點和前45個資料點都有NaN值。 您可以使用`df.dropna()`函式從資料集中移除這些點，此函式會移除所有具有NaN值的列。

![](./images/walkthrough/dropna.png)

修改後的資料集摘要如下所示：

![](./images/walkthrough/df_info_new.png)

### 培訓和驗證{#training-and-verification}

現在，是時候建立一些資料模型，並選擇哪個模型是預測未來銷售情況的最佳表現。 您將評估下列5種演算法：

- 線性回歸
- 決策樹
- 隨機森林
- 漸層增強
- K個鄰居

#### 將資料集分割為訓練和測試子集

您需要一種方法來了解模型能夠預測值的準確度。 您可以借由分配部分資料集以用作驗證，其餘資料集則用作訓練資料，來完成此評估。 由於`weeklySalesAhead`是`weeklySales`的實際未來值，因此您可以使用此值來評估模型在預測值時的準確度。 拆分如下：

![](./images/walkthrough/split_data.png)

您現在有`X_train`和`y_train`來準備模型，以及`X_test`和`y_test`以供稍後評估。

#### 競價檢查算法

在本節中，將所有演算法聲明到名為`model`的陣列中。 接下來，對此陣列進行迭代，並針對每個算法，使用`model.fit()`輸入訓練資料，該資料將建立模型`mdl`。 使用此模型，可以使用`X_test`資料預測`weeklySalesAhead`。

![](./images/walkthrough/training_scoring.png)

對於分數，您會取用預計`weeklySalesAhead`與`y_test`資料中實際值的平均百分比差。 由於您想要將預測與實際結果之間的差異最小化，因此「漸層增值回歸」(Gradient Boosting Relevsers)是效能最佳的模型。

#### 視覺化預測

最後，您可使用實際的每週銷售值來視覺化您的預測模型。 藍線代表實際數字，綠色則代表您使用漸層提升的預測。 下列程式碼會產生6張圖，代表資料集中45個商店中的6張。 此處僅顯示`Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## 後續步驟

本檔案涵蓋解決零售銷售問題的一般資料科學家工作流程。 總結：

- 載入工作流程所需的程式庫。
- 載入程式庫後，您就可以開始使用統計摘要、視覺效果和圖形來查看資料。
- 接下來，會使用功能工程來修改您的零售資料集。
- 最後，建立資料模型，並選取哪個模型在預測未來銷售時表現最佳。

準備就緒後，請先閱讀[JupyterLab使用手冊](./jupyterlab/overview.md)以快速概述Adobe Experience Platform Data Science Workspace中的筆記型電腦。 此外，如果您想了解「模型與方式」，請先閱讀[零售銷售結構與資料集](./models-recipes/create-retails-sales-dataset.md)教學課程。
