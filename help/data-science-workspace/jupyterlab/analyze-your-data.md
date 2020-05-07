---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: 使用筆記型電腦分析資料
topic: Tutorial
translation-type: tm+mt
source-git-commit: 37213f29e8099f8587cde9eb66f9b75de3ad8a3a
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 0%

---


# 使用筆記型電腦分析資料

本教學課程著重於如何使用Jupyter筆記型電腦（建立在資料科學工作區中）來存取、探索和視覺化您的資料。 在本教學課程結束時，您應瞭解Jupyter筆記型電腦提供的一些功能，以便更好地瞭解您的資料。

以下概念介紹：

- **JupyterLab:** [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是Project Jupyter的新一代網路介面，並與Adobe Experience Platform緊密整合。
- **批：** 資料集由批處理組成。 批是一組在一段時間內收集並作為單個單位一起處理的資料。 新增資料至資料集時，會建立新的批次。
- **資料存取SDK（已過時）:** 「資料存取SDK」現已停用。 請使用「平 [台SDK](../authoring/platform-sdk.md) 」指南。

## 在Data Science Workspace中探索筆記型電腦

在本節中，將探索先前納入零售銷售模式的資料。

Data Science Workspace可讓使用者透過JupyterLab平台建立Jupyter Notebooks，讓他們建立和編輯機器學習工作流程。 JupyterLab是伺服器用戶端協同作業工具，可讓使用者透過網頁瀏覽器編輯筆記型電腦檔案。 這些筆記型電腦可同時包含可執行代碼和富格文本元素。 為了我們的目的，我們將使用Markdown進行分析描述，並使用可執行的Python程式碼來執行資料探索和分析。

### 選擇您的工作區

在啟動JupyterLab時，我們將為Jupyter Notebooks提供基於Web的介面。 根據我們選擇的筆記本類型，將啟動相應的內核。

在比較要使用的環境時，我們必須考慮每項服務的限制。 例如，如果我們將熊貓圖書館 [與](https://pandas.pydata.org/) Python搭配使用，作為普通用戶，RAM限制為2 GB。 即使身為強大使用者，我們也只能使用20 GB的記憶體。 如果處理較大的計算，則使用Spark是合理的，它提供1.5 TB的容量，可與所有筆記本實例共用。

依預設，Tensorflow方式可在GPU叢集中運作，而Python則可在CPU叢集中執行。

### 建立新筆記本

在Adobe Experience Platform UI中，按一下頂端功能表中的「資料科學」標籤，即可帶您前往「資料科學工作區」。 在此頁中，按一下將開啟JupyterLab啟動程式的JupyterLab頁籤。 您應該會看到類似此的頁面。

![](../images/jupyterlab/analyze-data/jupyterlab_launcher.png)

在我們的教學課程中，我們將使用Jupyter筆記型電腦中的Python 3來示範如何存取和探索資料。 在「啟動器」頁中，提供了示例筆記本。 我們將使用Python 3的零售銷售配方。

![](../images/jupyterlab/analyze-data/retail_sales.png)

「零售銷售」方式是使用相同「零售銷售」資料集的獨立範例，以顯示如何在Jupyter Notebook中探索和視覺化資料。 此外，本筆記本還通過培訓和驗證深入探討。 有關此特定筆記本的詳細資訊，請參閱本 [步](../walkthrough.md)。

### 存取資料

>[!NOTE] 已過 `data_access_sdk_python` 時，不再建議使用。 請參閱將資料 [存取SDK轉換為平台SDK](../authoring/platform-sdk.md) 教學課程，以轉換您的程式碼。 本教學課程仍適用下列相同步驟。

我們將從Adobe Experience Platform內部存取資料，從外部存取資料。 我們將使用程式庫 `data_access_sdk_python` 來存取內部資料，例如資料集和XDM架構。 對於外部資料，我們將使用熊貓蟒蛇圖庫。

#### 外部資料

當零售銷售筆記型電腦開啟時，尋找「載入資料」標題。 以下Python程式碼使用 `DataFrame` 熊貓的資料結構和 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) ，將Github上代管的CSV讀入DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

熊貓的DataFrame資料結構是一種二維標籤資料結構。 若要快速查看資料的維度，我們可以使用 `df.shape`。 這會傳回表示DataFrame維度的元組：

![](../images/jupyterlab/analyze-data/df_shape.png)

最後，我們可以一窺我們的資料外觀。 我們可 `df.head(n)` 以用來檢視DataFrame `n` 的前幾列：

![](../images/jupyterlab/analyze-data/df_head.png)

#### 體驗平台資料

現在，我們將重點討論如何存取Experience Platform資料。

##### 依資料集ID

在本節中，我們使用零售銷售資料集，該資料集與零售銷售示例筆記本中使用的資料集相同。

在Jupyter Notebook中，我們可以從左側的「 **Data** 」（資料）頁籤訪問資料。 按一下該頁籤後，您將能夠看到資料集清單。

![](../images/jupyterlab/analyze-data/dataset_tab.png)

現在，在Datasets目錄中，我們將能夠看到所有收錄的資料集。 請注意，如果目錄中填入了大量資料集，則可能需要一分鐘來載入所有條目。

由於資料集相同，因此我們想要取代使用外部資料的上一區段的載入資料。 在「載入資 **料** 」下方選取程式碼區塊，並按 **鍵盤上的** 「d&#39;key」兩次。 請確定焦點在區塊上，而非在文字中。 您可以按 **&#39;esc&#39;** ，以逸出文字焦點，然後按 **&#39;d&#39;** 兩下。

現在，我們可以在資料集上按一 `Retail-Training-<your-alias>` 下滑鼠右鍵，並在下拉式清單中選取「探索筆記型電腦中的資料」選項。 可執行的代碼條目將出現在您的筆記本中。

>[!TIP] 請參閱平 [台SDK](../authoring/platform-sdk.md) 指南以轉換程式碼。

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

如果您使用的是Python以外的其他內核，請參 [閱本頁](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) ，以存取Adobe Experience Platform上的資料。

選擇可執行單元格，然後按工具欄中的播放按鈕將運行可執行代碼。 的輸出 `head()` 將是表，其中資料集的索引鍵為欄，而資料集中的前n列為欄。 `head()` 接受整數參數，以指定要輸出的行數。 預設為5。

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

如果重新啟動內核並再次運行所有單元格，則應獲得與以前相同的輸出。

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### 探索您的資料

既然我們可以存取您的資料，讓我們利用統計資料和視覺化功能來關注資料本身。 我們使用的資料集是零售資料集，它提供了關於給定日期45個不同商店的各種資訊。 特定特定的特 `date` 徵 `store` 包括：
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

我們可以利用Python的熊貓庫來獲取每個屬性的資料類型。 下列呼叫的輸出將提供每個欄的項目數和資料類型的相關資訊：

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

由於瞭解每欄的資料類型可讓我們瞭解如何處理資料，因此這項資訊十分實用。

現在讓我們來看一下統計摘要。 只會顯示數值資料類型，因此 `date`, `storeType`和 `isHoliday` 將不會輸出：

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

這樣，我們可以看到每個特徵有6435個實例。 給出了平均、標準差(std)、最小、最大和四分位數等統計資訊。 這會提供資料的偏差資訊。 在下一節，我們將檢視視覺化，並搭配這些資訊，讓我們更瞭解我們的資料。

從最小值和最大值看， `store`我們可以看到資料所代表的儲存區有45個。 此外，還有 `storeTypes` 哪些功能讓商店與眾不同。 通過執行下列操作，我們可 `storeTypes` 以看到的分佈：

![](../images/jupyterlab/analyze-data/df_groupby.png)

這表示22家店是 `storeType` 17家， `A`6家是 `storeType``B``storeType``C`。

#### 資料視覺化

既然我們知道我們的資料框值，我們想要以視覺化來補充，讓事物更清晰，更容易辨識模式。 在將結果傳達給觀眾時，圖表也很有用。 一些Python程式庫對視覺化有幫助，包括：
- [馬特普洛特利卜](https://matplotlib.org/)
- [熊貓](https://pandas.pydata.org/)
- [西伯恩](https://seaborn.pydata.org/)
- [gplot](https://ggplot2.tidyverse.org/)

在本節中，我們將快速介紹使用每個程式庫的一些優點。

[Matplotlib](https://matplotlib.org/) 是最舊的Python視覺化套件。 他們的目標是讓「輕鬆、艱難的事情成為可能」。 這通常是正確的，因為該套產品功能極強，但同時也具有複雜性。 在不花費大量時間和精力的情況下，要獲得合理的外觀圖並不總是容易的。

[Pactose](https://pandas.pydata.org/) 主要用於其DataFrame對象，它允許通過整合索引進行資料操作。 不過，熊貓也包括了一個基於matplotlib的內置繪圖功能。

[seaborn](https://seaborn.pydata.org/) 是以matplotlib為基礎的套件。 其主要目標是讓預設圖形更具視覺吸引力，並簡化複雜圖形的建立。

[ggplot](https://ggplot2.tidyverse.org/) 是也建立在matplotlib之上的套件。 但主要區別在於，該工具是R的ggplot2埠。 與西博恩類似，其目標是改進matplotlib。 熟悉gplot2 for R的使用者應考慮此程式庫。


##### 一元圖

單變數圖是個別變數的圖形。 常用的單變數圖形是方框和須條圖，用來視覺化您的資料。

使用我們過去的零售資料集，我們可以為45家商店及其每週銷售量產生包裝盒和須條圖。 使用函式生成 `seaborn.boxplot` 圖。

![](../images/jupyterlab/analyze-data/box_whisker.png)

用方框和晶須圖顯示資料的分佈。 圖的外線顯示上四分位數和下四分位數，而框則跨越四分位數範圍。 框中的行標示中間值。 任何高於上四分位數或下四分位數1.5倍的資料點都會標示為圓。 這些點被認為是離群的。

##### 多變數圖表

多變數圖表可用來查看變數之間的互動。 透過視覺化，資料科學家可以查看變數之間是否有任何關聯或模式。 常用的多變數圖形是關聯矩陣。 利用相關矩陣，利用相關係數量化多變數間的相關性。

使用相同的零售資料集，可以生成關聯矩陣。

![](../images/jupyterlab/analyze-data/correlation_1.png)

注意中心下方1的對角線。 這顯示在比較變數本身時，其具有完全正相關性。 強正相關度將接近1，弱關聯度接近0。 負相關顯示，負系數顯示逆趨勢。


## 後續步驟

本教學課程將說明如何在資料科學工作區中建立新的Jupyter筆記型電腦，以及如何從外部以及從Adobe Experience Platform存取資料。 具體來說，我們逐一檢視下列步驟：
- 建立新的Jupyter筆記型電腦
- 存取資料集和結構
- 探索資料集

現在，您已準備好進入下一 [節](../models-recipes/package-source-files-recipe.md) ，以封裝配方並匯入至Data Science Workspace。