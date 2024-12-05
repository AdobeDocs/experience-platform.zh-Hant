---
title: 使用SQL建立對象
description: 瞭解如何在Adobe Experience Platform的Data Distiller中使用SQL對象擴充功能，以使用SQL命令建立、管理和發佈對象。 本指南涵蓋對象生命週期的所有方面，包括建立、更新和刪除設定檔，以及使用資料導向對象定義來鎖定以檔案為基礎的目的地。
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 7db055f598e3fa7d5a50214a0cfa86e28e5bfe47
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 1%

---

# 使用SQL建立對象

使用SQL受眾擴充功能來建置具有來自Data Lake之資料的受眾，包括任何現有維度實體（例如客戶屬性或產品資訊）。

使用此SQL擴充功能可改善您建立受眾的能力，因為在定義受眾區段時，您不需要在設定檔中使用原始資料。 使用此方法建立的對象會自動在對象工作區中註冊，您可以進一步將對象鎖定在檔案型目的地。

![顯示SQL對象擴充功能工作流程的資訊圖。 階段包括：使用SQL命令透過查詢服務建立對象、在平台UI中管理對象，以及在檔案型目的地中啟用對象。](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

本文介紹如何在Adobe Experience Platform的Data Distiller中使用SQL對象擴充功能，以使用SQL命令建立、管理和發佈對象。

## Data Distiller中的對象建立生命週期 {#audience-creation-lifecycle}

請依照下列步驟建立、管理和啟用您的對象。 建立的受眾可無縫整合至「受眾流程」，因此您可以從基本受眾建立區段，並將檔案型目的地（例如CSV上傳或雲端儲存位置）作為客戶拓展的目標。 「受眾流程」是指建立、管理和啟用受眾的完整流程，能確保各個目的地間的無縫整合。

在「對象流程」中，使用下列SQL命令在Adobe Experience Platform中[建立](#create-audience)、[修改](#add-profiles-to-audience)和[刪除](#delete-audience)對象。

### 建立客群 {#create-audience}

使用`CREATE AUDIENCE AS SELECT`命令來定義新對象。 建立的對象會儲存在資料集中，並在Data Distiller下的[!UICONTROL 對象]工作區中註冊。

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**參數**

使用這些引數來定義您的SQL對象建立查詢：

| 參數 | 說明 |
|--------------------|------------------------------------------------------------------|
| `schema` | 選填。 為查詢建立的資料集定義XDM結構描述。 |
| `table_name` | 表格和對象的名稱。 |
| `primary_identity` | 指定對象的主要身分欄。 |
| `identity_namespace` | 身分的名稱空間。 您可以使用現有的名稱空間或建立新的名稱空間。 若要檢視可用的名稱空間，請使用`SHOW NAMESPACE`命令。 若要建立新的名稱空間，請使用`CREATE NAMESPACE`。 例如： `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`。 |
| `select_query` | 定義對象的SELECT陳述式。 您可以在[SELECT查詢](../sql/syntax.md#select-queries)區段中找到SELECT查詢的語法。 |

{style="table-layout:auto"}

>[!NOTE]
>
>若要為複雜的資料結構提供更大的彈性，您可以在定義對象時巢狀內嵌擴充屬性。 擴充屬性（例如`orders`、`total_revenue`、`recency`、`frequency`和`monetization`）可依需要用來篩選對象。

**範例：**

下列範例示範如何建構SQL對象建立查詢：

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

在此範例中，`userId`資料行被識別為身分資料行，並指派適當的名稱空間(`lumaCrmId`)。 其餘欄（`orders`、`total_revenue`、`recency`、`frequency`和`monetization`）都是擴充屬性，可為對象提供額外內容。

**限制：**

使用SQL建立對象時，請注意下列限制：

- 主要身分資料行&#x200B;**必須**&#x200B;位於資料集的最高層級，且不得巢狀內嵌於其他屬性或類別中。
- 使用SQL命令建立的外部對象保留期為30天。 30天後，這些對象會自動刪除，這是規劃對象管理策略的重要考量。

### 將設定檔新增至現有對象 {#add-profiles-to-audience}

使用`INSERT INTO`命令將設定檔（或整個對象）新增到現有對象。

```sql
INSERT INTO table_name
SELECT select_query
```

**參數**

下表說明`INSERT INTO`命令所需的引數：

| 參數 | 說明 |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | 建立為create audience命令一部分的表格名稱。 |
| `select_query` | SELECT陳述式。 您可以在SELECT查詢區段中找到SELECT查詢的語法。 |

{style="table-layout:auto"}

**範例：**

下列範例示範如何使用`INSERT INTO`命令將設定檔新增到現有對象：

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### RFM模型對象範例 {#rfm-model-audience-example}

下列範例示範如何使用「造訪間隔」、「頻率」和「營利」(RFM)模型來建立對象。 此範例會根據造訪間隔、頻率和營利得分來劃分客戶，以識別關鍵群組，例如忠誠客戶、新客戶和高價值客戶。

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

下列查詢會為RFM對象建立結構描述。 陳述式會設定欄位以儲存客戶資訊，例如`userId`、`days_since_last_purchase`、`orders`、`total_revenue`等。

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

建立受眾後，請使用客戶資料填入，並根據其RFM分數劃分設定檔。 以下SQL陳述式使用`NTILE(4)`函式，根據客戶的RFM （造訪間隔、頻率、營利）分數將客戶分至四分位數。 這些分數會將客戶分為六個區段，例如「核心」、「忠誠」和「鯨」。 然後區段的客戶資料會插入到對象`adls_rfm_profile`表格中。」

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### 刪除對象（刪除對象） {#delete-audience}

使用`DROP AUDIENCE`命令刪除現有的對象。 如果對象不存在，除非指定`IF EXISTS`，否則會發生例外狀況。

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**參數**

此表格包含`DROP AUDIENCE`命令所需的引數：

| 參數 | 說明 |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | 選填。 如果已指定，則在找不到資料表的事件中，不會引發例外狀況。 |
| `db_name` | 指定用來限定對象資料集的資料群組。 |
| `table_name` | 建立為create audience命令一部分的表格名稱。 |

{style="table-layout:auto"}

**範例：**

下列範例示範如何使用DROP AUDIENCE命令刪除對象：

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### 自動對象註冊與可用性 {#registration-and-availability}

使用SQL擴充功能建立的對象會自動在Audience工作區的Data Distiller [!UICONTROL Origin]下註冊。 註冊後，這些受眾即可在檔案型目的地中用於鎖定目標、增強細分和目標定位策略。 此程式不需要額外設定，可簡化受眾管理。 如需如何在Platform UI中檢視、管理和建立對象的詳細資訊，請參閱[對象入口網站概觀](../../segmentation/ui/audience-portal.md)。

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Adobe Experience Platform中的對象工作區，顯示自動發佈且可供使用的資料Distiller對象。](../images/data-distiller/sql-audiences/audiences.png)

## 針對目的地啟用客群 {#activate-audiences}

將對象鎖定在任何以檔案為基礎的目的地（例如[!DNL Amazon S3]、[!DNL SFTP]或[!DNL Azure Blob]），以啟用對象。 擴充的對象屬性可於需要時進行進一步細分和篩選。

![Adobe Experience Platform目的地型別的流程圖，顯示公開和私人/自訂目的地，包括批次和串流選項。](../images/data-distiller/sql-audiences/destination-types.png)

## 功能說明 {#faqs}

本節說明在Data Distiller中使用SQL建立和管理外部受眾的相關常見問題。

**問題**：

- 是否僅支援平面資料集進行受眾建立？

+++回答

目前，定義對象時，對象建立僅限於平面（根層級）屬性。

+++

- 建立對象會產生單一資料集或多個資料集，還是會根據設定而有所不同？

+++回答

對象和資料集之間有一對一的對應。

+++

- 在對象建立期間建立的資料集是否標籤為設定檔？

+++回答

否，在對象建立期間建立的資料集不會標籤為設定檔。

+++

- 資料集是否在資料湖上建立？

+++回答

是，與對象相關聯的資料集會在資料湖上建立。 此資料集中的屬性可在對象撰寫器和目的地流程中作為擴充屬性使用。

+++

- 對象中的屬性是否僅限於企業批次檔案型目的地？ （是或否）

+++回答

不可以。 對象中的擴充屬性可用於企業批次和檔案型目的地。 如果您遇到「以下區段ID具有此目的地不允許的名稱空間： e917f626-a038-42f7-944c-xyxyx」等錯誤，請在Data Distiller中建立新區段，並將其用於任何可用的目的地。

+++

- 我可以建立使用Data Distiller對象的對象嗎？

+++回答

可以，您可以建立使用Data Distiller受眾的受眾受眾。

+++

- 這些對象會出現在Adobe Journey Optimizer中嗎？ 如果沒有，我在規則產生器中建立新對象（包含此對象的所有成員）時，會發生什麼事？

+++回答

Adobe Journey Optimizer中也提供資料Distiller對象。 您可以在Adobe Journey Optimizer中使用Data Distiller受眾，並根據擴充的屬性篩選結果。

+++

- Data Distiller受眾是外部受眾，是否每30天刪除一次？

+++回答

是的，Data Distiller對象是外部對象，每30天會刪除一次。

+++

## 後續步驟

閱讀本檔案後，您已瞭解如何在資料Distiller中使用SQL對象擴充功能，以使用SQL命令有效建立、管理和發佈對象。 您現在可以根據獨特的業務需求自訂對象定義，並在各種目的地啟用對象定義，以最佳化行銷策略和資料導向式決策。

接下來，您可以閱讀下列檔案，進一步開發並最佳化Platform對象管理策略：

- **探索對象評估**：瞭解Adobe Experience Platform中的[對象評估方法](../../segmentation/home.md#evaluate-segments)：即時更新的串流細分、排程或隨選處理的批次細分，以及即時評估Edge Network的邊緣細分。
- **與目的地整合**：閱讀如何使用Platform目的地UI [隨選匯出檔案至批次目的地](../../destinations/ui/export-file-now.md)的指南。
- **檢閱對象效能**：分析您的SQL定義對象在不同管道中的執行方式。 使用資料深入分析來調整和改善您的對象定義和定位策略。 閱讀有關[對象深入分析](../../dashboards/insights/audiences.md)的檔案，瞭解如何在Adobe Real-Time CDP中存取和調整SQL查詢，以獲得對象深入分析。 接著，您可以自訂「對象」控制面板，建立自己的深入分析，並將原始資料轉換為可操作的資訊，以有效視覺化並運用這些深入分析，做出更好決策。

