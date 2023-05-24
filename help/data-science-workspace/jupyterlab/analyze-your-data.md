---
keywords: Experience Platform;JupyterLab；筆記本；Data Science Workspace；熱門主題；分析資料筆記本
solution: Experience Platform
title: 使用筆記本分析資料
type: Tutorial
description: 本教程重點介紹如何使用Jupyter Notebooks（在Data Science Workspace中構建）來訪問、瀏覽和可視化您的資料。
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# 使用筆記本分析資料

本教程重點介紹如何使用Jupyter Notebooks（在Data Science Workspace中構建）來訪問、瀏覽和可視化您的資料。 在本教程結束時，您應瞭解Jupyter筆記型電腦提供的一些功能，以便更好地瞭解您的資料。

介紹了以下概念：

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是Project Jupyter的新一代基於web的介面，並緊密整合到 [!DNL Adobe Experience Platform]。
- **批：** 資料集由批處理組成。 批是一組在一段時間內收集並作為單個單位一起處理的資料。 將資料添加到資料集時會建立新批。
- **資料存取SDK（不建議使用）:** 資料存取SDK現在已棄用。 請使用 [[!DNL Platform SDK]](../authoring/platform-sdk.md) 的子菜單。

## 在Data Science Workspace中瀏覽筆記本

在本節中，將探索以前已納入零售銷售架構的資料。

Data Science Workspace允許用戶建立 [!DNL Jupyter Notebooks] 通過 [!DNL JupyterLab] 可在其中建立和編輯機器學習工作流的平台。 [!DNL JupyterLab] 是一種伺服器 — 客戶端協作工具，允許用戶通過web瀏覽器編輯筆記本文檔。 這些筆記本可包含可執行代碼和富文本元素。 為了我們的目的，我們將使用Markdown進行分析說明和執行檔 [!DNL Python] 用於執行資料勘探和分析的代碼。

### 選擇工作區

啟動時 [!DNL JupyterLab]為Jupyter筆記本提供了一個基於Web的介面。 根據我們選擇的筆記本類型，將啟動相應的內核。

在比較要使用的環境時，我們必須考慮每個服務的局限性。 例如，如果我們使用 [熊貓](https://pandas.pydata.org/) 庫 [!DNL Python]，作為普通用戶，RAM限制為2 GB。 即使是電源用戶，也將限制為20 GB的RAM。 如果處理較大的計算，使用 [!DNL Spark] 它提供1.5 TB，與所有筆記本實例共用。

預設情況下，Tensorflow配方在GPU群集中工作，Python在CPU群集中運行。

### 建立新筆記本

在 [!DNL Adobe Experience Platform] UI，選擇 [!UICONTROL 資料科學] 的子菜單。 從此頁面中，選擇 [!DNL JupyterLab] 開啟 [!DNL JupyterLab] 啟動程式。 您應該看到類似的頁面。

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

在本教程中，我們將使用 [!DNL Python] 3，顯示如何訪問和瀏覽資料。 在「啟動程式」頁中，提供了示例筆記本。 我們將使用零售銷售處方 [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

零售銷售處方是一個獨立的示例，它使用相同的零售銷售資料集來顯示如何在Jupyter筆記本中瀏覽和可視化資料。 此外，筆記本在培訓和驗證方面更深入。 有關此特定筆記本的詳細資訊，請參閱 [漫步](../walkthrough.md)。

### 訪問資料

>[!NOTE]
>
>的 `data_access_sdk_python` 已棄用，不再推薦。 請參閱 [將資料存取SDK轉換為平台SDK](../authoring/platform-sdk.md) 教程來轉換代碼。 本教程仍適用以下相同步驟。

我們將從以下位置對內部資料進行訪問 [!DNL Adobe Experience Platform] 和外部資料。 我們將使用 `data_access_sdk_python` 庫以訪問內部資料，如資料集和XDM架構。 對於外部資料，我們用熊貓 [!DNL Python] 的下界。

#### 外部資料

開啟零售銷售筆記本後，查找「載入資料」標題。 以下 [!DNL Python] 代碼使用熊貓 `DataFrame` 資料結構和 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 函式，用於讀取托管於 [!DNL Github] 到DataFrame中：

![](../images/jupyterlab/analyze-data/read_csv.png)

Panots的DataFrame資料結構是一種二維標注資料結構。 要快速查看資料的維度，我們可以使用 `df.shape`。 這將返回表示DataFrame的維度的元組：

![](../images/jupyterlab/analyze-data/df_shape.png)

最後，我們可以看一看我們的資料是什麼樣子。 我們可以 `df.head(n)` 查看 `n` DataFrame的行：

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] 資料

現在，我們將通過 [!DNL Experience Platform] 資料。

##### 按資料集ID

對於本節，我們使用的是Retail Sales資料集，該資料集與Retail Sales示例筆記本中使用的資料集相同。

在Jupyter筆記本中，您可以從 **資料** 頁籤 ![資料頁籤](../images/jupyterlab/analyze-data/dataset-tab.png) 左邊。 選擇該頁籤後，將提供兩個資料夾。 選擇 **[!UICONTROL 資料集]** 的子菜單。

![](../images/jupyterlab/analyze-data/dataset_tab.png)

現在，在資料集目錄中，您可以看到所有攝取的資料集。 請注意，如果目錄中的資料集已大量填充，則載入所有條目可能需要一分鐘。

由於資料集是相同的，因此我們希望替換使用外部資料的前一部分的載入資料。 選擇下面的代碼塊 **載入資料** 然後按 **「d」** 鍵盤上鍵兩次。 確保焦點在塊上，而不是文本中。 你可以按 **「esc」** 在按前避開文本焦點 **「d」** 兩次。

現在，我們可以按一下右鍵 `Retail-Training-<your-alias>` 資料集，然後在下拉清單中選擇「瀏覽筆記本中的資料」選項。 可執行代碼條目將出現在您的筆記本中。

>[!TIP]
>
>請參閱 [[!DNL Platform SDK]](../authoring/platform-sdk.md) 的子菜單。

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

如果您正在處理除 [!DNL Python]，請參閱 [此頁](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) 訪問 [!DNL Adobe Experience Platform]。

選擇執行檔單元格，然後按工具欄中的播放按鈕將運行執行檔代碼。 的輸出 `head()` 將是一個表，其資料集的鍵為列，資料集中的前n行為。 `head()` 接受整數參數以指定要輸出的行數。 預設情況下，此值為5。

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

如果重新啟動內核並再次運行所有單元格，則應獲得與以前相同的輸出。

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### 瀏覽資料

既然我們可以訪問您的資料，讓我們通過統計和可視化來關注資料本身。 我們使用的資料集是零售資料集，它提供了關於給定日期45個不同商店的雜項資訊。 給定的某些特徵 `date` 和 `store` 包括：
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### 統計摘要

我們可以利用 [!DNL Python's] 熊貓庫獲取每個屬性的資料類型。 以下調用的輸出將提供有關每個列的條目數和資料類型的資訊：

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

此資訊非常有用，因為瞭解每列的資料類型將使我們能夠瞭解如何處理資料。

現在讓我們看一下統計摘要。 只顯示數字資料類型，因此 `date`。 `storeType`, `isHoliday` 將不輸出：

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

由此可以看出，每個特徵有6435個實例。 同時給出了平均、標準差(std)、最小、最大和四分之間的統計資訊。 這給出了資料偏差的資訊。 在下一節中，我們將瀏覽與這些資訊一起工作的可視化技術，以便我們更好地瞭解我們的資料。

查看 `store`，我們可以看到有45個資料表示的唯一儲存。 還有 `storeTypes` 才能區分店面。 我們可以看到 `storeTypes` 執行以下操作：

![](../images/jupyterlab/analyze-data/df_groupby.png)

這意味著22家商店 `storeType` `A`, 17 `storeType` `B`，和6 `storeType` `C`。

#### 資料可視化

既然我們知道我們的資料框架值，我們想用可視化來補充這一點，使事情更清晰，更容易識別模式。 圖形在將結果傳送給觀眾時也很有用。 部分 [!DNL Python] 用於可視化的庫包括：
- [馬普洛特利布](https://matplotlib.org/)
- [熊貓](https://pandas.pydata.org/)
- [西博恩](https://seaborn.pydata.org/)
- [積](https://ggplot2.tidyverse.org/)

在本節中，我們將快速介紹使用每個庫的一些優勢。

[馬普洛特利布](https://matplotlib.org/) 是 [!DNL Python] 可視化包。 他們的目標是讓「容易、難」成為可能。 這一點往往是正確的，因為一攬子計畫功能極強，但也伴隨著複雜性。 在不花費大量時間和精力的情況下，要獲得一個合理的外觀圖並不總是容易的。

[熊貓](https://pandas.pydata.org/) 主要用於其DataFrame對象，該對象允許使用整合索引進行資料操作。 不過，熊貓還包括一個內置的繪圖功能，該功能基於matplotlib。

[西博恩](https://seaborn.pydata.org/) 是在matplotlib上生成的包。 它的主要目標是使預設圖形更具有視覺吸引力，並簡化複雜圖形的建立。

[積](https://ggplot2.tidyverse.org/) 也是在matplotlib上構建的包。 但主要區別是該工具是R的ggplot2埠。與西博恩類似，其目標是改進matplotlib。 熟悉R的ggplot2的用戶應考慮此庫。


##### 單變數圖

單變數圖是單個變數的圖。 常用的單變數圖形用於將資料可視化為框和晶須圖。

使用我們以前的零售資料集，我們可以為45家商店中的每家及其每週銷售額生成框和晶須圖。 繪圖是使用 `seaborn.boxplot` 的子菜單。

![](../images/jupyterlab/analyze-data/box_whisker.png)

用盒和晶須圖顯示資料的分佈。 出圖的外線顯示上四分位和下四分位，而框跨過四分位範圍。 框中的線條標籤中位。 高於上四分之一或下四分之一的任何資料點都標籤為圓。 這些點被認為是異常點。

##### 多元圖

多變數圖用於查看變數之間的相互作用。 通過可視化，資料科學家可以查看變數之間是否存在任何相關或模式。 常用的多元圖是相關矩陣。 利用相關矩陣，利用相關係數量化多個變數之間的相關性。

使用同一零售資料集，可以生成相關矩陣。

![](../images/jupyterlab/analyze-data/correlation_1.png)

注意中心下方1的對角線。 這表明，在將變數與自身進行比較時，它具有完全正相關性。 強正相關度將接近1，弱相關度將接近0。 顯示負相關和顯示逆趨勢的負系數。


## 後續步驟

本教程將介紹如何在資料科學工作區中建立新的Jupyter筆記本，以及如何從外部和從中訪問資料 [!DNL Adobe Experience Platform]。 具體來說，我們介紹了以下步驟：
- 建立新的Jupyter筆記本
- 訪問資料集和架構
- 瀏覽資料集

現在，您已準備好 [下一部分](../models-recipes/package-source-files-recipe.md) 打包配方並導入到Data Science Workspace。
