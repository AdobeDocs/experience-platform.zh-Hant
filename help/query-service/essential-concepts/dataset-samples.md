---
title: 資料集示例
description: Query Service示例資料集使您能夠對大資料執行探索性查詢，同時大大減少了處理時間，並犧牲了查詢準確性。 本指南提供了有關如何管理示例以便進行近似查詢處理的資訊
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 資料集示例

Adobe Experience Platform查詢服務提供示例資料集作為其近似查詢處理功能的一部分。 使用現有樣本中的均勻隨機樣本建立樣本資料集 [!DNL Azure Data Lake Storage] (ADLS)資料集僅使用原始資料中的百分比記錄。 此百分比稱為採樣率。 通過調整採樣率來控制精度和處理時間的平衡，您可以對大資料執行探索性查詢，同時大大減少了處理時間，並犧牲了查詢精度。

由於許多用戶不需要針對資料集上的聚合操作給出確切答案，因此發出近似查詢以返回近似答案對於大型資料集上的探索性查詢更為有效。 由於示例資料集只包含原始資料集中資料的一個百分點，因此您可以使用查詢準確性來縮短響應時間。 在讀取時，查詢服務必須掃描的行數更少，這比查詢整個資料集時生成結果的速度更快。

為幫助您管理示例以進行近似查詢處理，Query Service支援以下資料集示例操作：

- [建立統一隨機資料集樣本。](#create-a-sample)
- [（可選）指定篩選條件](##optional-filter-criteria)
- [查看ADLS表的示例清單。](#view-list-of-samples)
- [直接查詢示例資料集。](#query-sample-datasets)
- [刪除示例。](#delete-a-sample)
- 刪除原始ADLS表時刪除關聯的示例。

## 快速入門 {#get-started}

要使用本文檔中詳細描述的建立和刪除近似查詢處理功能，必須將會話標誌設定為 `true`。 在查詢編輯器或PSQL客戶端的命令行中輸入 `SET aqp=true;` 的子菜單。

>[!NOTE]
>
>每次登錄平台時必須啟用會話標誌。

![突出顯示了「SET aqp=true；」命令的查詢編輯器。](../images/essential-concepts/set-session-flag.png)

## 建立統一隨機資料集樣本 {#create-a-sample}

使用 `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` 命令，以從該資料集建立統一的隨機示例。

採樣率是從原始資料集中提取的記錄的百分比。 您可以使用 `TABLESAMPLE SAMPLERATE` 關鍵字。 在本例中，5.0的值等於50%的採樣率。 值2.5等於25%，依此類推。

>[!IMPORTANT]
>
>該系統允許每個資料集最多五個樣本。 如果嘗試建立第六個示例資料集，螢幕上將顯示一條錯誤消息，指出已達到示例限制。

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## （可選）指定篩選條件 {#optional-filter-criteria}

您可以選擇為統一隨機抽樣指定篩選條件。 這允許您基於分析表的篩選子集建立示例。

建立示例時，首先應用可選篩選器，然後從資料集的篩選視圖建立示例。 具有應用篩選器的資料集示例遵循以下查詢格式：

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

此類過濾樣本資料集的實例如下：

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

在提供的示例中，表名為 `large_table`，原始表上的篩選條件為 `month(to_timestamp(timestamp)) in ('8', '9')`，採樣率為（濾波資料的X%）, `10`。

## 查看示例清單 {#view-list-of-samples}

使用 `sample_meta()` 函式，查看與ADLS表關聯的示例清單。

```sql
SELECT sample_meta('example_dataset_name')
```

資料集示例清單以下例的格式顯示。

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 查詢示例資料集 {#query-sample-datasets}

使用 `{EXAMPLE_DATASET_NAME}` 直接查詢示例表。 或者，添加 `WITHAPPROXIMATE` 關鍵字到查詢結尾，查詢服務自動使用最近建立的示例。

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## 刪除資料集示例 {#delete-a-sample}

刪除操作允許您在達到五個資料集樣本的最大限制後建立新樣本。

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>如果您有從原始ADLS資料集派生的多個示例資料集，則刪除原始資料集時，所有關聯的示例也會被刪除。
