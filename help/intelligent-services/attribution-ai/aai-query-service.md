---
keywords: 見解；屬性；屬性；屬性；屬性；屬性；屬性；屬性；屬性；屬性；屬性；attribution ai insights;AAI查詢服務；屬性查詢；屬性得分
feature: Attribution AI
title: 基於查詢服務的屬性評分分析
description: 瞭解如何使用Adobe Experience Platform查詢服務來分析Attribution AI分數。
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 使用查詢服務分析屬性得分

資料中的每一行表示轉換，在轉換中，相關觸點的資訊作為結構陣列儲存在 `touchpointsDetail` 的雙曲餘切值。

| 觸點資訊 | 欄 |
| ---------------------- | ------ |
| 觸點名稱 | `touchpointsDetail. touchpointName` |
| 觸點通道 | `touchpointsDetail.touchPoint.mediaChannel` |
| 觸點Attribution AI算法得分 | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## 查找資料路徑

在Adobe Experience PlatformUI中，選擇 **[!UICONTROL 資料集]** 的子菜單。 的 **[!UICONTROL 資料集]** 的子菜單。 接下來，選擇 **[!UICONTROL 瀏覽]** 頁籤，並查找Attribution AI分數的輸出資料集。

![訪問模型](./images/aai-query/datasets_browse.png)

選擇輸出資料集。 此時將顯示資料集活動頁。

![資料集活動頁](./images/aai-query/select_preview.png)

在資料集活動頁中，選擇 **[!UICONTROL 預覽資料集]** 在右上角預覽資料，並確保按預期接收資料。

![預覽資料集](./images/aai-query/preview_dataset.JPG)

預覽資料後，在右欄中選擇架構。 出現帶方案名稱和說明的跨距。 選擇方案名稱超連結以重定向到計分方案。

![選擇方案](./images/aai-query/select_schema.png)

使用計分方案，可以選擇或搜索值。 選擇後， **[!UICONTROL 欄位屬性]** 側軌開啟，允許您複製路徑以用於建立查詢。

![複製路徑](./images/aai-query/copy_path.png)

## 訪問查詢服務

要從平台UI中訪問查詢服務，請通過選擇 **[!UICONTROL 查詢]** 在左側導航中，選擇 **[!UICONTROL 瀏覽]** 頁籤。 載入先前保存的查詢的清單。

![查詢服務瀏覽](./images/aai-query/query_tab.png)

下一步，選擇 **[!UICONTROL 建立查詢]** 在右上角。 將載入查詢編輯器。 使用查詢編輯器，您可以開始使用計分資料建立查詢。

![查詢編輯器](./images/aai-query/query_example.png)

有關查詢編輯器的詳細資訊，請訪問 [查詢編輯器使用手冊](../../query-service/ui/user-guide.md)。

## 用於屬性得分分析的查詢模板

下面的查詢可用作不同得分分析方案的模板。 您需要 `_tenantId` 和 `your_score_output_dataset` 在計分輸出架構中找到正確的值。

>[!NOTE]
>
> 根據資料的接收方式，下面使用的值如 `timestamp` 可能是另一種格式。

### 驗證示例

**按轉換事件（在轉換窗口中）進行的轉換總數**

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

**僅轉換事件總數（在轉換窗口中）**

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

### 趨勢分析示例

**每天轉換數**

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

### 分佈分析示例

**按定義類型（在轉換窗口中）顯示轉換路徑上的接點數**

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

### 真知灼見生成示例

**按觸點和轉換日期（在轉換窗口中）分解的增量單位**

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

**按觸點和觸點日期（在轉換窗口中）劃分的增量單位**

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

**所有評分模型（在轉換窗口中）的某類觸地點的聚合得分**

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

**高級 — 路徑長度分析**

獲取每個轉換事件類型的路徑長度分佈：

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

**高級 — 轉換路徑分析上的點數不同**

獲取每個轉換事件類型的轉換路徑上不同觸點數的分佈：

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

### 架構展平和展開示例

此查詢將結構列拼合為多個單數列，並將分解陣列分解為多個行。 這有助於將屬性分數轉換為CSV格式。 此查詢的輸出在每行中具有一個轉換和一個對應於該轉換的觸點。

>[!TIP]
>
> 在此示例中，您需要 `{COLUMN_NAME}` 除了 `_tenantId` 和 `your_score_output_dataset`。 的 `COLUMN_NAME` 變數可以採用配置Attribution AI模型期間添加的可選傳遞列名（報告列）的值。 請查看您的評分輸出架構以查找 `{COLUMN_NAME}` 完成此查詢所需的值。

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
