---
title: 十等分衍生資料集使用案例
description: 本指南會示範使用查詢服務來建立十等分衍生資料集以搭配您的設定檔資料使用所需的步驟。
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# 十等分衍生資料集使用案例

衍生的資料集有助於分析來自資料湖的資料的複雜使用案例，這些資料可用於其他下游Experience Platform服務或發佈到您的即時客戶設定檔資料中。

此範例使用案例示範如何建立十等分衍生的資料集以搭配您的即時客戶設定檔資料使用。 本指南以航空公司忠誠度情境為例，告知您如何建立使用分類十分位數的資料集，以根據排名屬性來細分和建立對象。

下列重要概念已說明如下：

* 用於十等分分分割槽的結構描述建立。
* 類別十等分的建立。
* 建立複雜的衍生資料集。
* 計算回顧期間的十分位數。
* 示範彙總、排名和新增唯一身分的範例查詢，以允許根據這些十等分值區產生對象。

## 快速入門

本指南需要您實際瞭解查詢服務[&#128279;](../best-practices/writing-queries.md)中的查詢執行以及Adobe Experience Platform的下列元件：

* [即時客戶個人檔案總覽](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。
* [結構描述構成基本概念](../../xdm/schema/composition.md)：介紹體驗資料模型(XDM)結構描述，以及構成結構描述的建置區塊、原則和最佳實務。
* [如何啟用Real-Time Customer Profile的結構描述](../../profile/tutorials/add-profile-data.md)：本教學課程概述將資料新增到Real-Time Customer Profile所需的步驟。
* [如何定義自訂資料型別](../../xdm/api/data-types.md)：資料型別在類別或結構描述欄位群組中用作參考型別欄位，並允許一致使用結構描述中任何位置都可包含的多欄位結構。

## 目標

本檔案提供的範例使用十等位來建置衍生的資料集，用於排名來自航空公司忠誠度方案的資料。 衍生資料集可讓您根據所選類別的前「n」%識別對象，以最大化資料的效用。

## 建立十等位衍生資料集

若要根據特定維度和對應的量度定義十分位數排名，必須將結構描述設計成允許十分位數分組。

本指南使用航空公司忠誠度資料集來示範如何使用查詢服務，根據各種回顧期間的飛行英里數建立十分位數。

## 使用查詢服務建立十等分

使用查詢服務，您可以建立包含分類十分位數的資料集，然後可以將其分段，以根據屬性排名建立對象。 只要已定義類別且有可用的量度，下列範例中顯示的概念即可套用以建立其他十等分儲存貯體資料集。

航空忠誠度資料範例使用[XDM ExperienceEvents類別](../../xdm/classes/experienceevent.md)。 每個活動都是業務交易的記錄，包括里程貸記或借記，以及「傳單」、「常用」、「銀級」或「金級」會員忠誠度狀態。 主要身分欄位是`membershipNumber`。

### 範例資料集

此範例的初始航空公司忠誠度資料集是「航空公司忠誠度資料」，其結構描述如下。 請注意，結構描述的主要身分識別是`_profilefoundationreportingstg.membershipNumber`。

![航空公司忠誠度資料結構描述圖表。](../images/use-cases/airline-loyalty-data.png)

**範例資料**

下表顯示用於此範例的`_profilefoundationreportingstg`物件中所包含的範例資料。 它提供使用十等分儲存貯體建立複雜衍生資料集的相關情境。

>[!NOTE]
>
>為了簡單起見，租使用者ID `_profilefoundationreportingstg`已在欄標題的名稱空間開頭中省略，並在整個檔案中後續提及。

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | 新成員 | 5000 | 傳單 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | 銀級 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | 銀級 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | 銀級 |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | 新信用卡 | 10000 | 傳單 |

{style="table-layout:auto"}

## 產生十等分資料集

在上述的航空公司忠誠度資料中，`.mileage`值包含一名成員每乘坐一次個別航班的飛行裡數。 此資料可用來建立終生回顧及各種回顧期間飛行英里數的十分位數。 為此目的，會建立資料集，其中包含每個回顧期間的對應資料型別十進位，以及在`membershipNumber`下指派的每個回顧期間的適當十進位。

建立「航空公司忠誠度十等分結構描述」，以使用查詢服務建立十等分資料集。

![「航空公司忠誠度十分位數結構描述」的圖表。](../images/use-cases/airline-loyalty-decile-schema.png)

### 為即時客戶個人檔案啟用結構

擷取到Experience Platform以供即時客戶設定檔使用的資料必須符合為設定檔[&#128279;](../../xdm/ui/resources/schemas.md)啟用的體驗資料模型(XDM)結構描述。 若要為設定檔啟用結構描述，它必須實作XDM個別設定檔或XDM ExperienceEvent類別。

[使用結構描述登入API](../../xdm/tutorials/create-schema-api.md)或[結構描述編輯器使用者介面](../../xdm/tutorials/create-schema-ui.md)，啟用您的結構描述以用於Real-time Customer Profile。  有關如何為設定檔啟用結構的詳細指示，請參閱其各自的檔案。

接著，建立要重複用於所有十等分相關欄位群組的資料型別。 建立十等分欄位群組是每個沙箱的一次性步驟。 也可以重複用於所有十等分相關的結構描述。

### 建立身分名稱空間並將其標示為主要識別碼 {#identity-namespace}

任何為搭配十等分使用而建立的結構描述都必須指派主要身分。 您可以在Adobe Experience Platform結構描述UI[&#128279;](../../xdm/ui/fields/identity.md#define-an-identity-field)中或透過[結構描述登入API](../../xdm/api/descriptors.md#create)定義身分欄位。

查詢服務也可讓您直接透過SQL為臨時結構描述資料集欄位設定身分或主要身分。 如需詳細資訊，請參閱有關[在臨時結構描述身分中設定次要身分和主要身分的檔案](../data-governance/ad-hoc-schema-identities.md)。

### 建立查詢以計算回顧期間的十分位數 {#create-a-query}

下列範例示範用於計算回顧期間內十分位數的SQL查詢。

可在UI中使用查詢編輯器，或透過[查詢服務API](../api/query-templates.md#create-a-query-template)建立範本。

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### 查詢檢閱

在下面會更詳細地檢查範例查詢的區段。

#### 回顧期間

十分位數資料型別包含1、3、6、9、12和期限回顧的貯體。 查詢使用回顧期間1、3和6個月，因此每個區段將包含一些「重複」查詢，以便為每個回顧期間建立臨時表格。

>[!NOTE]
>
>如果來源資料沒有可用來決定回顧期間的資料行，則所有十等分類別排名都會在`decileMonthAll`下執行。

#### 彙總

使用通用表格運算式(CTE)，在建立10等分值區之前，將里程彙總在一起。 這會提供特定回顧期間的總里數。 CTE暫時存在，並且只能在較大的查詢範圍內使用。

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

此區塊在範本（`summed_miles_3`和`summed_miles_6`）中重複兩次，而且日期計算有所變更，以便產生其他回顧期間的資料。

請務必注意查詢的身分、維度和量度資料行（分別為`membershipNumber`、`loyaltyStatus`和`totalMiles`）。

#### 排名

十分位數可讓您執行分類分組。 若要建立排名編號，在依`loyaltyStatus`欄位分組的WINDOW中，`NTILE`函式與`10`的引數搭配使用。 如此即會產生從1到10的排名。 將`WINDOW`的`ORDER BY`子句設定為`DESC`，以確保將`1`的排名值指定給維度內的&#x200B;**greatest**&#x200B;量度。

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### 對應彙總

如果有多個回顧期間，您需要使用`MAP_FROM_ARRAYS`和`COLLECT_LIST`函式預先建立十等分貯體對應。 在範常式式碼片段中，`MAP_FROM_ARRAYS`會建立具有索引鍵(`loyaltyStatus`)和值(`decileBucket`)陣列的對應。 `COLLECT_LIST`傳回具有指定資料行中所有值的陣列。

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>如果只有存留期才需要十分位數排名，則不需要對映彙總。

#### 唯一的身分識別

需要唯一身分清單(`membershipNumber`)，才能建立所有成員資格的唯一清單。

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>如果只有存留期才需要十分位數排名，則可以省略此步驟，並可在最後一個步驟中完成`membershipNumber`的彙總。

#### 將所有暫時資料彙整在一起

最後一個步驟是將所有臨時資料拼接在一起，形成一個與欄位群組中十等分的結構相同的表單。

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

如果只有期限資料可用，您的查詢會顯示如下：

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

由於使用了十等分，因此在查詢結果中可確保排名數字與百分位數之間的相關性。 每個排名都相等於10%，因此根據前30%來識別對象只需要鎖定排名1、2和3。

### 執行查詢範本

執行查詢以填入十分位數的資料集。 您也可以將查詢儲存為範本，並排定其以步調執行。 當另存為範本時，也可以更新查詢以使用參照`table_exists`命令的建立和插入模式。 有關如何使用`table_exists`命令的詳細資訊，請參閱[SQL語法指南](../sql/syntax.md#table-exists)。

## 後續步驟

以上提供的範例使用案例重點說明步驟，讓即時客戶個人檔案可以使用十等分衍生的資料集。 這可讓Segmentation Service （透過使用者介面或RESTful API）能夠根據這些十等分的貯體產生對象。 如需如何建立、評估及存取區段的詳細資訊，請參閱[區段服務總覽](../../segmentation/home.md)。
