---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；重複資料刪除；重複資料刪除；
solution: Experience Platform
title: 查詢服務中的重複資料刪除
type: Tutorial
description: 本檔案概述子選取和完整範例查詢範例，用於去除三個常見使用案例（體驗事件、購買和量度）。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# [!DNL Query Service]中的重複資料刪除

Adobe Experience Platform [!DNL Query Service]支援重複資料刪除。 當需要從計算中移除整個列或忽略特定欄位集（因為列中只有部分資料是重複資訊）時，可以執行重複資料刪除。

重複資料刪除通常涉及在順序時間內對ID （或一組ID）在視窗中使用`ROW_NUMBER()`函式，這會傳回代表偵測到重複專案次數的新欄位。 時間通常使用[!DNL Experience Data Model] (XDM) `timestamp`欄位來表示。

當`ROW_NUMBER()`的值為`1`時，它會參考原始執行個體。 一般而言，這是您想要使用的例項。 這通常會在子選取內完成，其中重複資料刪除會在較高層級`SELECT`中完成，就像執行彙總計數一樣。

重複資料刪除使用案例可以是全域的，或限製為`identityMap`中的單一使用者或一般使用者ID。

本檔案概述如何針對三個常見使用案例執行重複資料刪除：體驗事件、購買和量度。

每個範例都包含範圍、視窗索引鍵、重複資料刪除方法的大綱，以及完整的SQL查詢。

## 體驗事件 {#experience-events}

如果出現重複的體驗事件，您可能希望忽略整列。

>[!CAUTION]
>
>[!DNL Experience Platform]中的許多資料集(包括Adobe Analytics Data Connector產生的資料集)已套用體驗事件層級的重複資料刪除。 因此，重新套用此層級的重複資料刪除是不必要的，而且會減慢查詢速度。
>
>請務必瞭解資料集的來源，並知道是否已套用體驗事件層級的重複資料刪除。 對於串流處理的任何資料集(例如來自Adobe Target的資料集)，您&#x200B;**將**&#x200B;需要套用體驗事件層級的重複資料刪除，因為這些資料來源具有「至少一次」語意。

**領域：**&#x200B;全域

**視窗索引鍵：** `id`

### 重複資料刪除範例

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

## 購買次數 {#purchases}

如果您有重複購買，您可能會想要保留大多數[!DNL Experience Event]列，但忽略與購買相關聯的欄位（例如`commerce.orders`量度）。 購買包含購買ID的特殊欄位，即`commerce.order.purchaseID`。

建議在訪客範圍內使用`purchaseID`，因為這是XDM中購買ID的標準語意欄位。 建議使用訪客範圍來移除重複的購買資料，因為查詢的速度比使用全域範圍來得快，而且購買ID不太可能跨多個訪客ID重複。

**範圍：**&#x200B;訪客

**視窗索引鍵：** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### 重複資料刪除範例

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

>[!NOTE]
>
>在某些情況下，原始Analytics資料跨訪客ID具有重複的購買ID，您&#x200B;**可能**&#x200B;需要對所有訪客執行購買ID重複計數。 當購買ID不存在時，此方法需要您納入條件，以使用事件ID來儘可能快速地保留查詢。

### 完整範例

以下範例使用condition子句，在購買ID不存在的情況下使用事件ID。

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

如果您的量度使用選用的唯一ID，且出現該ID的重複專案，您可能會想要忽略該量度值，並保留體驗事件的其餘部分。

在XDM中，幾乎所有量度都使用`Measure`資料型別，其中包含您可用來重複資料刪除的選用欄位`id`。

**範圍：**&#x200B;訪客

**視窗索引鍵：** identityMap[$NAMESPACE].ID和Measure物件識別碼

### 重複資料刪除範例

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

本檔案提供重複資料刪除的範例，並說明如何在查詢服務內執行重複資料刪除。 如需使用查詢服務撰寫查詢時的最佳實務，請參閱[撰寫查詢指南](../best-practices/writing-queries.md)。
