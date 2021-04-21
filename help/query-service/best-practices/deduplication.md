---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；重複資料消除；
solution: Experience Platform
title: 查詢服務中的重複資料消除
topic-legacy: queries
type: Tutorial
description: 本檔案概述了用於消除重複的三個常見使用案例：體驗事件、購買和度量的子選取和完整範例查詢範例。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# [!DNL Query Service]中的重複資料消除

Adobe Experience Platform[!DNL Query Service]支援重複資料消除。 當需要從計算中刪除整個行或忽略特定欄位集時，可以執行重複資料消除，因為行中只有一部分資料是重複資訊。

重複資料刪除通常涉及在訂購時間內跨窗口使用`ROW_NUMBER()`函式來查找ID（或一對ID），這會返回一個新欄位，表示檢測到重複的次數。 該時間通常使用[!DNL Experience Data Model](XDM)`timestamp`欄位來表示。

當`ROW_NUMBER()`的值為`1`時，它會參照原始實例。 一般來說，這就是您想要使用的例項。 這通常是在子選擇內完成的，在子選擇內，重複資料消除在較高級別`SELECT`中完成，如執行聚合計數。

重複資料消除使用案例可以是全局的，也可以限制為`identityMap`中的單個用戶或最終用戶ID。

本文檔概述了如何對三個常見使用案例執行重複資料消除：體驗事件、購買和量度。

每個示例包括範圍、窗口鍵、重複資料消除方法的概要以及完整的SQL查詢。

## 體驗事件{#experience-events}

若是重複的「體驗事件」，您可能會希望忽略整列。

>[!CAUTION]
>
>[!DNL Experience Platform]中的許多資料集(包括由Adobe Analytics資料連接器生成的資料集)都已應用了「體驗——事件」級重複資料刪除。 因此，無需重新應用此級別的重複資料消除，並會減慢查詢速度。
>
>請務必瞭解資料集的來源，並瞭解是否已在Experience-Event層級套用重複資料消除。 對於任何串流化的資料集(例如來自Adobe Target的資料集)，您&#x200B;**將**&#x200B;需要套用體驗——事件層級的去重複化，因為這些資料來源具有「至少一次」的語義。

**範圍：全** 域

**窗口鍵：** `id`

### 重複資料消除示例

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### 完整範例

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## 購買 {#purchases}

如果您有重複的購買，您可能會希望保留大部分的「體驗事件」列，但忽略與購買相關聯的欄位（例如`commerce.orders`量度）。 購買包含購買ID的特殊欄位，即`commerce.order.purchaseID`。

**範圍：訪** 客

**視窗金鑰：** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### 重複資料消除示例

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

### 完整範例

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## 量度 {#metrics}

如果您有使用可選唯一ID的量度，且該ID出現復本，您可能會想要忽略該量度值，並保留其餘的「體驗事件」。

在XDM中，幾乎所有度量都使用`Measure`資料類型，其中包含可用於重複資料消除的可選`id`欄位。

**範圍：訪** 客

**視窗金鑰：** identityMap[$NAMESPACE].id和Measure物件的ID

### 重複資料消除示例

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### 完整範例

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## 後續步驟

本文檔概述了如何在查詢服務中執行重複資料消除，以及重複資料消除示例。 有關使用查詢服務編寫查詢時的更多最佳實踐，請閱讀[編寫查詢指南](./writing-queries.md)。
