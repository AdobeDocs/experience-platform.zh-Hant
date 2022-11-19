---
title: 使用機器學習產生的預測模型來判斷傾向分數
description: 了解如何使用Query Service將您的預測模型套用至Platform資料。 本檔案示範如何使用Platform資料來預測客戶每次造訪的購買傾向。
source-git-commit: af1c8f94d1758b3a4e7ea00c46b0f9a71a01c6be
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# 使用機器學習產生的預測模型來判斷傾向分數

使用「查詢服務」，您可以在機器學習平台中運用Experience Platform資料，產生預測模型，例如傾向分數。 本指南說明如何使用Query Service將資料傳送至機器學習平台，以便在計算筆記型電腦中訓練模型。 訓練好的模型可以套用至使用SQL的資料，以預測客戶每次造訪的購買傾向。

## 快速入門

在此過程中，需要您培訓機器學習模型，本文檔假定一個或多個機器學習環境的工作知識。

此範例使用 [!DNL Jupyter Notebook] 作為開發環境。 雖然有許多選擇， [!DNL Jupyter Notebook] 建議使用，因為這是一個開放原始碼Web應用程式，具有低的計算需求。 可能是 [從官方網站下載](https://jupyter.org/).

如果您尚未這麼做，請依照 [connect [!DNL Jupyter Notebook] 搭配Adobe Experience Platform Query Service](../clients/jupyter-notebook.md) 繼續閱讀本指南之前。

此範例中使用的程式庫包括：

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## 從Platform將分析表格匯入 [!DNL Jupyter Notebook] {#import-analytics-tables}

若要產生傾向分數模型，儲存於Platform中之分析資料的投影必須匯入至 [!DNL Jupyter Notebook]. 從 [!DNL Python] 3 [!DNL Jupyter Notebook] 連線至Query Service，下列命令會從虛構的服裝商店Luma匯入客戶行為資料集。 使用Experience Data Model(XDM)格式儲存Platform資料時，必須產生符合結構的範例JSON物件。 請參閱本檔案，了解如何 [產生範例JSON物件](../../xdm/ui/sample.md).

![此 [!DNL Jupyter Notebook] 加亮幾個命令的儀表板。](../images/use-cases/jupyter-commands.png)

輸出會顯示Luma行為資料集內 [!DNL Jupyter Notebook] 控制面板。

![Luma匯入的客戶行為資料集在 [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## 準備資料以進行機器學習 {#prepare-data-for-machine-learning}

必須標識目標列以訓練機器學習模型。 由於購買傾向是此使用案例的目標，因此 `analytic_action` 欄是從Luma結果中選為目標欄。 值 `productPurchase` 是客戶購買的指標。 此 `purchase_value` 和 `purchase_num` 欄也會移除，因為它們與產品購買動作直接相關。

執行這些操作的命令如下：

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

接下來，必須將Luma資料集的資料轉換為適當的表示法。 需要兩個步驟：

1. 將表示數字的欄轉換為數值欄。 若要明確轉換 `dataframe`.
1. 也可將類別欄轉換為數值欄。

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

一種叫做 *熱編碼* 用於轉換類別資料變數以用於機器和深層學習演算法。 這進而改善模型的預測及分類準確度。 使用 `Sklearn` 程式庫，以在個別欄中表示每個類別值。

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

定義為 `X` 已建立表格，並顯示如下：

![X在內的表格化輸出 [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


現在機器學習的必要資料已可供使用，因此可在 [!DNL Python]&#39;s `sklearn` 程式庫。 [!DNL Logistics Regression] 可用來訓練傾向模型，並可讓您查看測試資料的準確度。 在這種情況下，大約為85%。

此 [!DNL Logistic Regression] 算法和訓練測試分割法，用於評估機器學習算法的效能，在以下代碼塊中導入：

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

測試資料的準確度為0.8518518518518519。

透過使用「物流回歸」，您可以視覺化購買的原因，並依遞減訂單的排名重要性來排序決定傾向的功能。 第一欄表示導致購買行為的較高因果關係。 後幾欄指出不會導致購買行為的因素。

將結果視覺化為兩個長條圖的程式碼如下：

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

結果的垂直長條圖視覺效果如下：

![前10項功能的視覺效果，定義購買或不購買的傾向。](../images/use-cases/visualized-results.png)

您可從長條圖中辨識出數個模式。 渠道的銷售點(POS)和呼叫主題作為報銷是決定購買行為的最重要因素。 而作為投訴和發票的呼叫主題是定義不購買行為的重要角色。 這些是可量化、可操作的深入分析，行銷人員可運用這些分析進行行銷活動，以解決購買這些客戶的傾向。

## 使用Query Service來應用經過培訓的模型 {#use-query-service-to-apply-trained-model}

建立訓練的模型後，必須將其套用至Experience Platform中保留的資料。 要執行此操作，必須將機器學習管道的邏輯轉換為SQL。 此轉變的兩個關鍵元件如下：

- 首先，SQL必須取代 [!DNL Logistics Regression] 模組，用以取得預測標籤的機率。 物流回歸所建立的模型生成了回歸模型 `y = wX + c`  權重 `w` 截距 `c` 是模型的輸出。 SQL特徵可用於乘權以獲得概率。

- 其次，在工程過程中 [!DNL Python] SQL中還必須包含一個熱編碼。 例如，在原始資料庫中，我們 `geo_county` 欄以儲存縣，但欄會轉換為 `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. 以下SQL陳述式執行相同的轉換，其中 `w1`, `w2`，和 `w3` 可以用中從模型學習的權重取代 [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

對於數值特徵，可以用權值直接乘以列，如下面的SQL陳述式所示。

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

在得到數值後，可以將其移植到sigmoid函式中，物流回歸算法生成最終預測。 在以下陳述中， `intercept` 是回歸中的截距數。
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### 端對端範例

在您有兩個欄(`c1` 和 `c2`)，如果 `c1` 有兩個類別， [!DNL Logistic Regression] 演算法會透過下列函式進行訓練：
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
SQL中的對等項如下：

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
此 [!DNL Python] 自動翻譯程式的程式碼如下：

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

使用SQL推斷資料庫時，輸出如下：

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

表格化結果會顯示每個客戶工作階段的購買傾向，包括 `0` 表示沒有購買傾向和 `1` 即確定的購買傾向。

![使用SQL進行資料庫推理的表化結果。](../images/use-cases/inference-results.png)

## 處理取樣資料：引導 {#working-on-sampled-data}

如果資料大小太大，以致於本地電腦無法儲存用於模型培訓的資料，則可以採取樣本，而不是Query Service的完整資料。 要了解從查詢服務中取樣需要多少資料，可以應用一種名為引導的技術。 在這方面，引導意味著對模型進行多次訓練，並檢查不同樣本間模型精度的方差。 為了調整上述的傾向模型範例，首先將整個機器學習工作流程封裝為一個函式。 代碼如下：

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

然後，此函式可在一個循環中執行多次，例如10次。 與先前的程式碼不同之處在於，現在不會從整個表格中擷取範例，而只會擷取一組列。 例如，以下范常式式碼僅需1000列。 可以儲存每個迭代的準確度。

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

然後，對引導模型的準確度進行排序。 之後，在給定樣本大小下，模型精度的第10和第90個量將變為95%信賴區間。

![顯示傾向分數的信賴區間的列印命令。](../images/use-cases/confidence-interval.png)

上圖指出，如果您只需要1000列來訓練模型，則精確度會降低約84%到88%之間。 您可以調整 `LIMIT` 子句，根據您的需求來查詢以確保模型的效能。


