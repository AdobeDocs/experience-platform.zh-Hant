---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；重複資料消除；
solution: Experience Platform
title: 查詢服務中的重複資料消除
type: Tutorial
description: 本文檔概述了用於消除重複的三個常見使用情形體驗事件、採購和度量的子選擇和完整示例查詢示例。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 中的重複資料消除 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支援重複資料消除。 當需要從計算中刪除整個行或忽略特定的一組欄位時，可以執行重複資料消除，因為該行中只有一部分資料是重複資訊。

重複資料消除通常涉及使用 `ROW_NUMBER()` 在窗口中按順序顯示ID（或一對ID）的函式，返回表示檢測到重複的次數的新欄位。 時間通常通過使用 [!DNL Experience Data Model] (XDM) `timestamp` 的子菜單。

當 `ROW_NUMBER()` 是 `1`，它指的是原始實例。 通常，您希望使用該實例。 這通常在子選擇內完成，其中重複資料消除在更高級別中完成 `SELECT` 比如執行聚合計數。

重複資料消除使用情形可以是全局的，也可以是限制為單個用戶或最終用戶ID `identityMap`。

本文檔概述了如何針對以下三種常見使用情形執行重複資料消除：體驗事件、購買和指標。

每個示例都包括範圍、窗口鍵、重複資料消除方法的概要以及完整SQL查詢。

## 體驗事件 {#experience-events}

如果是重複的「體驗事件」，您可能希望忽略整個行。

>[!CAUTION]
>
>許多資料集 [!DNL Experience Platform]包括由Adobe Analytics資料連接器生產的，已應用了經驗事件級重複資料消除。 因此，重新應用此級別的重複資料消除是不必要的，並且會降低查詢速度。
>
>瞭解資料集的來源並瞭解體驗事件級別的重複資料消除是否已應用非常重要。 對於流式傳輸的任何資料集(例如，來自Adobe Target的資料集)，您 **會** 需要應用體驗事件級重複資料消除，因為這些資料源具有「至少一次」語義。

**範圍：** 全球

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

### 完整示例

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

如果您有重複的購買，您可能希望保留 [!DNL Experience Event] 行，但忽略與採購關聯的欄位(如 `commerce.orders` 度量)。 採購包含採購ID的特殊欄位， `commerce.order.purchaseID`。

建議使用 `purchaseID` 訪問者範圍內，因為它是XDM內購買ID的標準語義欄位。 建議刪除重複的採購資料存取器範圍，因為查詢比使用全局範圍快，並且採購ID不太可能跨多個訪問者ID重複。

**範圍：** 訪問者

**窗口鍵：** 標識映射[$命名空間].id &amp; commerce.order.purchaseID

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

>[!NOTE]
>
>在原始分析資料具有跨訪問者ID的重複採購ID的某些情況下，您 **五月** 需要在所有訪問者中運行採購ID重複計數。 當採購ID不存在時，此方法要求您包括一個條件，該條件會改用事件ID來盡可能快地保持查詢。

### 完整示例

下面的示例在採購ID不存在時使用條件子句來使用事件ID。

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

如果您有使用可選唯一ID的度量，並且顯示該ID的重複項，則可能希望忽略該度量值並保留「體驗事件」的其餘部分。

在XDM中，幾乎所有度量都使用 `Measure` 包括可選資料類型 `id` 用於重複資料消除的欄位。

**範圍：** 訪問者

**窗口鍵：** 標識映射[$命名空間].id和度量對象的id

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

### 完整示例

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

本文檔提供了重複資料消除示例，並概述了如何在查詢服務中執行重複資料消除。 有關使用查詢服務編寫查詢時的更多最佳做法，請閱讀 [編寫查詢指南](../best-practices/writing-queries.md)。
