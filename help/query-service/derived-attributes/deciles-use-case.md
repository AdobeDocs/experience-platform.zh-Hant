---
title: 基於分檔的派生屬性使用案例
description: 本指南示範使用Query Service建立資料型衍生屬性以搭配您的設定檔資料使用所需的步驟。
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# 基於分檔的派生屬性使用案例

衍生屬性有助於分析資料湖的複雜使用案例，這些資料湖可與其他下游Platform服務搭配使用，或發佈至您的即時客戶設定檔資料。

此範例使用案例示範如何建立以資料為基礎的衍生屬性，以搭配您的即時客戶設定檔資料使用。 以航空公司忠誠度案例為例，本指南會通知您如何建立使用類別資料集來區隔和根據排名屬性建立對象的資料集。

說明下列重要概念：

* 為分段建立結構。
* 分類標籤建立。
* 建立複雜的派生屬性。
* 計算回顧期間的十進位檔。
* 示範匯總、排名和新增唯一身分的查詢範例，以便根據這些資料桶產生對象。

## 快速入門

本指南需要妥善了解 [查詢服務中的查詢執行](../best-practices/writing-queries.md) 及下列Adobe Experience Platform元件：

* [即時客戶個人檔案概觀](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [結構構成基本概念](../../xdm/schema/composition.md):介紹Experience Data Model(XDM)結構，以及構成結構的基礎要素、原則和最佳實務。
* [如何啟用即時客戶個人檔案的結構](../../profile/tutorials/add-profile-data.md):本教學課程概述將資料新增至即時客戶設定檔的必要步驟。
* [如何定義自訂資料類型](../../xdm/api/data-types.md):資料類型用作類或架構欄位組中的參考型別欄位，並允許一致地使用可包含在架構中的任何位置的多欄位結構。

## 目標

本檔案中提供的範例使用資料集來建立衍生屬性，以從航空公司忠誠度結構中排名資料。 衍生屬性可讓您根據所選類別的前n%來識別對象，以最大化資料的公用程式。

## 建立以資料檔案為基礎的衍生屬性

若要根據特定維度和對應量度定義分檔的排名，必須設計結構以允許分檔分段。

本指南使用航空公司忠誠度資料集，示範如何使用Query Service根據不同回顧期間的飛行里程來建立資料集。

## 使用Query Service建立檔案

您可以使用「查詢服務」來建立包含類別分檔的資料集，然後再依據屬性排名來分段，以建立對象。 只要已定義類別且量度可用，下列範例中顯示的概念即可套用至建立其他資料貯體資料集。

航空公司忠誠度資料範例使用 [XDM ExperienceEvents類別](../../xdm/classes/experienceevent.md). 每個事件都是里程的商業交易記錄，記入或借記，以及「傳單」、「常客」、「銀」或「金」的會員忠誠度狀態。 主要身分欄位為 `membershipNumber`.

### 範例資料集

此範例的初始航空公司忠誠度資料集為「航空公司忠誠度資料」，其結構如下。 請注意，架構的主要身分為 `_profilefoundationreportingstg.membershipNumber`.

![航空公司忠誠度資料結構的圖表。](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**範例資料**

下表顯示 `_profilefoundationreportingstg` 用於此示例的對象。 它提供上下文，供使用資料桶建立複雜的派生屬性。

>[!NOTE]
>
>為簡單起見，租用戶ID `_profilefoundationreportingstg` 在欄標題中的命名空間開頭以及檔案中後續的提及中，會忽略。

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | 狀態(_M) | 新成員 | 5000 | 傳單 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | 甘乃迪 — 弗拉 | 7500 | 銀色 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | 狀態(_M) | 甘乃迪 — 弗拉 | 7500 | 銀色 |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | 銀色 |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | 狀態(_M) | 新信用卡 | 10000 | 傳單 |

{style=&quot;table-layout:auto&quot;}

## 產生資料集

在上述的航空公司忠誠度資料中， `.mileage` 值包含成員每次乘坐的航班所飛行的里程數。 此資料可用來建立在期限回顧期間飛行的英里數和各種回顧期間的分檔。 為此，系統會建立資料集，其中包含每個回顧期間之對應資料類型的分檔，以及根據 `membershipNumber`.

建立「航空公司忠誠度資料集結構」，使用「查詢服務」建立資料集。

![「航空公司忠誠度決策架構」的圖表。](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### 啟用即時客戶個人檔案的結構

要擷取到Experience Platform中以供即時客戶設定檔使用的資料，必須符合 [為設定檔啟用的Experience Data Model(XDM)結構](../../xdm/ui/resources/schemas.md). 若要為「設定檔」啟用結構，必須實作XDM個別設定檔或XDM ExperienceEvent類別。

[使用Schema Registry API啟用您的架構，以便用於Real-Time Customer Profile](../../xdm/tutorials/create-schema-api.md) 或 [結構編輯器使用者介面](../../xdm/tutorials/create-schema-ui.md).  如需如何啟用設定檔結構的詳細指示，請參閱其各自的檔案。

接下來，建立一個資料類型，以便在所有與檔案相關的欄位組中重複使用。 建立資料欄位群組是每個沙箱的一次性步驟。 它也可重複用於所有與檔案相關的結構。

### 建立身分命名空間並將其標示為主要識別碼 {#identity-namespace}

為與資料檔案搭配使用而建立的任何架構都必須指派主要身分。 您可以 [在Adobe Experience Platform結構UI中定義身分欄位](../../xdm/ui/fields/identity.md#define-an-identity-field)，或透過 [結構註冊表API](../../xdm/api/descriptors.md#create).

Query Service還允許您直接通過SQL為Ad Hoc架構資料集欄位設定標識或主標識。 請參閱 [在臨機架構身分設定次要身分和主要身分](../data-governance/ad-hoc-schema-identities.md) 以取得更多資訊。

### 建立查詢以計算回顧期間的資料 {#create-a-query}

以下範例示範用於計算回顧期間十進位檔的SQL查詢。

範本可使用UI中的查詢編輯器製作，或透過 [查詢服務API](../api/query-templates.md#create-a-query-template).

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

### 查詢審核

下面將更詳細地檢查示例查詢的各節。

#### 回顧期間

十檔資料類型包含1、3、6、9、12和期限回顧的貯體。 查詢會使用1、3和6個月的回顧期間，因此每個區段都會包含一些「重複」查詢，以便為每個回顧期間建立臨時表格。

>[!NOTE]
>
>如果來源資料沒有可用來判斷回顧期間的欄，則所有十檔的類別排名都會在 `decileMonthAll`.

#### 彙總

在建立資料桶之前，請使用通用表格運算式(CTE)將里程匯總在一起。 這可提供特定回顧期間的總英里數。 CTE暫時存在，僅可在較大查詢的範圍內使用。

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

在範本中重複區塊兩次(`summed_miles_3` 和 `summed_miles_6`)，並在日期計算中有所變更，以便產生其他回顧期間的資料。

請務必記下查詢的身分、維度和量度欄(`membershipNumber`, `loyaltyStatus` 和 `totalMiles` )。

#### 排名

脫檔檔案可讓您執行類別分組。 若要建立排名數字，請 `NTILE` 函式與 `10` 在按 `loyaltyStatus` 欄位。 排名從1到10。 設定 `ORDER BY` 條款 `WINDOW` to `DESC` 以確保排名值 `1` 是提供給 **最偉大** 量度。

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### 映射聚合

若有多個回顧期間，您必須事先使用 `MAP_FROM_ARRAYS` 和 `COLLECT_LIST` 函式。 在范常式式碼片段中， `MAP_FROM_ARRAYS` 使用一對鍵建立地圖(`loyaltyStatus`)和值(`decileBucket`)陣列。 `COLLECT_LIST` 返回一個陣列，在指定列中包含所有值。

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
>如果僅要求存留期期間有資料排名，則不需要地圖匯總。

#### 不重複身分

唯一身分的清單(`membershipNumber`)，才能建立所有成員的唯一清單。

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>如果期限期間僅需要分級排名，則可依 `membershipNumber` 可以在最後的步驟中完成。

#### 匯整所有臨時資料

最後一步是將所有臨時資料拼接在一起，形式與欄位組中的檔案結構相同。

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

如果僅存留期資料可用，您的查詢將如下所示：

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

由於使用了十進位檔，因此在查詢結果中可保證排名數字和百分位數之間的關聯。 每個排名相當於10%，因此根據前30%來識別受眾只需鎖定排名1、2和3即可。

### 運行查詢模板

執行查詢以填入資料集。 您也可以將查詢儲存為範本，並排程在執行階段執行。 另存為範本時，也可更新查詢，以使用參照的建立和插入模式 `table_exists` 命令。 有關如何使用 `table_exists`命令 [SQL語法指南](../sql/syntax.md#table-exists).

## 後續步驟

上述提供的範例使用案例著重說明在「即時客戶設定檔」中提供資料屬性的步驟。 這可讓區段服務（透過使用者介面或RESTful API）根據這些資料桶產生對象。 請參閱 [區段服務概觀](../../segmentation/home.md) 以取得如何建立、評估和存取區段的資訊。
