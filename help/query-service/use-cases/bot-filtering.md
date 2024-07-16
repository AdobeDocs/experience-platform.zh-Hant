---
title: 使用機器學習的查詢服務中的機器人篩選
description: 本檔案概述如何使用查詢服務和機器學習來判斷機器人活動，並從正版線上網站訪客流量中篩選其動作。
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# 使用機器學習在[!DNL Query Service]中篩選機器人

機器人活動可能會影響分析量度，並損害資料完整性。 透過機器人篩選程式，您可以使用Adobe Experience Platform [!DNL Query Service]來維持資料品質。

機器人篩選可讓您廣泛移除與網站非人為互動所造成的資料汙染，進而維持資料品質。 此過程是透過SQL查詢和機器學習的組合來實現的。

識別機器人活動有多種方式。 本檔案採取的方法著重於活動尖峰，在此案例中是使用者在指定時段內採取的動作次數。 最初，SQL查詢會任意設定一段時間內採取的動作數臨界值，以符合機器人活動的資格。 然後使用機器學習模型動態地調整此臨界值，以改善這些比率的準確性。

本檔案提供SQL機器人篩選查詢的概覽和詳細範例，以及您在環境中設定程式所需的機器學習模型。

## 快速入門

在此過程中，您需要訓練機器學習模型，本檔案假設您具備一或多個機器學習環境的工作知識。

此範例使用[!DNL Jupyter Notebook]作為開發環境。 雖然有許多可用選項，但建議使用[!DNL Jupyter Notebook]，因為它是運算需求低的開放原始碼Web應用程式。 可從官方網站](https://jupyter.org/)下載[。

## 使用[!DNL Query Service]定義機器人活動的臨界值

用於擷取資料以進行機器人偵測的兩個屬性是：

* Experience Cloud訪客ID （ECID，也稱為MCID）：此可提供永久性的通用ID，可識別所有Adobe解決方案中的訪客。
* 時間戳記：當網站上發生活動時，這會以UTC格式提供時間和日期。

>[!NOTE]
>
>在對Experience Cloud訪客ID的名稱空間參考中仍然可以找到`mcid`的使用，如下例所示。

下列SQL陳述式提供識別機器人活動的初始範例。 陳述式假設訪客在一分鐘內執行50次點選，則使用者為機器人。

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

運算式會篩選符合臨界值但未處理其他間隔流量尖峰之所有訪客的ECID (`mcid`)。

## 透過機器學習改善機器人偵測

初始SQL陳述式可以細化，成為機器學習的特徵擷取查詢。 改良的查詢應該會在各種間隔產生更多功能，以訓練高準確度的機器學習模型。

此範例陳述式會從一分鐘展開至最多60次點按，以包含分別點按計數300和1800的5分鐘和30分鐘週期。

範例陳述式會收集各個ECID (`mcid`)在各種期間的最大點按次數。 初始陳述式已展開並包含一分鐘（60秒）、5分鐘（300秒）和一小時（即1800秒）週期。

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

此運算式的結果可能類似於以下提供的表格。

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## 使用機器學習識別新的尖峰臨界值

接著，將產生的查詢資料集匯出為CSV格式，然後匯入為[!DNL Jupyter Notebook]。 在該環境中，您可以使用目前的機器學習程式庫來訓練機器學習模型。 請參閱疑難排解指南，以取得有關[如何以CSV格式從 [!DNL Query Service] 匯出資料](../troubleshooting-guide.md#export-csv)的詳細資料

最初建立的臨機尖峰臨界值不是資料導向的，因此缺乏準確性。 機器學習模型可用來訓練引數做為臨界值。 因此，您可以移除不需要的功能，減少`GROUP BY`個關鍵字的數量，以提高查詢效率。

此範例使用Scikit-Learn機器學習程式庫，預設會與[!DNL Jupyter Notebook]一起安裝。 「熊貓」Python資料庫也會匯入以供此處使用。 下列命令已輸入至[!DNL Jupyter Notebook]。

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下來，您必須在資料集上訓練決策樹分類器，並觀察從模型產生的邏輯。

「Matplotlib」資料庫用於在以下範例中視覺化決策樹分類器。

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

此範例從[!DNL Jupyter Notebook]傳回的值如下。

```text
Model Accuracy: 0.99935
```

![來自[!DNL Jupyter Notebook]機器學習模型的統計輸出。](../images/use-cases/jupiter-notebook-output.png)

上述範例中顯示的模型結果精確度超過99%。

由於決策樹分類器可使用排程查詢以規則順序使用[!DNL Query Service]中的資料進行訓練，因此您可以透過以高準確度篩選機器人活動來確保資料完整性。 透過使用衍生自機器學習模型的引數，可以使用模型建立的高度精確的引數來更新原始查詢。

此範例模型以高度的精確度來判斷，在5分鐘內互動超過130次的任何訪客都是機器人。 此資訊現在可用於調整您的機器人篩選SQL查詢。

## 後續步驟

閱讀本檔案可讓您更瞭解如何使用[!DNL Query Service]以及機器學習來判斷及篩選機器人活動。

顯示[!DNL Query Service]對貴組織策略性業務深入分析之優點的其他檔案為[放棄的瀏覽使用案例](./abandoned-browse.md)範例。
