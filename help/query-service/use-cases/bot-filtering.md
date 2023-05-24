---
title: 基於機器學習的查詢服務中的Bot過濾
description: 本文檔概述了如何使用查詢服務和機器學習來確定bot活動並從真正的線上網站訪問流量中過濾其操作。
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# Bot篩選 [!DNL Query Service] 利用機器學習

Bot活動可能影響分析指標並損害資料完整性。 Adobe Experience Platform [!DNL Query Service] 可以通過bot篩選過程來保持資料質量。

Bot篩選允許您通過廣泛刪除與網站的非人交互導致的資料污染來維護資料質量。 這個過程是通過SQL查詢和機器學習相結合來實現的。

可以通過多種方式識別Bot活動。 本文檔中採用的方法側重於活動尖峰，在本例中是用戶在給定時間段內執行的操作數。 最初， SQL查詢任意設定一個閾值，以確定在一段時間內執行的操作數以作為bot活動。 然後使用機器學習模型動態地細化該閾值以提高這些比率的精確度。

本文檔提供了SQL bot篩選查詢和在環境中設定流程所需的機器學習模型的概述和詳細示例。

## 快速入門

作為此過程的一部分，您需要培訓機器學習模型，本文檔假定您瞭解一個或多個機器學習環境的工作知識。

此示例使用 [!DNL Jupyter Notebook] 作為發展環境。 雖然有很多選擇， [!DNL Jupyter Notebook] 建議使用，因為它是一個計算要求低的開源Web應用程式。 可能 [從官方網站下載](https://jupyter.org/)。

## 使用 [!DNL Query Service] 定義bot活動的閾值

用於提取機器人檢測資料的兩個屬性是：

* Experience Cloud訪問者ID（ECID，又稱MCID）:這提供了通用、持久的ID，可標識所有Adobe解決方案中的訪問者。
* 時間戳：這提供了網站上發生活動時以UTC格式顯示的時間和日期。

>[!NOTE]
>
>使用 `mcid` 在對Experience Cloud訪問者ID的命名空間引用中仍然找到，如下例所示。

以下SQL陳述式提供了標識bot活動的初始示例。 該語句假定，如果訪問者在一分鐘內進行50次按一下，則用戶是bot。

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

表達式將篩選ECID(`mcid`)，但未解決其他時間間隔中通信量的峰值。

## 利用機器學習改進機器人檢測

初始SQL陳述式可以細化為機器學習的特徵提取查詢。 改進的查詢應該為訓練具有較高準確度的機器學習模型的各種間隔產生更多的特徵。

示例語句從一分鐘擴展，點擊次數最多達60次，包括5分鐘和30分鐘，點擊次數分別為300和1800。

示例語句為每個ECID收集最大按一下次數(`mcid`)。 初始語句已擴展為包括1分（60秒）、5分（300秒）和1小時（即1800秒）時段。

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

此表達式的結果可能與下面提供的表類似。

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

## 使用機器學習確定新的尖峰閾值

接下來，將生成的查詢資料集導出為CSV格式，然後將其導入 [!DNL Jupyter Notebook]。 在此環境中，可以使用當前的機器學習庫來訓練機器學習模型。 有關更多詳細資訊，請參閱故障排除指南 [如何從 [!DNL Query Service] 的子菜單。](../troubleshooting-guide.md#export-csv)

最初建立的臨時尖峰閾值不是由資料驅動的，因此缺乏準確性。 機器學習模型可以用來訓練參數作為閾值。 因此，可以通過減少 `GROUP BY` 關鍵字。

此示例使用預設安裝的Scikit-Learn機器學習庫 [!DNL Jupyter Notebook]。 &quot;熊貓&quot;蟒蛇庫也在這裡引進使用。 將以下命令輸入到 [!DNL Jupyter Notebook]。

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下來，必須在資料集上訓練決策樹分類器並觀察由模型生成的邏輯。

「Matplotlib」庫用於在以下示例中直觀顯示決策樹分類器。

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

返回的值 [!DNL Jupyter Notebook] 如下所示。

```text
Model Accuracy: 0.99935
```

![來自 [!DNL Jupyter Notebook] 機器學習模型。](../images/use-cases/jupiter-notebook-output.png)

上例所示模型的結果準確率超過99%。

由於決策樹分類器可以使用來自 [!DNL Query Service] 在使用計畫查詢的常規序列中，可以通過以高準確度過濾bot活動來確保資料完整性。 通過使用從機器學習模型導出的參數，可以用模型建立的高精度參數更新原始查詢。

該示例模型以高精確度確定，在5分鐘內交互超過130次的任何訪問者都是bot。 現在，此資訊可用於優化您的bot篩選SQL查詢。

## 後續步驟

通過閱讀此文檔，您可以更好地理解如何使用 [!DNL Query Service] 和機器學習來確定和過濾機器人活動。

其他顯示 [!DNL Query Service] 對您組織的戰略性業務洞見是 [已放棄的瀏覽使用案例](./abandoned-browse.md) 示例。
