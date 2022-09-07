---
title: 基於機器學習的查詢服務機器人過濾
description: 本檔案概述如何使用Query Service和機器學習來判斷機器人活動，並從正版的線上網站訪客流量篩選其動作。
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: 8a7c04ebe8fe372dbf686fddc92867e938a93614
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# 中的機器人篩選 [!DNL Query Service] 使用機器學習

機器人活動可能會影響分析量度，並損害資料完整性。 Adobe Experience Platform [!DNL Query Service] 可透過機器人篩選程式來維護資料品質。

機器人篩選可讓您廣泛移除非人與網站互動所造成的資料污染，以維護資料品質。 該過程是通過SQL查詢和機器學習的結合來實現的。

可透過多種方式來識別機器人活動。 本檔案中採用的方法著重於活動尖峰，在此案例中，是指使用者在指定時段內採取的動作數。 最初，SQL查詢會任意設定一段時間內執行的動作數量的臨界值，以符合機器人活動的資格。 然後使用機器學習模型動態地細化該閾值，以改進這些比率的準確度。

本檔案提供SQL機器人篩選查詢的概述和詳細範例，以及您在環境中設定程式所需的機器學習模型。

## 快速入門

在此過程中，需要您培訓機器學習模型，本文檔假定一個或多個機器學習環境的工作知識。

此範例使用 [!DNL Jupyter Notebook] 作為開發環境。 雖然有許多選擇， [!DNL Jupyter Notebook] 建議使用，因為這是一個開放原始碼Web應用程式，具有低的計算需求。 可能是 [從官方網站下載](https://jupyter.org/).

## 使用 [!DNL Query Service] 為機器人活動定義臨界值

用於擷取資料以用於機器人偵測的兩個屬性為：

* Experience Cloud訪客ID（ECID，又稱為MCID）:這提供永續性的通用ID，可識別所有Adobe解決方案中的訪客。
* 時間戳記：這可在網站上發生活動時，以UTC格式提供時間和日期。

>[!NOTE]
>
>使用 `mcid` 在Experience Cloud空間參考中仍會找到「訪客ID」，如下列範例所示。

以下SQL陳述式提供識別機器人活動的初始範例。 此陳述式假設，如果訪客在一分鐘內執行了50次點按，則使用者為機器人。

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

運算式會篩選ECID(`mcid`)，但未解決其他間隔流量尖峰的所有訪客。

## 透過機器學習改善機器人偵測

初始SQL陳述式可經過細化，成為機器學習的特徵提取查詢。 改良的查詢應針對各種間隔產生更多功能，以訓練高準確度的機器學習模型。

範例陳述式從1分鐘擴展為60次點按，包含5分鐘和30分鐘期間，點按計數分別為300和1800。

範例陳述式會收集每個ECID的點按次數上限(`mcid`)。 初始陳述式已擴充為包含1分鐘（60秒）、5分鐘（300秒）和1小時（即1800秒）句點。

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

此運算式的結果可能類似於下表提供的表格。

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

## 使用機器學習找出新的尖峰臨界值

接著，將產生的查詢資料集匯出為CSV格式，然後匯入至 [!DNL Jupyter Notebook]. 從該環境中，可以使用當前的機器學習庫來訓練機器學習模型。 如需詳細資訊，請參閱疑難排解指南 [如何從 [!DNL Query Service] 格式](../troubleshooting-guide.md#export-csv)

最初建立的臨機尖峰臨界值不是資料導向，因此缺乏準確性。 機器學習模型可用來訓練參數作為閾值。 因此，您可以減少 `GROUP BY` 關鍵字，移除不需要的功能。

此示例使用Scikit-Learn機器學習庫，預設情況下，該庫與 [!DNL Jupyter Notebook]. 「熊貓」蟒蛇庫也在這裡進口使用。 以下命令將輸入 [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下來，您必須在資料集上訓練決策樹分類器，並觀察模型產生的邏輯。

在以下範例中，「Matplotlib」程式庫可用來視覺化決策樹分類器。

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

傳回的值 [!DNL Jupyter Notebook] 在此範例中，如下所示。

```text
Model Accuracy: 0.99935
```

![統計輸出 [!DNL Jupyter Notebook] 機器學習模型。](../images/use-cases/jupiter-notebook-output.png)

以上範例所示模型的結果準確率超過99%。

由於決策樹分類器可以使用來自 [!DNL Query Service] 在使用排程查詢的常規順序上，您可以高精確度篩選機器人活動，以確保資料完整性。 通過使用從機器學習模型導出的參數，可以用由模型建立的高精度參數更新原始查詢。

此範例模型以高準確度判斷，只要訪客在5分鐘內的互動超過130次，即為機器人。 此資訊現在可用來調整機器人篩選SQL查詢。

## 後續步驟

閱讀本檔案，您就能更清楚了解如何使用 [!DNL Query Service] 和機器學習來判斷及篩選機器人活動。

說明 [!DNL Query Service] 對貴組織的策略性業務洞察 [放棄的瀏覽使用案例](./abandoned-browse.md) 範例。
