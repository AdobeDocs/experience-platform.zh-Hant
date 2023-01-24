---
title: Query Accelerated Store Reporting Insights指南
description: 了解如何透過Query Service建立報表前瞻分析資料模型，以便與加速儲存資料和使用者定義的控制面板搭配使用。
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Query Accelerated Store報告深入分析指南

查詢加速儲存可讓您縮短從資料中獲取重要見解所需的時間和處理能力。 通常會以定期的間隔（例如，每小時或每日）處理資料，以建立匯總檢視並據以報告。 這些從匯總資料產生的報表分析衍生出旨在改善業務績效的深入分析。 查詢加速儲存提供快取服務、並行、互動式體驗和無狀態API。 但是，它假設資料已經過預處理並針對聚合查詢進行了優化，而不是原始資料查詢。

查詢加速存放區可讓您建立自訂資料模型及/或擴充現有的Adobe Real-time Customer Data Platform資料模型。 然後，您就可以參與報表分析，或將其嵌入您所選擇的報表/視覺效果架構中。 請參閱Real-time Customer Data Platform Insights資料模型檔案，了解如何 [自訂SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表](../../../dashboards/cdp-insights-data-model.md).

Adobe Experience Platform的Real-Time CDP資料模型可提供設定檔、區段和目的地的深入分析，並啟用Real-Time CDP深入分析控制面板。 本檔案會引導您完成建立報表前瞻分析資料模型的程式，並說明如何視需要擴充Real-Time CDP資料模型。

## 先決條件

本教學課程使用使用者定義的控制面板，將Platform UI中自訂資料模型的資料視覺化。 請參閱 [使用者定義的控制面板檔案](../../../dashboards/user-defined-dashboards.md) 以深入了解此功能。

## 快速入門

您必須建立自訂資料模型，以便進行報表分析，並擴充包含豐富Platform資料的Real-Time CDP資料模型，才能使用Data Distiller SKU。 請參閱 [包裝](../../packages.md), [護欄](../../guardrails.md#query-accelerated-store)，和 [授權](../../data-distiller/license-usage.md) 與資料Distiller SKU相關的檔案。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得詳細資訊。

## 建立報表前瞻分析資料模型

本教學課程使用建立受眾分析資料模型的範例。 如果您使用一或多個廣告商平台來觸及您的對象，則可以使用廣告商的API來取得您對象的大致相符計數。

一開始，您會從來源（可能是來自廣告商平台API）取得初始資料模型。 若要匯總檢視原始資料，請建立報表前瞻分析模型，如下圖所述。 這可讓一個資料集取得對象比對的上下界限。

![受眾分析使用者模型的實體關係圖(ERD)。](../../images/query-accelerated-store/audience-insight-user-model.png)

在此範例中， `externalaudiencereach` 表格/資料集以ID為基礎，並追蹤比對計數的下界和上界。 此 `externalaudiencemapping` 維度表格/資料集會將外部ID對應至Platform上的目的地和區段。

## 使用Data Distiller建立報表深入分析的模型

接下來，建立報表分析模型(`audienceinsight` 在此示例中)，並使用SQL命令 `ACCOUNT=acp_query_batch and TYPE=QSACCEL` 以確保在加速儲存區上建立。 然後使用Query Service來建立 `audienceinsight.audiencemodel` 的架構 `audienceinsight` 資料庫。

>[!NOTE]
>
>資料Distiller SKU是 `ACCOUNT=acp_query_batch` 命令。 若沒有，則會在資料湖上建立規則資料模型。

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## 建立表、關係和填充資料

現在您已建立 `audienceinsight` 報告分析模型，建立 `externalaudiencereach` 和 `externalaudiencemapping` 並建立它們之間的關係。 接下來，使用 `ALTER TABLE` 命令在表之間添加外鍵約束並定義關係。 以下SQL示例演示了如何執行此操作。

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

成功執行兩者後 `ALTER TABLE` 命令，則會形成數值表和維表之間的關係。

執行陳述式後，請使用 `SHOW datagroups;` 命令，從 `audienceinsight.audiencemodel`. 您的表格結果應類似於下面提供的範例。

>[!IMPORTANT]
>
>只有加速儲存中的資料可從Query Service無狀態API端點存取 `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## 查詢報表分析資料模型

使用查詢服務來查詢 `audiencemodel.externalaudiencereach` 維度表格。 以下是範例查詢。

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

清單結果包括計數和ID。

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## 使用Real-Time CDP前瞻分析資料模型擴充您的資料模型

您可以使用其他詳細資料擴充您的對象模型，以建立更豐富的維度表格。 例如，您可以將區段名稱和目的地名稱對應至外部對象識別碼。 若要這麼做，請使用Query Service建立或重新整理新資料集，並將其新增至對象模型，將區段和目的地與外部身分結合。 下圖說明此資料模型擴充功能的概念。

![連結Real-Time CDP分析資料模型和查詢加速儲存模型的ERD圖表。](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## 建立維度表格以擴充您的報表前瞻分析模型

使用Query Service將擴充的Real-Time CDP維度資料集中的關鍵描述性屬性新增至 `audienceinsight` 資料模型，並建立數值表與新維度表之間的關係。 以下的SQL示範如何將現有的維度表整合到您的報表深入分析資料模型中。

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

使用 `SHOW datagroups;` 命令確認建立其他 `external_seg_dest_map` 維度表格。

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## 查詢延伸加速儲存報告深入分析資料模型

現在， `audienceinsight` 資料模型已得到擴展，已準備好查詢。 以下SQL顯示映射的目標和段的清單。

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

查詢會傳回查詢加速儲存區上的所有資料集：

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## 使用使用者定義的控制面板將資料視覺化

現在您已建立自訂資料模型，可使用自訂查詢和使用者定義的控制面板將資料視覺化。

以下SQL提供依目標中對象的比對計數劃分，以及依區段的每個目標對象劃分。

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

下圖提供使用您的報表前瞻分析資料模型的可能自訂視覺效果範例。

![根據新的報表前瞻分析資料模型建立的目的地和區段介面工具集的比對計數。](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

您的自訂資料模型可在使用者定義控制面板工作區中可用的資料模型清單中找到。 請參閱 [使用者定義的控制面板指南](../../../dashboards/user-defined-dashboards.md) 以取得如何運用自訂資料模型的指引。
