---
title: Query Acceleded Store Reporting Insights指南
description: 瞭解如何通過查詢服務構建報告見解資料模型，以便與加速的儲存資料和用戶定義的儀表板一起使用。
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# 查詢加速儲存報告見解指南

查詢加速儲存使您能夠減少從資料中獲取關鍵見解所需的時間和處理能力。 通常，資料會按定期間隔（例如，按小時或每日處理）進行處理，在此期間建立並報告聚合視圖。 從匯總資料中生成的這些報告的分析得出旨在改進業務表現的見解。 查詢加速儲存提供快取服務、併發、交互體驗和無狀態API。 但是，它假定資料經過預處理並優化以用於聚合查詢，而不是用於原始資料查詢。

查詢加速儲存允許您構建自定義資料模型和/或擴展現有的Adobe Real-time Customer Data Platform資料模型。 然後，您可以將報告洞察力納入或嵌入您選擇的報告/可視化框架。 請參閱Real-time Customer Data Platform洞察力資料模型文檔以瞭解如何 [自定義SQL查詢模板，為您的市場營銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表](../../../dashboards/cdp-insights-data-model.md)。

Adobe Experience Platform的Real-Time CDP資料模型提供了對概況、段和目的地的洞察，並啟用了Real-Time CDP洞察儀錶盤。 本文檔將指導您完成建立報告見解資料模型的過程，以及如何根據需要擴展Real-Time CDP資料模型。

## 先決條件

本教程使用用戶定義的儀表板在平台UI中可視化自定義資料模型中的資料。 請參閱 [用戶定義的儀表板文檔](../../../dashboards/user-defined-dashboards.md) 瞭解有關此功能的詳細資訊。

## 快速入門

資料DistillerSKU需要構建自定義資料模型，以便您能夠瞭解報告，並擴展保存豐富平台資料的Real-Time CDP資料模型。 請參閱 [包裝](../../packages.md) 和 [護欄](../../guardrails.md#query-accelerated-store) 與資料DistillerSKU相關的文檔。 如果您沒有資料DistillerSKU，請聯繫您的Adobe客戶服務代表以獲取詳細資訊。

<!-- Document is hidden temporarily
Please see the [packaging](../../packages.md), [guardrails](../../guardrails.md#query-accelerated-store), and [licensing](../../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

## 構建報告見解資料模型

本教程使用構建受眾洞察性資料模型的示例。 如果您使用一個或多個廣告商平台來接觸您的受眾，則可以使用廣告商的API獲取您的受眾的大致匹配計數。

一開始，您會從您的來源（可能來自您的廣告商平台API）獲得初始資料模型。 要對原始資料進行聚合視圖，請建立報告透視模型，如下圖所述。 這允許一個資料集獲取觀眾匹配的上下限。

![受眾洞察用戶模型的實體關係圖(ERD)。](../../images/query-accelerated-store/audience-insight-user-model.png)

在此示例中， `externalaudiencereach` 表/資料集基於ID並跟蹤匹配計數的下界和上界。 的 `externalaudiencemapping` 維表/資料集將外部ID映射到平台上的目標和段。

## 使用資料Distiller建立報告見解的模型

接下來，建立報告真知灼見模型(`audienceinsight` 在本示例中)，並使用SQL命令 `ACCOUNT=acp_query_batch and TYPE=QSACCEL` 確保在加速儲存上建立。 然後使用查詢服務建立 `audienceinsight.audiencemodel` 架構 `audienceinsight` 資料庫。

>[!NOTE]
>
>資料DistillerSKU是 `ACCOUNT=acp_query_batch` 的子菜單。 沒有它，在資料湖上建立一個常規資料模型。

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## 建立表、關係和填充資料

既然您已建立 `audienceinsight` reporting insight model，建立 `externalaudiencereach` 和 `externalaudiencemapping` 建立關係。 接下來，使用 `ALTER TABLE` 命令在表之間添加外鍵約束並定義關係。 以下SQL示例演示了如何執行此操作。

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

在成功執行兩個 `ALTER TABLE` 命令，形成事實表和尺寸表之間的關係。

語句運行後，使用 `SHOW datagroups;` 命令，從 `audienceinsight.audiencemodel`。 您的清單結果應與下面提供的示例類似。

>[!IMPORTANT]
>
>只有加速儲存中的資料才能從查詢服務無狀態API終結點訪問 `POST /data/foundation/query/accelerated-queries`。

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## 查詢報表透視資料模型

使用查詢服務查詢 `audiencemodel.externalaudiencereach` 維表。 下面可以看到查詢示例。

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

## 使用Real-Time CDP洞察力資料模型擴展您的資料模型

可以擴展受眾模型，並附加詳細資訊以建立更豐富的維表。 例如，可以將段名稱和目標名稱映射到外部訪問群體標識符。 為此，請使用查詢服務建立或刷新新資料集並將其添加到將段和目標與外部標識組合在一起的受眾模型。 下圖說明了此資料模型擴展的概念。

![連結Real-Time CDP洞察資料模型和查詢加速儲存模型的ERD圖。](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## 建立維表以擴展報告見解模型

使用查詢服務將密鑰描述性屬性從富集的Real-Time CDP維資料集添加到 `audienceinsight` 建立資料模型，並在事實表和新維表之間建立關係。 下面的SQL演示了如何將現有維表整合到報告見解資料模型中。

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

使用 `SHOW datagroups;` 命令，確認建立附加 `external_seg_dest_map` 維表。

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## 查詢擴展的加速儲存報告見解資料模型

現在 `audienceinsight` 資料模型已經擴展，已經可以查詢。 以下SQL顯示映射的目標和段的清單。

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

查詢返回查詢加速儲存上的所有資料集：

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

## 使用用戶定義的儀表板可視化資料

現在，您已建立了自定義資料模型，您已準備好使用自定義查詢和用戶定義的儀表板來可視化資料。

以下SQL提供了按目標中的受眾細分的匹配計數，以及按段細分的每個受眾目標。

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

下圖提供了使用報告透視資料模型的可能自定義可視化的示例。

![根據新報告透視資料模型建立的目標和段構件的匹配計數。](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

自定義資料模型可在用戶定義的儀表板工作區中可用資料模型清單中找到。 查看 [用戶定義的儀表板指南](../../../dashboards/user-defined-dashboards.md) 有關如何利用自定義資料模型的指導。
