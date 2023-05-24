---
title: 使用機器學習生成的預測模型確定傾向分數
description: 瞭解如何使用查詢服務將預測模型應用於平台資料。 本文檔演示如何使用平台資料來預測客戶每次訪問時的購買傾向。
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: 40c27a52fdae2c7d38c5e244a6d1d6ae3f80f496
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# 使用機器學習生成的預測模型確定傾向得分

使用查詢服務，您可以利用基於機器學習平台構建的預測模型來分析Experience Platform資料。

本指南說明如何使用查詢服務將資料發送到機器學習平台以在計算筆記本中訓練模型。 訓練好的模型可以應用到使用SQL的資料中，以預測客戶每次訪問的購買傾向。

## 快速入門

作為此過程的一部分，您需要培訓機器學習模型，本文檔假定您瞭解一個或多個機器學習環境的工作知識。

此示例使用 [!DNL Jupyter Notebook] 作為發展環境。 雖然有很多選擇， [!DNL Jupyter Notebook] 建議使用，因為它是一個計算要求低的開源Web應用程式。 可能 [從官方網站下載](https://jupyter.org/)。

如果尚未執行此操作，請執行以下步驟： [連接 [!DNL Jupyter Notebook] 與Adobe Experience Platform查詢服務](../clients/jupyter-notebook.md) 在繼續本指南之前。

此示例中使用的庫包括：

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## 將分析表從平台導入到 [!DNL Jupyter Notebook] {#import-analytics-tables}

要生成傾向得分模型，必須將儲存在平台中的分析資料的投影導入到 [!DNL Jupyter Notebook]。 從 [!DNL Python] 3 [!DNL Jupyter Notebook] 連接到查詢服務後，以下命令從虛擬服裝店Luma導入客戶行為資料集。 當平台資料使用體驗資料模型(XDM)格式儲存時，必須生成符合架構結構的示例JSON對象。 有關如何 [生成示例JSON對象](../../xdm/ui/sample.md)。

![的 [!DNL Jupyter Notebook] 加亮了多個命令的儀表板。](../images/use-cases/jupyter-commands.png)

輸出顯示Luma行為資料集中所有列的表格化視圖 [!DNL Jupyter Notebook] 控制項欄。

![Luma導入的客戶行為資料集在 [!DNL Jupyter Notebook]。](../images/use-cases/behavioural-dataset-results.png)

## 準備資料以進行機器學習 {#prepare-data-for-machine-learning}

必須標識目標列以訓練機器學習模型。 由於購買傾向是此使用案例的目標， `analytic_action` 列被選作Luma結果中的目標列。 值 `productPurchase` 是客戶購買的指標。 的 `purchase_value` 和 `purchase_num` 列與產品採購操作直接相關，因此也會刪除這些列。

執行這些操作的命令如下：

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

接下來，必須將Luma資料集中的資料轉換為適當的表示形式。 需要兩個步驟：

1. 將表示數字的列轉換為數字列。 為此，請顯式轉換 `dataframe`。
1. 將分類列也轉換為數字列。

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

一種叫做 *一個熱編碼* 用於轉換用於機器和深度學習算法的分類資料變數。 這反過來改善了模型的預測和分類精度。 使用 `Sklearn` 庫以表示單獨列中的每個類別值。

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

定義為 `X` 顯示為表格，如下所示：

![內X的表化輸出 [!DNL Jupyter Notebook]。](../images/use-cases/x-output-table.png)


現在，機器學習所需的資料已可用，因此它可以在 [!DNL Python]`s `sklearn` 的下界。 [!DNL Logistics Regression] 用於訓練傾向模型，並允許您查看test資料的準確性。 在這種情況下，約為85%。

的 [!DNL Logistic Regression] 算法和訓練 — test分割法用於評估機器學習算法的效能，在下面的代碼塊中導入：

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

test資料準確度為0.8518518518519。

通過使用「物流回歸」，您可以直觀地顯示採購原因，並按降序重要性排序確定傾向的特徵。 第一清單示導致購買行為的較高因果關係。 後一列指明不導致採購行為的因素。

將結果可視化為兩個條形圖的代碼如下所示：

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

下面顯示了結果的垂直條形圖可視化：

![前10項功能的可視化功能定義了購買傾向或不購買傾向。](../images/use-cases/visualized-results.png)

可以從條形圖中識別多個模式。 渠道的銷售點(POS)和作為報銷的呼叫主題是決定購買行為的最重要因素。 而「呼叫」主題作為投訴和發票是定義非採購行為的重要職責。 這些是可量化的、可操作的洞見，營銷人員可以利用這些洞見進行營銷活動，以解決購買這些客戶的傾向。

## 使用查詢服務應用已訓練的模型 {#use-query-service-to-apply-trained-model}

在建立經過訓練的模型後，必須將其應用於保存在Experience Platform中的資料。 為此，必須將機器學習流水線的邏輯轉換為SQL。 此轉換的兩個關鍵元件如下：

- 首先，SQL必須代替 [!DNL Logistics Regression] 模組獲取預測標籤的概率。 物流回歸模型生成回歸模型 `y = wX + c`  權重 `w` 攔截 `c` 是模型的輸出。 SQL功能可用於乘權以獲得概率。

- 其次，在CC500000000000000000000000000000000000000000000000000000000000000000000000000000000000 [!DNL Python] 還必須將一個熱編碼併入SQL。 例如，在原始資料庫中， `geo_county` 列以儲存縣，但列將轉換為 `geo_county=Bexar`。 `geo_county=Dallas`。 `geo_county=DeKalb`。 以下SQL陳述式執行相同的轉換，其中 `w1`。 `w2`, `w3` 可以用中從模型中學習的權重替換 [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

對於數字特徵，可以直接用權值乘列，如下面的SQL陳述式中所示。

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

在得到數值後，可以將其移植到Sigmoid函式中，Logistics Regression算法生成最終的預測。 在以下陳述中， `intercept` 是回歸中截距的數。
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### 端到端示例

在您有兩列(`c1` 和 `c2`)，如果 `c1` 有兩類， [!DNL Logistic Regression] 算法採用以下函式進行訓練：
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
SQL中的等效項如下：

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
 
的 [!DNL Python] 自動翻譯流程的代碼如下：

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

當使用SQL推斷資料庫時，輸出如下：

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

表格化結果顯示每次客戶會話購買的傾向 `0` 意味著沒有購買和 `1` 意味著確定的購買傾向。

![使用SQL進行資料庫推理的表格化結果。](../images/use-cases/inference-results.png)

## 處理採樣資料：引導 {#working-on-sampled-data}

如果資料大小太大，本地電腦無法儲存用於模型培訓的資料，則可以採集樣本，而不是從Query Service獲取完整資料。 要瞭解從Query Service中採樣需要多少資料，可以應用一種稱為引導的技術。 在這方面，自舉意味著利用不同樣本對模型進行多次訓練，並檢驗模型精度在不同樣本之間的方差。 為了調整上述的傾向性模型示例，首先將整個機器學習工作流封裝成一個函式。 代碼如下：

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

此函式隨後可以在循環中運行多次，例如10次。 與上一代碼的不同之處在於，現在不是從整個表中抽取樣本，而是只抽取行樣本。 例如，下面的示例代碼僅佔用1000行。 可以儲存每個迭代的精度。

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

然後對引導模型的準確度進行排序。 之後，模型的第10和第90個量的精度在給定樣本大小的情況下變為模型的95%置信區間。

![顯示傾向得分置信區間的打印命令。](../images/use-cases/confidence-interval.png)

上圖說明，如果您只需要1000行來培訓模型，則預計精度將降低約84%到88%。 您可以調整 `LIMIT` 查詢服務查詢中的子句，以確保模型的效能。
