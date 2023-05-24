---
title: 派生屬性的無縫SQL流
description: Query Service SQL已擴展，為派生屬性提供無縫支援。 瞭解如何使用此SQL擴展建立為配置檔案啟用的派生屬性，以及如何將該屬性用於即時客戶配置檔案和分段服務。
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 6202b1a5956da83691eeb5422d3ebe7f3fb7d974
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# 派生屬性的無縫SQL流

Query Service SQL已擴展，為派生屬性提供無縫支援。 這為您的Real-Time Customer Profile業務使用案例建立派生屬性提供了一種有效的替代方法。

本文檔概述了各種方便的SQL擴展，這些擴展生成了用於即時客戶概要檔案的派生屬性。 該工作流簡化了通過各種API調用或平台UI交互而必須完成的過程。

通常，生成和發佈Real-Time Customer Profile的屬性將涉及以下步驟：

* 建立標識命名空間（如果尚不存在）。
* 建立用於儲存派生屬性的資料類型（如有必要）。
* 建立具有該資料類型的欄位組以儲存派生的屬性資訊。
* 建立或分配具有先前建立的命名空間的主標識列。
* 使用先前建立的欄位組和資料類型建立方案。
* 使用您的架構建立新資料集，並根據需要將其啟用為配置檔案。
* （可選）將資料集標籤為已啟用配置檔案。

完成上述步驟後，即可填充資料集。 如果為配置檔案啟用了資料集，則還可以建立引用新屬性的段並開始生成洞見。

Query Service允許您使用SQL查詢執行上面列出的所有操作。 這包括根據需要對資料集和欄位組進行更改。

## 建立帶選項的表以啟用配置檔案 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查詢假定使用了預先存在的命名空間。

使用「建立表為選擇」(CTAS)查詢可建立資料集、分配資料類型、設定主標識、建立方案並將其標籤為啟用配置檔案。 下面的示例SQL陳述式建立屬性，並使其可用於即時客戶資料配置檔案(Real-Time CDP)。 SQL查詢將遵循以下示例中所示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

支援的資料類型包括：boolean 、 datetime 、 text 、 float 、 bigint 、 integer 、 map 、 array和struct/row。

下面的SQl代碼塊提供了定義結構/行、映射和陣列資料類型的示例。 第一行演示行語法。 第二行演示了映射語法和第三行陣列語法。

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

或者，也可以通過平台UI為配置檔案啟用資料集。 有關將資料集標籤為已啟用配置檔案的詳細資訊，請參閱 [為Real-Time Customer Profile文檔啟用資料集](../../../catalog/datasets/user-guide.md#enable-profile)。

在下面的示例查詢中， `decile_table` 資料集建立時 `id` 作為主標識列，並具有命名空間 `IDFA`。 它還有一個名為 `decile1Month` 的子菜單。 建立的表(`decile_table`)。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

成功執行查詢後，資料集ID將返回控制台，如下例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

使用 `label='PROFILE'` 在 `CREATE TABLE` 命令建立啟用配置檔案的資料集。 的 `upsert` 預設情況下，功能處於開啟狀態。 的 `upsert` 權能可使用 `ALTER` 命令，如下例所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

有關使用的詳細資訊，請參閱SQl語法文檔 [更改表](../../sql/syntax.md#alter-table) 命令和 [標籤作為CTAS查詢的一部分](../../sql/syntax.md#create-table-as-select)。

## 用於幫助通過SQL管理派生屬性的結構

下面介紹的功能在通過SQL管理派生屬性時非常有用。

### 更改要為配置檔案啟用的現有資料集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL構造可用於為配置檔案啟用現有資料集。 這要求將啟用配置檔案的標籤添加到模式和相應的資料集。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>論《中華人民共和國宣言》 `ALTER TABLE` 命令，控制台返回 `ALTER SUCCESS`。

### 將主標識添加到現有資料集 {#add-primary-identity}

將資料集中的現有列標籤為主標識集，否則將導致錯誤。 要使用SQL設定主標識，請使用下面顯示的查詢格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的示例中， `id2` 是 `test1_dataset`。

### 禁用配置檔案的資料集 {#disable-dataset-for-profile}

如果要禁用表以用於配置檔案，則必須使用DROP命令。 USES的SQL陳述式示例 `DROP` 下面顯示。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL陳述式為使用API調用提供了一種有效的替代方法。 有關詳細資訊，請參閱有關如何 [使用資料集API禁用資料集以與Real-Time CDP一起使用](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile)。

### 允許更新和插入資料集的功能 {#enable-upsert-functionality-for-dataset}

UPSERT命令允許您插入新記錄或更新表中的現有資料。 具體而言，它允許您在表中已存在指定值時更新現有行，或在指定值不存在時插入新行。

下面顯示了使用正確格式的示例語句。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL陳述式為使用API調用提供了一種有效的替代方法。 有關詳細資訊，請參閱有關如何 [使用資料集API啟用資料集以與Real-Time CDP和UPSERT一起使用](../../../catalog/datasets/enable-upsert.md#enable-the-dataset)。

### 禁用資料集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

此命令禁用更新行並將行插入資料集的功能。

下面顯示了使用正確格式的示例語句。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 顯示與每個表關聯的其他表資訊 {#show-labels-for-tables}

為啟用配置檔案的資料集保留其他元資料。 使用 `SHOW TABLES` 命令以顯示額外 `labels` 列，其中提供了有關與表關聯的任何標籤的資訊。

以下是此命令輸出的示例：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

從示例中可以看出 `table_with_a_decile` 已啟用配置檔案，並與標籤(如 [「UPSERT」](#enable-upsert-functionality-for-dataset)。 [「配置檔案」](#enable-existing-dataset-for-profile) 如前所述。

### 使用SQL建立欄位組

現在可以通過使用SQL建立欄位組。 這為在平台UI中使用架構編輯器或對架構註冊表進行API調用提供了替代方法。

下面可以看到建立欄位組的示例語句。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>如果SQL的 `label` 語句中未提供標誌，或者欄位組已存在。
>確保查詢包含 `IF NOT EXISTS` 子句，以避免查詢失敗，因為欄位組已存在。

一個真實世界的例子可能與下面看到的類似。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功執行此語句將返回已建立的欄位組ID。 例如 `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

請參閱有關如何 [在架構編輯器中建立新欄位組](../../../xdm/ui/resources/field-groups.md#create) 或使用 [架構註冊表API](../../../xdm/api/field-groups.md#create) 的雙曲餘切值。

### 刪除欄位組

有時可能需要從架構註冊表中刪除欄位組。 通過執行 `DROP FIELDGROUP` 命令。

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

例如：

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>如果欄位組不存在，則通過SQL刪除欄位組將失敗。 確保語句包含 `IF EXISTS` 子句，以避免查詢失敗。

### 顯示表的所有欄位組名稱和ID

的 `SHOW FIELDGROUPS` 命令返回一個包含表的名稱、fieldgroupId和所有者的表。

以下是此命令輸出的示例：

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## 後續步驟

閱讀此文檔後，您更瞭解如何使用SQL建立基於派生屬性的配置檔案和啟用更新的資料集。 您現在可以將此資料集與批處理接收工作流一起使用，以更新您的配置檔案資料。 要瞭解有關將資料導入Adobe Experience Platform的更多資訊，請首先閱讀 [資料攝取概述](../../../ingestion/home.md)。
