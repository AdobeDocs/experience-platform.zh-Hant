---
title: 查詢服務中的模糊比對
description: 瞭解如何在您的Platform資料上執行比對，並透過大致比對您選擇的字串來合併來自多個資料集的結果。
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# 查詢服務中的模糊比對

在您的Adobe Experience Platform資料上使用「模糊」相符專案，傳回最有可能的近似相符專案，而不需要搜尋具有相同字元的字串。 這樣可讓您更靈活地搜尋資料，並節省時間和精力，讓您的資料更易於存取。

模糊比對不會嘗試重新格式化搜尋字串以便進行比對，而是會分析兩個序列之間的相似度比率，並傳回相似度百分比。 建議將[[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/)用於此程式，因為其函式比[!DNL regex]或[!DNL difflib]更適合在更複雜的情況下協助比對字串。

此使用案例中提供的範例著重於比對來自兩個不同旅行社資料集的飯店房間搜尋的類似屬性。 本檔案會示範如何透過字串與大型個別資料來源的相似度來比對字串。 在此範例中，模糊比對會比較來自Luma和Acme旅行社之房間功能的搜尋結果。

## 快速入門 {#getting-started}

在此過程中，您需要訓練機器學習模型，本檔案假設您具備一或多個機器學習環境的工作知識。

此範例使用[!DNL Python]和[!DNL Jupyter Notebook]開發環境。 雖然有許多可用選項，但建議使用[!DNL Jupyter Notebook]，因為它是運算需求低的開放原始碼Web應用程式。 可從[官方Jupyter網站](https://jupyter.org/)下載。

開始之前，您必須匯入必要的程式庫。 [!DNL FuzzyWuzzy]是在[!DNL difflib]資料庫上建置的開放來源[!DNL Python]資料庫，用來比對字串。 它使用[!DNL Levenshtein Distance]來計算序列和模式之間的差異。 [!DNL FuzzyWuzzy]有下列需求：

- [!DNL Python] 2.4 （或更高版本）
- [!DNL Python-Levenshtein]

從命令列，使用以下命令來安裝[!DNL FuzzyWuzzy]：

```console
pip install fuzzywuzzy
```

或使用下列命令安裝[!DNL Python-Levenshtein]：

```console
pip install fuzzywuzzy[speedup]
```

有關[!DNL Fuzzywuzzy]的更多技術資訊可在其[正式檔案](https://pypi.org/project/fuzzywuzzy/)中找到。

### 連線到查詢服務

您必須提供連線認證，將機器學習模型連線至查詢服務。 可提供過期和不過期的認證。 如需如何取得必要認證的詳細資訊，請參閱[認證指南](../ui/credentials.md)。 如果您使用[!DNL Jupyter Notebook]，請閱讀[如何連線至查詢服務](../clients/jupyter-notebook.md)的完整指南。

此外，請務必將[!DNL numpy]套件匯入您的[!DNL Python]環境以啟用線性代數。

```python
import numpy as np
```

必須執行下列命令，才能從[!DNL Jupyter Notebook]連線到查詢服務：

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

您的[!DNL Jupyter Notebook]執行個體現在已連線至查詢服務。 如果連線成功，則不會顯示任何訊息。 如果連線失敗，將會顯示錯誤。

### Luma資料集的Draw資料 {#luma-dataset}

使用下列命令，從第一個資料集擷取要分析的資料。 為簡短起見，這些範例已限製為欄的前10個結果。

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

選取&#x200B;**輸出**&#x200B;以顯示傳回的陣列。

+++輸出

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Acme資料集的Draw資料 {#acme-dataset}

現在，使用下列命令從第二個資料集擷取分析資料。 同樣地，為了簡單起見，這些範例已限製為欄的前10個結果。

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

選取&#x200B;**輸出**&#x200B;以顯示傳回的陣列。

+++輸出

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### 建立模糊評分函式 {#fuzzy-scoring}

接下來，您必須從FuzzyWuzzy資料庫匯入`fuzz`，並執行字串的部分比率比較。 partial ratio函式可讓您執行子字串比對。 這會採用最短的字串，並將其與具有相同長度的所有子字串比對。 此函式會傳回高達100%的百分比相似度比率。 例如，部分比率函式會比較下列字串「Deluxe Room」、「1 King Bed」和「Deluxe King Room」，並傳回69%的相似度分數。

在飯店房間符合使用案例中，會使用下列命令來完成：

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

接著，從[!DNL SciPy]資料庫匯入`cdist`，以計算兩個輸入集合中每一組之間的距離。 這會計算每個旅行社所提供之所有酒店客房的分數。

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### 使用模糊聯結分數在兩個欄之間建立對應

現在，欄已根據距離計分，您可以索引配對，並僅保留分數高於特定百分比的相符專案。 此範例只會保留分數為70%或更高的配對。

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

可以使用以下命令顯示結果。 為簡單起見，結果限製為10列。

```python
matched_pairs[:10]
```

選取&#x200B;**輸出**&#x200B;以檢視結果。

+++輸出

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

然後使用SQL搭配下列命令來比對結果：

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## 在查詢服務中套用對應以進行模糊聯結 {#mappings-for-query-service}

接著，高分相符配對配對會使用SQL聯結以建立新資料集。

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

選取&#x200B;**輸出**&#x200B;以檢視此聯結的結果。

+++輸出

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### 將模糊比對結果儲存至Platform {#save-to-platform}

最後，模糊比對的結果可以儲存為資料集，以供使用SQL的Adobe Experience Platform使用。

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```
