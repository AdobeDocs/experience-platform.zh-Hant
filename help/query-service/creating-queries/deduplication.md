---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: 重複資料消除
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---


# 在 [!DNL Query Service]

Adobe Experience Platform可 [!DNL Query Service] 能需要從計算中移除整個列，或忽略特定欄位集，因為只有行中的部分資料是重複資料，因此支援重複資料處理。 重複資料消除的常見模式包括 `ROW_NUMBER()` ，在有序時間(使用 [!DNL Experience Data Model]`timestamp` (XDM)欄位)跨窗口使用ID或一對ID的函式，以返回表示檢測到重複的次數的新欄位。 當此值為時， `1`即表示原始例項，在大多數情況下，即您想使用的例項，而忽略其他每個例項。 這通常是在子選擇內完成的，在子選擇內，重複資料消除是在較高級別(如執行聚合計 `SELECT` 數)中完成的。

## 使用個案

重複資料消除的某些使用案例跨日期範圍是全局的，有些使用案例僅限於中的單個訪客或最終用戶ID `identityMap`。

本文檔概述了用於消除重複的三種常見使用案例的子選擇和完整示例查詢示例：
- [ExperienceEvents](#experienceevents)
- [購買](#purchases)
- [量度](#metrics)

### ExperienceEvents {#experienceevents}

若是重複的ExperienceEvents，您可能會希望忽略整列。

>[!CAUTION]
>
>許多DataSets(包 [!DNL Experience Platform]括Adobe Analytics Data Connector製作的DataSets)都已套用ExperienceEvent層級的去重複化功能。 因此，無需重新應用此級別的重複資料消除，並會減慢查詢速度。 請務必瞭解DataSet的來源，並瞭解是否已在ExperienceEvent層級應用重複資料消除。 對於任何串流化的DataSet（例如Adobe Target），您必須套用ExperienceEvent層級的去重複化，因為這些資料來源具有「至少一次」的語義。

**範圍：** 全球

**窗口鍵：** id

#### 子選擇

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### 完整範例

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

### 購買 {#purchases}

如果您有重複的購買，您可能會希望保留大部分的ExperienceEvent列，但忽略與購買相關聯的欄位(例如 `commerce.orders` 量度)。 對於購買，購買ID有特殊欄位。 此欄位為 `commerce.order.purchaseID`。

**範圍：** 訪客

**窗口鍵：** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### 子選擇

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

#### 完整範例

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

### 量度 {#metrics}

如果您有使用可選唯一ID的量度，且顯示該ID的復本，您可能會想要忽略該量度值，並保留其餘的ExperienceEvent。 在XDM中，幾乎所有度量都使用 `Measure` 包含可選欄位的數 `id` 據類型，您可以使用該欄位進行重複資料消除。

**範圍：** 訪客

**窗口鍵：** identityMap[$NAMESPACE].id &amp; id of Measure物件

#### 子選擇

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

#### 完整範例

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
