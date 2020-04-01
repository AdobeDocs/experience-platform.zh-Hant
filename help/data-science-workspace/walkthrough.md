---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Data Science Workspace逐步說明
topic: Walkthrough
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# Data Science Workspace逐步說明

本檔案提供Adobe Experience Platform Data Science Workspace的逐步說明。 具體來說，我們將回顧資料科學家所經歷的一般工作流程，以解決使用機器學習的問題。

## 必要條件

- 已註冊的Adobe ID帳戶
   - Adobe ID帳戶必須已新增至可存取Adobe Experience Platform和Data Science Workspace的組織

## 資料科學家的動機

零售商在保持現有市場競爭力方面面臨許多挑戰。 零售商的主要顧慮之一是決定其產品的最佳價格，並預測銷售趨勢。 透過精確的預測模型，零售商將能夠找出需求與定價政策之間的關係，並做出最佳化定價決策，以最大化銷售與收入。

## 資料科學家的解決方案

資料科學家的解決方案是運用零售商可存取的豐富歷史資料，預測未來趨勢，並最佳化定價決策。 我們將使用過去的銷售資料來訓練我們的機器學習模型，並使用該模型來預測未來的銷售趨勢。 如此一來，零售商在變更定價時，將能獲得深入資訊以協助他們。

在此概觀中，我們將逐一介紹資料科學家在取得資料集並建立模型以預測每週銷售。 我們將在Adobe Experience Platform Data Science Workspace的「零售銷售筆記型範例」中，瀏覽下列章節：

- [設定](#setup)
- [探索資料](#exploring-data)
- [功能工程](#feature-engineering)
- [訓練與驗證](#training-and-verification)

### Data Science Workspace中的筆記型電腦

首先，我們希望建立一個JupyterLab筆記本，以開啟「零售銷售」示例筆記本。 遵循筆記型電腦中資料科學家所執行的步驟，將讓我們瞭解典型的工作流程。

在Adobe Experience Platform UI中，按一下頂端功能表中的「資料科學」標籤，即可帶您前往「資料科學工作區」。 在此頁中，按一下將開啟JupyterLab啟動程式的JupyterLab頁籤。 您應該會看到類似此的頁面。

![](./images/walkthrough/jupyterlab_launcher.png)

在我們的教學課程中，我們將使用Jupyter筆記型電腦中的Python 3來示範如何存取和探索資料。 在「啟動器」頁面中，提供了示例筆記本。 我們將使用Python 3的「零售銷售」範例。

![](./images/walkthrough/retail_sales.png)

### 設定

當零售銷售筆記型電腦開啟時，我們首先要載入工作流程所需的程式庫。 下列清單將簡短說明每個清單的用途：
- **numpy** —— 新增對大型、多維陣列和矩陣的支援的科學計算庫
- **熊貓** -提供資料結構和操作以用於資料操作和分析的圖書館
- **matplotlib.pyplot** —— 繪圖庫，在繪圖時提供類似MATLAB的體驗
- **seaborn** —— 基於matplotlib的高級介面資料可視化庫
- **sklearn** —— 具備分類、回歸、支援向量和叢集演算法的機器學習庫
- **警告** -控制警告訊息的程式庫

### 探索資料

#### 載入資料

載入程式庫後，我們就可以開始檢視資料。 以下Python代碼使用熊貓的 `DataFrame` 資料結構和 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) ，將Github上托管的CSV讀入熊貓的DataFrame:

![](./images/walkthrough/read_csv.png)

熊貓的DataFrame資料結構是一種二維標籤資料結構。 若要快速查看資料的維度，我們可以使用 `df.shape`。 這會傳回表示DataFrame維度的元組：

![](./images/walkthrough/df_shape.png)

最後，我們可以一窺我們的資料外觀。 我們可 `df.head(n)` 以用來檢視DataFrame `n` 的前幾列：

![](./images/walkthrough/df_head.png)

#### 統計摘要

我們可以利用Python的熊貓庫來獲取每個屬性的資料類型。 下列呼叫的輸出將提供每個欄的項目數和資料類型的相關資訊：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

由於瞭解每欄的資料類型可讓我們瞭解如何處理資料，因此這項資訊十分實用。

現在讓我們來看一下統計摘要。 只會顯示數值資料類型 `date`, `storeType`且 `isHoliday` 不會輸出：

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

這樣，我們可以看到每個特徵有6435個實例。 此外，還給出了平均、標準差(std)、最小、最大和四分位數等統計資訊。 這會提供資料的偏差資訊。 在下一節，我們將檢視視覺化，並搭配這些資訊一起運作，讓我們完全瞭解我們的資料。

從最小值和最大值看， `store`我們可以看到資料所代表的儲存區有45個。 此外，還有 `storeTypes` 哪些功能讓商店與眾不同。 通過執行下列操作，我們可 `storeTypes` 以看到的分佈：

![](./images/walkthrough/df_groupby.png)

這表示22家店是 `storeType A` ,17家是 `storeType B`,6家是 `storeType C`。

#### 視覺化資料

既然我們知道我們的資料框值，我們想要以視覺化來補充，讓事物更清晰，更容易辨識模式。 在將結果傳達給觀眾時，這些圖表也很實用。

#### 一元圖

單變數圖是個別變數的圖形。 用於視覺化資料的通用單變數圖形是方框圖和須條圖。

使用我們過去的零售資料集，我們可以為45家商店及其每週銷售量產生包裝盒和須條圖。 使用函式生成 `seaborn.boxplot` 圖。

![](./images/walkthrough/box_whisker.png)

用方框和晶須圖顯示資料的分佈。 圖的外線顯示上四分位數和下四分位數，而框跨越四分位數範圍。 框中的行標示中間值。 任何高於上四分位數或下四分位數1.5倍的資料點都會標示為圓。 這些點被認為是離群的。

接下來，我們可以按時間來規劃每週的銷售情況。 我們只展示第一家商店的產出。 筆記本中的程式碼會產生6張圖，對應我們資料集中45個商店中的6張。

![](./images/walkthrough/weekly_sales.png)

使用此圖表，我們可以比較2年內的每週銷售額。 隨著時間的推移，銷售高峰和低谷模式很容易被看到。

#### 多變數圖表

多變數圖表可用來查看變數之間的互動。 透過視覺化，資料科學家可以查看變數之間是否有任何關聯或模式。 常用的多變數圖形是關聯矩陣。 利用相關矩陣，利用相關係數量化多變數間的相關性。

使用相同的零售資料集，可以生成關聯矩陣。

![](./images/walkthrough/correlation_1.png)

請注意中心下方的對角線。 這顯示在比較變數本身時，其具有完全正相關性。 強正相關度將接近1，弱關聯度接近0。 負相關顯示，負系數顯示逆趨勢。

### 功能工程

在本節中，我們將修改我們的零售資料集。 我們將執行下列操作：

- 新增周與年欄
- 將storeType轉換為指示符變數
- 將isHoliday轉換為數值變數
- 預測每週下週的銷售情況

#### 新增周和年欄

日期(`2010-02-05`)的目前格式很難區分每週的資料。 因此，我們會將日期轉換為周和年。

![](./images/walkthrough/date_to_week_year.png)

現在，周和日期如下：

![](./images/walkthrough/date_week_year.png)

#### 將storeType轉換為指標變數

接下來，我們要將storeType欄轉換為代表各欄的欄 `storeType`。 我們有3種商店類型，`A`( `B`、 `C`)，從中建立3個新欄。 在每個欄中設定的值都是布林值，其中&#39;1&#39;會根據原來的值和其 `storeType` 他 `0` 2欄而設定。

![](./images/walkthrough/storeType.png)

將刪 `storeType` 除當前列。

#### 將isHoliday轉換為數值類型

接下來的修改是將布林值 `isHoliday` 變更為數值表示。

![](./images/walkthrough/isHoliday.png)


#### 預測每週下週的銷售情況

現在，我們想要將之前和未來每週銷售額新增至每個資料集。 我們這麼做是為了抵消我們的損失 `weeklySales`。 此外，我們也在計算差 `weeklySales` 異。 這是透過扣 `weeklySales` 除前一週的值 `weeklySales`。

![](./images/walkthrough/weekly_past_future.png)

由於我們正在向前偏移45個數 `weeklySales` 據集，而向後偏移45個資料集以建立新列，因此前45個和後45個資料點將具有NaN值。 我們可以使用函式從資料集中移除這些 `df.dropna()` 點，此函式會移除所有具有NaN值的列。

![](./images/walkthrough/dropna.png)

我們修改後的資料集摘要如下：

![](./images/walkthrough/df_info_new.png)

### 培訓與驗證

現在，是時候建立一些資料模型，並選擇哪個模型在預測未來銷售時表現最佳。 我們將評估以下5種算法：

- 線性回歸
- 決策樹
- 隨機森林
- 漸層增強功能
- K鄰居

#### 將資料集分割為訓練和測試子集

我們需要一種方法來知道我們的模型能夠預測值有多精確。 此評估可借由分配部分資料集以用作驗證，而其餘資料則用作訓練資料來完成。 由 `weeklySalesAhead` 於是實際的未來值， `weeklySales`因此我們可以用它來評估模型在預測值時的準確性。 拆分如下：

![](./images/walkthrough/split_data.png)

我們現在已 `X_train` 經準備好 `y_train` 了模型，並準備 `X_test` 了以 `y_test` 後進行評估。

#### 特別檢查算法

在本節中，我們將將所有演算法聲明到名為的陣列中 `model`。 接下來，我們對這個陣列進行循環，對於每個算法，輸入我們的訓練資料，用 `model.fit()` 於建立模型 `mdl`。 使用這個模型，我們將用我們的 `weeklySalesAhead` 資料來 `X_test` 預測。

![](./images/walkthrough/training_scoring.png)

對於計分，我們採用預測值與資料中實際值之 `weeklySalesAhead` 間的平均百分比差 `y_test` 異。 由於我們希望將預測與實際值的差異最小化，因此梯度推進回歸模型是效能最佳的模型。

#### 視覺化預測

最後，我們將以實際的每週銷售值來視覺化我們的預測模型。 藍線代表實際數字，綠色代表我們使用漸層提升的預測。 下列程式碼會產生6張圖，代表我們資料集中45個商店中的6張。 僅 `Store 1` 顯示於：

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## 結論

透過此概觀，我們重溫資料科學家將解決零售銷售問題的工作流程。 具體來說，我們會逐一執行下列步驟，以找到預測未來每週銷售的解決方案。

- [設定](#setup)
- [探索資料](#exploring-data)
- [功能工程](#feature-engineering)
- [訓練與驗證](#training-and-verification)