---
keywords: 見解；歸因ai；歸因ai洞察；AAI查詢服務；歸因查詢；歸因分數
solution: Intelligent Services, Experience Platform
title: 使用查詢服務分析歸因分數
topic-legacy: Attribution AI queries
description: 瞭解如何使用Adobe Experience Platform查詢服務來分析Attribution AI分數。
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 使用查詢服務分析歸因分數

資料中的每一列代表轉換，相關觸點的資訊會儲存為`touchpointsDetail`欄下的結構陣列。

| 觸點資訊 | 欄目 |
| ---------------------- | ------ |
| 觸點名稱 | `touchpointsDetail. touchpointName` |
| 觸點頻道 | `touchpointsDetail.touchPoint.mediaChannel` |
| 觸點Attribution AI演算法分數 | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## 尋找資料路徑

在Adobe Experience PlatformUI中，選擇左側導覽中的&#x200B;**[!UICONTROL Datasets]**。 此時將顯示&#x200B;**[!UICONTROL Datasets]**&#x200B;頁。 接著，選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，並尋找您的Attribution AI分數的輸出資料集。

![存取您的例項](./images/aai-query/datasets_browse.png)

選取您的輸出資料集。 此時會顯示資料集活動頁面。

![資料集活動頁](./images/aai-query/select_preview.png)

在資料集活動頁面中，選取右上角的&#x200B;**[!UICONTROL Preview dataset]**&#x200B;以預覽資料，並確定資料已如預期接收。

![預覽資料集](./images/aai-query/preview_dataset.JPG)

預覽資料後，請在右側欄中選取結構。 出現一個帶有架構名稱和說明的跨頁。 選擇模式名稱超連結以重定向至計分模式。

![選擇方案](./images/aai-query/select_schema.png)

使用計分結構，您可以選擇或搜索值。 選取後，**[!UICONTROL Field properties]**&#x200B;側欄會開啟，讓您複製路徑以用於建立查詢。

![複製路徑](./images/aai-query/copy_path.png)

## 存取查詢服務

若要從平台UI存取查詢服務，請從左側導覽中選取&#x200B;**[!UICONTROL Queries]**&#x200B;開始，然後選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤。 系統會載入先前儲存的查詢清單。

![查詢服務瀏覽](./images/aai-query/query_tab.png)

接著，選取右上角的&#x200B;**[!UICONTROL Create query]**。 查詢編輯器將載入。 使用查詢編輯器，您可以開始使用計分資料建立查詢。

![查詢編輯器](./images/aai-query/query_example.png)

有關查詢編輯器的詳細資訊，請訪問[查詢編輯器使用手冊](../../query-service/ui/user-guide.md)。

## 用于歸因分數分析的查詢範本

以下查詢可用作不同分數分析藍本的範本。 您需要將`_tenantId`和`your_score_output_dataset`取代為計分輸出結構中的適當值。

>[!NOTE]
>
> 根據資料的擷取方式，下列使用的值（例如`timestamp`）可能是不同的格式。

### 驗證範例

**依轉換事件（在轉換視窗中）劃分的轉換總數**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**僅限轉換的事件總數（在轉換視窗中）**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### 趨勢分析範例

**每天轉換次數**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### 分佈分析範例

**依定義類型（在轉換視窗中）劃分轉換路徑上的觸點數量**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### 洞察力產生範例

**依觸點和轉換日期（在轉換視窗中）劃分的遞增件數**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**依觸點和觸點日期（在轉換視窗中）劃分的遞增件數**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**針對所有計分模型（在轉換視窗中）的特定觸點類型匯總分數**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**進階——路徑長度分析**

取得每個轉換事件類型的路徑長度分佈：

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**進階——轉換路徑分析上的不同觸點數**

針對每個轉換事件類型，取得轉換路徑上不同觸點數目的分佈：

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

### 架構平面化和展開範例

此查詢會將結構列平面化為多個奇異列，並將陣列分解為多個行。 這有助於將歸因分數轉換為CSV格式。 此查詢的輸出具有一個轉換和一個對應於每行中該轉換的觸點。

>[!TIP]
>
> 在此範例中，除了`_tenantId`和`your_score_output_dataset`外，您還需要取代`{COLUMN_NAME}`。 `COLUMN_NAME`變數可取用在設定Attribution AI例項期間新增的選擇性傳遞欄名稱（報告欄）的值。 請檢閱計分輸出結構，以尋找完成此查詢所需的`{COLUMN_NAME}`值。

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
