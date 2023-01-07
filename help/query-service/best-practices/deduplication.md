---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；重複資料刪除；重複資料刪除；
solution: Experience Platform
title: 查詢服務中的重複資料刪除
type: Tutorial
description: 本檔案概述子選取和完整的查詢範例，以刪除重複的三個常見使用案例：體驗事件、購買和量度。
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 中的重複資料刪除 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支援重複資料刪除。 當需要從計算中刪除整個行或忽略特定欄位集時，可以執行重複資料消除，因為行中只有一部分資料是重複資訊。

重複資料刪除通常涉及使用 `ROW_NUMBER()` 會在視窗間傳回ID（或一對ID），而這會傳回一個新欄位，代表偵測到重複項目的次數。 時間通常以 [!DNL Experience Data Model] (XDM) `timestamp` 欄位。

當 `ROW_NUMBER()` is `1`，則會參照原始例項。 一般來說，這就是您想使用的例項。 這通常會在子選取內完成，而重複資料刪除是在較高層級完成 `SELECT` 例如執行匯總計數。

重複資料刪除的使用案例可以是全域性的，或限制為 `identityMap`.

本檔案概述如何針對三種常見使用案例執行重複資料刪除：體驗事件、購買和量度。

每個示例都包括範圍、窗口鍵、重複資料消除方法的大綱以及完整的SQL查詢。

## 體驗事件 {#experience-events}

若是重複的體驗事件，您可能會想要忽略整列。

>[!CAUTION]
>
>中的許多資料集 [!DNL Experience Platform]，包括Adobe Analytics Data Connector所產生的重複資料刪除，已套用體驗事件層級重複資料刪除。 因此，不需要重新應用此級別的重複資料消除，這會減慢查詢速度。
>
>請務必了解資料集的來源，並了解是否已套用體驗事件層級的重複資料刪除，這點非常重要。 對於串流的任何資料集(例如來自Adobe Target的資料集)，您 **will** 需要套用體驗事件層級重複資料刪除，因為這些資料來源具有「至少一次」語義。

**範圍：** 全球

**窗口鍵：** `id`

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

## 購買 {#purchases}

如果您有重複的購買，您可能會想要保留 [!DNL Experience Event] ，但忽略與購買相連結的欄位(例如 `commerce.orders` 量度)。 購買包含購買ID的特殊欄位，即 `commerce.order.purchaseID`.

建議使用 `purchaseID` 在訪客範圍內，因為這是XDM內購買ID的標準語義欄位。 建議移除重複的購買資料使用訪客範圍，因為查詢比使用全域範圍更快，而且購買ID不太可能跨多個訪客ID重複。

**範圍：** 訪客

**窗口鍵：** identityMap[$命名空間].id與commerce.order.purchaseID

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
>在某些情況下，如果原始Analytics資料在訪客ID之間有重複的購買ID，您 **5月** 需要對所有訪客執行購買ID重複計數。 當購買ID不存在時，此方法會要求您加入條件，而非使用事件ID來盡快保持查詢。

### 完整範例

以下範例使用條件子句，在購買ID不存在時使用事件ID。

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

如果您的量度使用選用的唯一ID，且該ID的重複項目出現，您可能會想要忽略該量度值，並保留其餘的體驗事件。

在XDM中，幾乎所有量度都使用 `Measure` 包含選用項目的資料類型 `id` 欄位，您可用於重複資料刪除。

**範圍：** 訪客

**窗口鍵：** identityMap[$命名空間]度量對象的.id和id

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

本檔案概述如何在Query Service中執行重複資料刪除，以及重複資料刪除的範例。 有關使用Query Service編寫查詢時的更多最佳做法，請閱讀 [撰寫查詢指南](./writing-queries.md).
