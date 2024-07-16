---
title: 使用高階函式擷取類似記錄
description: 瞭解如何根據相似度量度和相似度臨界值，從一個或多個資料集中識別及擷取類似或相關記錄。 此工作流程可強調不同資料集之間有意義的關聯或重疊。
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# 使用較高階函式擷取類似記錄

使用資料Distiller高階函式來解決各種常見的使用案例。 若要從一個或多個資料集中識別及擷取類似或相關的記錄，請使用本指南中詳述的篩選、轉換和還原函式。 若要瞭解如何使用高階函式來處理複雜的資料型別，請參閱有關如何[管理陣列和對應資料型別](../sql/higher-order-functions.md)的檔案。

使用本指南來識別來自不同資料集，且其特性或屬性具有重大相似性的產品。 此方法提供的解決方案包括：重複資料刪除、記錄連結、建議系統、資訊擷取和文字分析等。

本檔案說明實作相似度加入的程式，接著會使用Data Distiller高階函式計算資料集之間的相似度，並根據選取的屬性加以篩選。 對於程式的每個步驟，都會提供SQL程式碼片段和說明。 此工作流程會使用Jaccard相似性測量來實施相似性結合，並使用Data Distiller高階函式來實施代碼化。 這些方法接著用於根據相似性量度，從一個或多個資料集中識別及擷取類似或相關的記錄。 處理序的關鍵區段包括： [使用高階函式的tokenization](#data-transformation)、唯一元素的[交叉聯結](#cross-join-unique-elements)、[Jaccard相似度計算](#compute-the-jaccard-similarity-measure)，以及[臨界值型篩選](#similarity-threshold-filter)。

## 先決條件

在繼續閱讀本檔案之前，您應該熟悉下列概念：

- **相似性聯結**&#x200B;是根據記錄之間的相似性測量值，從一或多個資料表中識別及擷取記錄對的作業。 相似性聯結的主要需求如下：
   - **相似度量度**：相似度加入需依賴預先定義的相似度量度或量度。 這類量度包括：Jaccard相似度、餘弦相似度、編輯距離等。 量度取決於資料的性質和使用案例。 此量度可量化兩條記錄的相似或相異程度。
   - **臨界值**：相似度臨界值是用來判斷兩個記錄何時被視為相似到可以包含在聯結結果中。 相似度分數高於臨界值的記錄會被視為符合專案。
- **Jaccard相似度**指數，或Jaccard相似性測量，是用來測量樣本集相似度和多樣性的統計資料。 其定義為交集的大小除以樣本集的聯集大小。 Jaccard相似性測量的範圍從零到一。 Jaccard相似度為零表示這些集合之間沒有相似性，而Jaccard相似度為1表示這些集合完全相同。
  ![文氏圖表以說明Jaccard相似性測量。](../images/use-cases/jaccard-similarity.png)
- **資料Distiller中的高階函式**&#x200B;是動態的內嵌工具，可直接在SQL陳述式中處理及轉換資料。 這些多功能函式消除了資料操作中多個步驟的需求，尤其是當[處理複雜型別（例如陣列和地圖](../sql/higher-order-functions.md)）時。 透過提高查詢效率和簡化轉換，高階函式有助於在各種業務情景中更敏捷地分析和更好的決策。

## 快速入門

必須使用Data Distiller SKU才能對Adobe Experience Platform資料執行更高階的功能。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得更多資訊。

## 建立相似性 {#establish-similarity}

此使用案例需要稍後用來建立篩選臨界值的文字字串之間的相似性測量。 在此範例中，集合A和集合B中的產品代表兩個檔案中的文字。

Jaccard相似性量度可套用至廣泛的資料型別，包括文字資料、分類資料和二進位資料。 它也適合用於即時或批次處理，因為它對於大型資料集的計算上很有效率。

產品集A和產品集B包含此工作流程的測試資料。

- 產品集A： `{iPhone, iPad, iWatch, iPad Mini}`
- 產品集B： `{iPhone, iPad, Macbook Pro}`

若要計算產品集A和B之間的Jaccard相似度，請先尋找產品集的&#x200B;**交集** （通用元素）。 在這種情況下，`{iPhone, iPad}`。 接下來，尋找兩個產品集的&#x200B;**聯合** （所有唯一元素）。 在此範例中，`{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`。

最後，使用Jaccard相似度公式： `J(A,B) = A∪B / A∩B`來計算相似度。

J =積木距離
A =設定1
B =設定2

產品集A和B之間的Jaccard相似度為0.4。這表示兩個檔案中使用的字詞之間具有中等程度的相似性。 這兩個集之間的這種相似性定義了相似性聯結中的欄。 這些欄代表儲存在表格中且用於執行相似度計算的資訊片段，或與資料相關聯的特性。

### 使用字串相似度進行配對的Jaccard計算 {#pairwise-similarity}

若要更準確地比較字串之間的相似性，必須計算成對相似性。 「成對相似度」會將高維物件分割成較小維度的物件，以供比較和分析。 為此，文字字串將分成較小的部分或單位（代號）。 它們可以是個別字母、字母群組（如音節）或完整字詞。 系統會計算集合A中每個元素與集合B中每個元素之間每對權杖的相似度。此代碼化作業提供分析和運算比較、關係和深入分析的基礎，以便從資料中提取。

對於成對相似度計算，此範例使用字元雙格（兩個字元權杖）來比較集合A和集合B中產品文字字串之間的相似度比對。雙元格是指定序列或文字中兩個專案或元素的連續序列。 您可以將其泛化為n格。

此範例假設大小寫無關緊要，且不應計入空格。 根據這些條件，「設定A」和「設定B」具有下列雙格線：

產品集A雙格：

- iPhone(5)： 「ip」、「ph」、「ho」、「on」、「ne」
- iPad (3)： &quot;ip&quot;、&quot;pa&quot;、&quot;ad&quot;
- iWatch (5)： 「iw」、「wa」、「at」、「tc」、「ch」
- iPad Mini (7)： 「ip」、「pa」、「ad」、「dm」、「mi」、「in」、「ni」

產品集B雙格：

- iPhone(5)： 「ip」、「ph」、「ho」、「on」、「ne」
- iPad (3)： &quot;ip&quot;、&quot;pa&quot;、&quot;ad&quot;
- Macbook Pro (9)： 「Ma」、「ac」、「cb」、「bo」、「ooo」、「ok」、「kp」、「pr」、「ro」

接著，計算每組的Jaccard相似度係數：

|                   | iPhone （設定B） | iPad （設定B） | Macbook Pro （設定B） |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone （設定A） | （交集：5，聯集：5） = 5 / 5 = 1 | （交集： 1，等位： 7） =1 / 7 ≈ 0.14 | （交集：0，聯集：14） = 0 / 14 = 0 |
| iPad （設定A） | （交集：1，聯集：7） = 1 / 7 ≈ 0.14 | （交集：3，聯集：3） = 3 / 3 = 1 | （交集：0，聯集：12） = 0 / 12 = 0 |
| iWatch （設定A） | （交集：0，聯集：8） = 0 / 8 = 0 | （交集：0，聯集：8） = 0 / 8 = 0 | （交集： 0，聯集： 8） = 0 / 8 =0 |
| iPad Mini （設定A） | （交集： 1，聯集： 11） = 1 / 11 ≈ 0.09 | （交集：3，聯集：7） = 3 / 7 ≈ 0.43 | （交集：0，聯集：16） = 0 / 16 = 0 |

{style="table-layout:auto"}

## 使用SQL建立測試資料 {#create-test-data}

若要手動建立產品集的測試表格，請使用SQL CREATE TABLE敘述句。

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

下列說明提供上述SQL程式碼區塊的劃分：

- 第1行： `CREATE TEMP TABLE featurevector1 AS`：此陳述式會建立名為`featurevector1`的暫存資料表。 臨時表格通常只能在目前的作業階段中存取，並在作業階段結束時自動捨棄。
- 第1行和第2行： `SELECT * FROM (...)`：程式碼的這個部分是用於產生插入`featurevector1`資料表中的資料的子查詢。
在子查詢內，使用`UNION ALL`命令結合多個`SELECT`陳述式。 每個`SELECT`陳述式會產生`ProductName`資料行指定值的一列資料。
- 第3行： `SELECT 'iPad' AS ProductName`：這會在`ProductName`欄中產生值為`iPad`的列。
- 第5行： `SELECT 'iPhone'`：這會在`ProductName`欄中產生值為`iPhone`的列。

SQL陳述式會建立表格，如下所示：

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

若要建立第二個特徵向量，請使用下列SQL敘述句：

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## 資料轉換 {#data-transformation}

在此範例中，必須執行數個動作才能準確比較集合。 首先，系統會移除特徵向量中的所有空格，因為系統假設這些空格不會對相似性度量產生任何影響。 然後，會移除特徵向量中的任何重複專案，因為這些專案會浪費運算處理。 接著，從特徵向量中擷取兩個字元（雙格）的權杖。 在此範例中，它們被假定為重疊。

>[!NOTE]
>
>為了方便說明，已處理的欄會新增到每個步驟的特徵向量旁邊。

以下章節說明在開始代碼化程式之前的先決條件資料轉換，例如重複資料刪除、移除空白字元和小寫轉換。

### 去重複化 {#deduplication}

接下來，使用`DISTINCT`子句移除重複專案。 此範例中沒有重複專案，不過這是改善任何比較正確性的重要步驟。 必要的SQL顯示如下：

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### 移除空格 {#whitespace-removal}

在以下SQL陳述式中，會從特徵向量中移除空格。 查詢的`replace(ProductName, ' ', '') AS featurevector1_nospaces`部分從`featurevector1`資料表取得`ProductName`資料行並使用`replace()`函式。 `REPLACE`函式會以空字串(&quot;)取代所有出現的空格(&#39; &#39;)。 這會有效地從`ProductName`值中移除所有空格。 結果別名為`featurevector1_nospaces`。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

結果如下表所示：

|   | featurevector1_distinct | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

SQL陳述式及其在第二個特徵向量上的結果如下所示：

+++選取以展開

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

結果如下所示：

|   | featurevector2_distinct | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### 轉換為小寫 {#lowercase-conversion}

接著，SQL經過改良，將產品名稱轉換為小寫並移除任何空格。 下層函式(`lower(...)`)已套用至`replace()`函式的結果。 下層函式會將修改`ProductName`值中的所有字元轉換為小寫。 這可確保值為小寫，無論其原始大小寫為何。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

此陳述式的結果為：

|   | featurevector1_distinct | featurevector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

SQL陳述式及其在第二個特徵向量上的結果如下所示：

+++選取以展開

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

結果如下所示：

|   | featurevector2_distinct | featurevector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### 使用SQL擷取Token {#tokenization}

下一個步驟是代碼化，或文字分割。 代碼化是擷取文字並將其分成個別辭彙的程式。 這通常涉及將句子分割成單字。 在此範例中，字串會透過使用SQL函式（例如`regexp_extract_all`）擷取權杖而分解為雙格（和更高階n格）。 必須為有效的代碼化產生重疊的雙向圖。

SQL已進一步改善以使用`regexp_extract_all`。 `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:`此部分的查詢會進一步處理上一步驟中建立的已修改`ProductName`值。 它使用`regexp_extract_all()`函式從修改的小寫`ProductName`值中擷取一到兩個字元的所有非重疊子字串。 `.{2}`規則運算式模式符合長度為兩個字元的子字串。 然後，函式的`regexp_extract_all(..., '.{2}', 0)`部分會從輸入文字中擷取所有相符的子字串。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

結果如下表所示：

+++選取以展開

|   | featurevector1_distinct | featurevector1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;，&quot;ad&quot;，&quot;mi&quot;，&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;，&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;，&quot;at&quot;， &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;，&quot;ho&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

若要進一步改善正確性，必須使用SQL來建立重疊的權杖。 例如，上方的「iPad」字串缺少「pa」代號。 若要解決此問題，請將lookahead運運算元（使用`substring`）移動一個步驟，並產生雙元格。

與上一個步驟類似，`regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):`會從修改的產品名稱中擷取兩個字元的序列，但會使用`substring`方法從第二個字元開始建立重疊的權杖。 接著，在第3到7行(`array_union(...) AS tokens`)中，`array_union()`函式會結合兩個規則運算式擷取所取得的雙字元序列陣列。 這可確保結果包含來自非重疊和重疊序列的唯一權杖。

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

結果如下表所示：

+++選取以展開

|   | featurevector1_distinct | featurevector1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;，&quot;ad&quot;，&quot;mi&quot;，&quot;ni&quot;，&quot;pa&quot;，&quot;dm&quot;，&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;，&quot;ad&quot;，&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;，&quot;at&quot;，&quot;ch&quot;，&quot;wa&quot;，&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;，&quot;ho&quot;，&quot;ne&quot;，&quot;ph&quot;，&quot;on&quot;} |

{style="table-layout:auto"}

+++

不過，使用`substring`作為問題的解決方案有其限制。 如果您要以三字元（三個字元）為基礎從文字製作權杖，需要使用兩個`substrings`來回顧兩次，以取得所需的班次。 若要產生10克，您需要九個`substring`運算式。 這會使程式碼膨脹，變得無法維持。 不適宜使用純規則運算式。 我們需要新方法。

### 調整產品名稱的長度 {#length-adjustment}

可使用序列和長度函式改善SQl。 在下列範例中，`sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)`會產生從一到修改的產品名稱長度減三的編號序列。 例如，如果修改後的產品名稱是字元長度為8的「ipadmini」，則會產生一到五(8-3)的數字。

以下陳述式會擷取唯一的產品名稱，然後將每個名稱細分為四個字元長度的字元（代號）序列（不包括空格），並將它們顯示為兩欄。 其中一欄顯示唯一的產品名稱，而另一欄則顯示其產生的Token。

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

結果如下表所示：

+++選取以展開

|   | featurevector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;，&quot;padm&quot;，&quot;admi&quot;，&quot;dmin&quot;，&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;，&quot;watc&quot;，&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;，&quot;phon&quot;，&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### 確保設定權杖長度 {#ensure-set-token-length}

可以向陳述式新增其他條件，以確保產生的序列具有特定長度。 下列SQL陳述式會使`transform`函式更複雜，以擴充權杖產生邏輯。 陳述式使用`transform`內的`filter`函式，以確保產生的序列長度為6個字元。 它透過將NULL值指定給這些職位來處理不可能的情況。

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

結果如下表所示：

+++選取以展開

|   | featurevector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;，&quot;padmin&quot;，&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## 使用Data Distiller高階函式探索解決方案 {#higher-order-function-solutions}

高階函式是強大的建構，可讓您實作「程式設計」，例如Data Distiller中的語法。 它們可用來反複運算陣列中多個值的函式。

在Data Distiller中，高階函式非常適合建立n格和反複處理字元順序。

`reduce`函式（尤其是在`transform`產生的序列內使用時）提供衍生累積值或聚總的方法，這在各種分析和計畫處理中可能至關重要。

例如，在下面的SQl陳述式中，`reduce()`函式會使用自訂彙總器來彙總陣列中的元素。 它會模擬for回圈以&#x200B;**建立所有整數**&#x200B;從1到5的累積和。`1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`。

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

以下是對SQL敘述句的分析：

- 第1行： `transform`將函式`x -> reduce`套用至序列中產生的每個專案。
- 第2行： `sequence(1, 5)`產生從1到5的數字序列。
- 第3行： `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)`對序列中的每個元素x執行縮減操作（從1到5）。
   - `reduce`函式採用初始的累計器值0、從1到目前值`x`的順序，以及高階函式`(acc, y) -> acc + y`來加入數字。
   - 高階函式`acc + y`將目前值`y`加到累加器`acc`以累積總計。
- 第8行： `AS sum_result`會將結果欄重新命名為sum_result。

總而言之，這個高階函式接受兩個引數（`acc`和`y`），並定義要執行的作業，在此情況下，會將`y`加入累加器`acc`。 在縮減程式期間，會針對序列中的每個元素執行此高階函式。

此陳述式的輸出是單一資料行(`sum_result`)，其中包含一到五的數字累積總和。

### 高階函式的值 {#value-of-higher-order-functions}

本節會分析精簡版的Tri-gram SQL敘述句，以便更清楚瞭解Data Distiller中高階函式的值，進而更有效率地建立n個字元。

以下陳述式在`featurevector1`資料表中的`ProductName`資料行上運作。 它會使用從產生的序列中取得的位置，產生一組衍生自表格內已修改產品名稱的三字元子字串。

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

以下是對SQL敘述句的分析：

- 第2行： `transform`將更高階的函式套用至序列中的每個整數。
- 第3行： `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)`產生從`1`到修改的產品名稱長度減二的整數序列。
   - `length(lower(replace(ProductName, ' ', '')))`在將`ProductName`設為小寫並移除空格後，會計算其長度。
   - `- 2`會從長度中減去兩個，以確保序列會產生3個字元子字串的有效起始位置。 減2可確保每個起始位置後面有足夠的字元來擷取3個字元的子字串。 此處的子字串函式的運作方式類似於lookahead運運算元。
- 第4行： `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)`是高階函式，在產生的序列中每個整數`i`上運作。
   - `substring(...)`函式會從`ProductName`欄擷取3個字元的子字串。
   - 在擷取子字串之前，`lower(replace(ProductName, ' ', ''))`會將`ProductName`轉換為小寫並移除空格以確保一致性。

輸出是長度為三個字元的子字串清單，根據序列中指定的位置從修改的產品名稱中擷取。

## 篩選結果 {#filter-results}

`filter`函式具有後續的[資料轉換](#data-transformation)，允許從文字資料更精細且更精確地擷取相關資訊。 這可讓您獲得見解、改善資料品質並促進更好的決策過程。

下列SQL陳述式中的`filter`函式可用來調整及限制字串中的位置順序，後續的轉換函式會從中擷取子字串。

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

`filter`函式在修改的`ProductName`內產生一系列有效的起始位置，並擷取特定長度的子字串。 只允許允許擷取七個字元的子字串的開始位置。

條件`i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))`可確保起始位置`i`加上`6` （所需7個字元子字串的長度減一）不超過修改的`ProductName`的長度。

`CASE`陳述式用於根據子字串的長度有條件地包含或排除子字串。 只包含7個字元的子字串；其他字串則以NULL取代。 然後`transform`函式會使用這些子字串，從`featurevector1`表格的`ProductName`資料行建立子字串序列。

>[!TIP]
>
>您可以使用[引數化範本](../ui/parameterized-queries.md)功能，在查詢中重複使用和抽象邏輯。 例如，當您建置一般用途的公用程式函式（例如上方顯示的用來標籤字串的函式）時，可以使用字元數為引數的Data Distiller引數化範本。

## 計算兩個特徵向量間不重複元素的交叉聯結 {#cross-join-unique-elements}

根據資料的特定轉換來識別兩個資料集之間的差異或差異，是維持資料準確性、改善資料品質及確保資料集之間一致性的常見程式。

以下這個SQL陳述式會在套用轉換後，擷取`featurevector2`中存在，但`featurevector1`中不存在的不重複產品名稱。

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>除了`EXCEPT`之外，您也可以根據您的使用案例使用`UNION`和`INTERSECT`。 此外，您也可以使用`ALL`或`DISTINCT`子句進行實驗，以檢視納入所有值與只傳回指定資料行唯一值之間的差異。

結果如下表所示：

+++選取以展開

|   | lower(replace(ProductName， &#39;， &quot;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

接下來，執行交叉聯結以組合來自兩個特徵向量的元素，以建立元素配對以供比較。 此程式的第一步是建立代碼化向量。

標籤化向量是文字資料的結構化表示法，其中每個字詞、片語或意義單位（標籤）都會轉換為數字格式。 此轉換可讓自然語言處理演演算法瞭解和分析文字資訊。

下方的SQl會建立標籤化向量。

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>如果您使用[!DNL DbVisualizer]，請在建立或刪除資料表之後，重新整理資料庫連線，以便重新整理資料表的中繼資料快取。 資料Distiller不會推出中繼資料更新。

結果如下表所示：

+++選取以展開

|   | featurevector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

然後對`featurevector2`重複此程式：

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

結果如下表所示：

+++選取以展開

|   | featurevector2_distinct | Token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

兩個標籤化向量都完成後，您現在可以建立交叉聯結。 這可在以下SQL中看見：

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

以下是用來建立交叉聯結的SQl摘要：

- 第2行： `A.featurevector1_distinct AS SetA_ProductNames`從資料表`A`選取`featurevector1_distinct`資料行，並指派別名`SetA_ProductNames`。 SQL的這個區段會產生第一個資料集中的不同產品名稱清單。
- 第4行： `A.tokens AS SetA_tokens1`從資料表或子查詢`A`選取`tokens`資料行，並指派別名`SetA_tokens1`。 SQL的這個區段會產生與第一個資料集中的產品名稱相關聯的代碼化值清單。
- 第8行： `CROSS JOIN`作業會結合兩個資料集的所有可能資料列組合。 換言之，它將來自第一個資料表的每個產品名稱及其關聯權杖(`A`)與來自第二個資料表的每個產品名稱及其關聯權杖(`B`)配對。 這會產生兩個資料集的笛卡爾乘積，其中輸出中的每一列代表兩個資料集中的產品名稱及其關聯權杖的組合。

結果如下表所示：

+++選取以展開

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## 計算Jaccard相似性測量 {#compute-the-jaccard-similarity-measure}

接下來，使用Jaccard相似度係數進行計算，透過比較兩組產品名稱的代碼化表示來執行相似度分析。 以下SQL指令碼的輸出會提供下列內容：兩個資料集的產品名稱、其標籤化表示、通用和總唯一標籤計數，以及每對資料集的已計算Jaccard相似度係數。


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

以下是用來計算Jaccard相似度係數的SQL摘要：

- 第6行： `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count`計算`SetA_tokens1`和`SetB_tokens2`共用的權杖數量。 這項計算是透過計算兩個權杖陣列交集的大小來完成。
- 第7行： `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count`計算`SetA_tokens1`和`SetB_tokens2`之間的不重複權杖總數。 此行會計算兩個權杖陣列聯集的大小。
- 第8-10行： `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity`會計算語彙基元集之間的Jaccard相似度。 這些線將權杖交集的大小除以權杖聯集的大小，並將結果四捨五入為兩位小數。 結果會是介於0和1之間的值，其中1表示完全相似性。

結果如下表所示：

+++選取以展開

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Jaccard相似度 |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 3 | 7 | 0.43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 16 | 0.0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 1 | 11 | 0.09 |
| 4 | ipad | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 3 | 3 | 1.0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 12 | 0.0 |
| 6 | ipad | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 1 | 7 | 0.14 |
| 7 | iwatch | ipad | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 0 | 8 | 0.0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 14 | 0.0 |
| 9 | iwatch | iphone | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 0 | 10 | 0.0 |
| 10 | iphone | ipad | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 1 | 7 | 0.14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 14 | 0.0 |
| 12 | iphone | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 5 | 5 | 1.0 |

{style="table-layout:auto"}

+++

## 根據Jaccard相似度臨界值篩選結果 {#similarity-threshold-filter}

最後，根據預先定義的臨界值篩選結果，以僅選取符合相似度條件的配對。 下列SQL陳述式會篩選Jaccard相似度係數至少為0.4的產品。這會將結果縮小至顯示相當程度相似性的配對。

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

此查詢的結果會提供相似性聯結的欄，如下所示：

+++選取以展開

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++：

### 後續步驟 {#next-steps}

閱讀本檔案後，您現在可以使用此邏輯來強調不同資料集之間有意義的關係或重疊。 從特性或屬性具有重大相似性的不同資料集中識別產品的能力，有多項真實世界應用程式。 此邏輯可用於以下情況：

- 產品比對：將類似的產品分組或建議給客戶。
- 資料清除：改善資料品質。
- 購物籃分析：提供客戶行為、偏好設定和潛在交叉銷售機會的深入分析。

如果您尚未閱讀[AI/ML功能管道概觀](../data-distiller/ml-feature-pipelines/overview.md)，建議您先閱讀。 使用該概述來瞭解Data Distiller和您偏好的機器學習如何建立自訂資料模型，透過Experience Platform資料支援您的行銷使用案例。
