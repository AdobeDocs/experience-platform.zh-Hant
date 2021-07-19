---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；疑難排解指南；faq；疑難排解；
solution: Experience Platform
title: 查詢服務疑難排解指南
topic-legacy: troubleshooting
description: 本文檔包含有關您遇到的常見錯誤代碼和可能原因的資訊。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e3557fe75680153f051b8a864ad8f6aca5f743ee
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# [!DNL Query Service] 疑難排解指南

本檔案提供查詢服務常見問題的解答，並提供使用查詢服務時常見錯誤代碼的清單。 有關Adobe Experience Platform中其他服務的問題和疑難排解，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

## 常見問答

以下是關於Query Service常見問題的解答清單。

### 如何只取得查詢的中繼資料？

若要僅取得查詢的中繼資料，您可以執行傳回零列的查詢，如下所示：

```sql
SELECT * FROM <table> WHERE 1=0
```

此查詢只返回指定表的元資料。

### 如何快速迭代CTAS（以選取方式建立表格）查詢，而不對其進行具體化？

您可以建立臨時表，以在將查詢實體化以供使用之前，快速迭代和實驗查詢。 您也可以使用臨時表格來驗證查詢是否可行。

例如，您可以建立臨時表格：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然後，您可以使用臨時表格，如下所示：

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= To_timestamp('2021-01-21 12:00:00')
AND timestamp < To_timestamp('2021-01-21 13:00:00')
LIMIT 100;
```

### 如何篩選我的時間序列資料？

使用時間序列資料進行查詢時，您應盡可能使用時間戳記篩選器，以進行更精確的分析。

以下是使用時間戳記篩選的範例：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### 我是否應使用萬用字元（例如*），從資料集中取得所有列？

您無法使用萬用字元(*)來從您的列取得所有資料，因為「查詢服務」應被視為&#x200B;**欄位式存放區**，而非傳統的以列為基礎的存放系統。

## REST API錯誤

| HTTP狀態代碼 | 說明 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 錯誤請求 | 格式錯誤或非法查詢 |
| 401 | 驗證失敗 | 驗證令牌無效 |
| 500 | 內部伺服器錯誤 | 內部系統故障 |

## PostgreSQL API錯誤

| 錯誤代碼和連接狀態 | 說明 | 可能的原因 |
| ------------------------------- | ----------- | -------------- |
| **28P01** 啟動 — 驗證 | 密碼無效 | 驗證令牌無效 |
| **28000** 啟動 — 驗證 | 授權類型無效 | 授權類型無效。 必須為`AuthenticationCleartextPassword`。 |
| **42P12** 啟動 — 驗證 | 未找到表 | 未找到要使用的表 |
| **42601查** 詢 | 語法錯誤 | 命令或語法錯誤無效 |
| **58000** 查詢 | 系統錯誤 | 內部系統故障 |
| **42P01查** 詢 | 未找到表 | 未找到查詢中指定的表 |
| **42P07查** 詢 | 表存在 | 具有相同名稱的表已存在(CREATE TABLE) |
| **53400查** 詢 | LIMIT超過最大值 | 用戶指定的LIMIT子句大於100,000 |
| **53400查** 詢 | 語句超時 | 提交的即時陳述最多需要10分鐘 |
| **08P01** 不適用 | 不支援的消息類型 | 不支援的消息類型 |
