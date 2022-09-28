---
title: 資料集範例
description: Query Service範例資料集可讓您對大資料執行探索性查詢，大幅縮短處理時間，並降低查詢準確度。 本指南提供如何管理範例以進行近似查詢處理的資訊
source-git-commit: 81531f8c5a89fd21a34d4fc233c2c57f79335f76
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 資料集範例

Adobe Experience Platform Query Service提供範例資料集，作為其近似查詢處理功能的一部分。 範例資料集是以現有的統一隨機範例建立 [!DNL Azure Data Lake Storage] (ADLS)資料集僅使用原始記錄的百分比。 此百分比稱為取樣率。 調整採樣率以控制精確度和處理時間的平衡，允許您對大資料進行探索性查詢，並大大減少處理時間，同時犧牲查詢準確性。

由於許多使用者不需要針對資料集的匯總作業提供確切的答案，因此發出近似查詢以傳回近似答案，對於大型資料集的探索性查詢會更有效率。 由於範例資料集僅包含原始資料集中資料的百分比，因此您可以利用查詢正確性來交易，以縮短回應時間。 在讀取時，Query Service必須掃描的列數更少，而產生結果的速度比查詢整個資料集的速度快。

為協助您管理範例以進行近似查詢處理，Query Service支援對資料集範例執行下列作業：

- [建立統一的隨機資料集範例。](#create-a-sample)
- [查看ADLS表的示例清單。](#view-list-of-samples)
- [直接查詢範例資料集。](#query-sample-datasets)
- [刪除範例。](#delete-a-sample)
- 刪除原始ADLS表格時的相關範例。

## 快速入門

若要使用上述的近似查詢處理功能，您必須將工作階段標幟設為 `true`. 從查詢編輯器或PSQL客戶端的命令行中，輸入 `SET aqp=true;` 命令。

>[!NOTE]
>
>每次登入平台時，都必須啟用工作階段標幟。

![突出顯示「SET aqp=true；」命令的查詢編輯器。](../images/sql/set-session-flag.png)

## 建立統一的隨機資料集範例 {#create-a-sample}

使用 `ANALYZE TABLE` 命令，以從該資料集建立統一的隨機樣本。

取樣率是從原始資料集取取的記錄百分比。 您可以使用 `TABLESAMPLE SAMPLERATE` 關鍵字。 在此範例中，值5.0相當於50%的取樣率。 值2.5等於25%，以此類推。

>[!IMPORTANT]
>
>系統最多可為每個資料集允許五個範例。 如果您嘗試建立第六個範例資料集，畫面會顯示錯誤訊息，指出已達到範例限制。

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## 查看示例清單 {#view-list-of-samples}

使用 `sample_meta()` 函式來檢視與ADLS表格相關聯的範例清單。

```sql
SELECT sample_meta('example_dataset_name')
```

資料集範例清單以下列範例格式顯示。

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 查詢範例資料集 {#query-sample-datasets}

使用 `{EXAMPLE_DATASET_NAME}` 直接查詢示例表。 或者，新增 `WITHAPPROXIMATE` 關鍵字到查詢結尾，查詢服務會自動使用最近建立的範例。

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## 刪除資料集範例 {#delete-a-sample}

刪除操作可讓您在達到五個資料集範例的上限後，建立新範例。

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>如果您有多個從原始ADLS資料集衍生的範例資料集，則刪除原始資料集時，所有相關的範例也會一併刪除。
