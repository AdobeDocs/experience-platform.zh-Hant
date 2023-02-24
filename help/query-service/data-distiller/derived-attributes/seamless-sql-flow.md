---
title: 派生屬性的無縫SQL流
description: Query Service SQL已擴展，可提供衍生屬性的無縫支援。 了解如何使用此SQL擴充功能建立為設定檔啟用的衍生屬性，以及如何為即時客戶設定檔和細分服務使用屬性。
source-git-commit: 1ff66d0ac8e0491a6db518545d122555d9d54c75
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---

# 派生屬性的無縫SQL流

Query Service SQL已擴展，可提供衍生屬性的無縫支援。 這為您的即時客戶設定檔業務使用案例建立衍生屬性提供了有效的替代方法。

本文檔概述了各種方便的SQL擴展，這些擴展生成了用於即時客戶配置檔案的派生屬性。 工作流程可簡化您原本必須透過各種API呼叫或平台UI互動完成的程式。

通常，為「即時客戶設定檔」產生和發佈屬性時，會涉及下列步驟：

* 建立身分命名空間（如果尚未存在）。
* 如有必要，請建立資料類型以儲存派生屬性。
* 使用該資料類型建立欄位組以儲存派生屬性資訊。
* 使用先前建立的命名空間建立或指派主要身分欄。
* 使用先前建立的欄位組和資料類型建立架構。
* 使用您的結構建立新資料集，並視需要為設定檔啟用。
* （可選）將資料集標示為已啟用設定檔。

完成上述步驟後，即可填入資料集。 如果您為設定檔啟用資料集，也可以建立參照新屬性的區段，並開始產生深入分析。

查詢服務允許您使用SQL查詢執行上述所有操作。 這包括視需要變更資料集和欄位群組。

## 建立表格，並提供為設定檔啟用的選項 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查詢假設使用預先存在的命名空間。

使用「以選取方式建立表格」(CTAS)查詢來建立資料集、指派資料類型、設定主要身分、建立結構，以及將其標示為已啟用設定檔。 以下示例SQL陳述式建立屬性，並使其可用於即時客戶資料配置檔案(Real-Time CDP)。 您的SQL查詢將遵循以下範例中所示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

或者，您也可以透過Platform UI為設定檔啟用資料集。 如需將資料集標示為已啟用設定檔的詳細資訊，請參閱 [啟用即時客戶個人檔案檔案的資料集](../../../catalog/datasets/user-guide.md#enable-profile).

在以下範例查詢中， `decile_table` 資料集建立時使用 `id` 作為主要身分欄，且具有命名空間 `IDFA`. 還有一個欄位名為 `decile1Month` 地圖資料類型。 建立的表格(`decile_table`)已針對設定檔啟用。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

<!--        decile3Month map<text, integer>,
            decile6Month map<text, integer>,
            decile9month map<text, integer>,
            decile12month map<text, integer>,
            decilelifetime map<text, integer> -->

成功執行查詢時，資料集ID會傳回至主控台，如下列範例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

使用 `label='PROFILE'` 在 `CREATE TABLE` 命令建立啟用設定檔的資料集。 此 `upsert` 功能預設為啟用。 此 `upsert` 功能可使用 `ALTER` 命令，如以下示例所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

如需使用的詳細資訊，請參閱SQl語法檔案 [ALTER TABLE](../../sql/syntax.md#alter-table) 命令和 [標籤作為CTAS查詢的一部分](../../sql/syntax.md#create-table-as-select).

## 用於幫助通過SQL管理派生屬性的結構

以下所述的功能在通過SQL管理派生屬性時非常有益。

### 變更要為設定檔啟用的現有資料集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL結構可用於為配置檔案啟用現有資料集。 這需要將已啟用設定檔的標籤新增至結構和對應的資料集。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>關於成功執行 `ALTER TABLE` 命令，控制台返回 `ALTER SUCCESS`.

### 將主要身分新增至現有資料集 {#add-primary-identity}

將資料集中的現有欄標示為主要身分集，否則會導致錯誤。 要使用SQL設定主標識，請使用下面顯示的查詢格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的範例中， `id2` 是 `test1_dataset`.

### 停用設定檔的資料集 {#disable-dataset-for-profile}

如果要禁用配置檔案使用的表，必須使用DROP命令。 USES的示例SQL陳述式 `DROP` 顯示於下方。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL陳述式提供了使用API調用的有效替代方法。 如需詳細資訊，請參閱如何 [使用資料集API停用與Real-Time CDP搭配使用的資料集](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### 允許更新和插入資料集的功能 {#enable-upsert-functionality-for-dataset}

UPSERT命令允許您插入新記錄或更新表中的現有資料。 具體來說，它允許您在表中已存在指定值時更新現有行，或在指定值不存在時插入新行。

下面顯示了使用正確格式的示例語句。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL陳述式提供了使用API調用的有效替代方法。 如需詳細資訊，請參閱如何 [啟用資料集以與Real-Time CDP搭配使用，並使用資料集API將UPSERT插入](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### 停用資料集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

此命令會停用更新列並插入資料集的功能。

下面顯示了使用正確格式的示例語句。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 顯示與每個表關聯的其他表資訊 {#show-labels-for-tables}

已啟用設定檔的資料集會保留其他中繼資料。 使用 `SHOW TABLES` 顯示 `labels` 欄，提供有關與表關聯的任何標籤的資訊。

以下是此命令輸出的示例：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

您可從範例中看到 `table_with_a_decile` 已啟用設定檔，並套用標籤，例如 [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) 如先前所述。

### 使用SQL建立欄位組

現在可以透過使用SQL來建立欄位群組。 除了在Platform UI中使用結構編輯器，或對結構註冊表進行API呼叫外，此功能還提供其他方法。

下面可以看到建立欄位組的示例語句。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>如果 `label` 如果欄位組已存在，則語句中不提供標籤。
>請確定查詢包含 `IF NOT EXISTS` 子句，以避免查詢失敗，因為欄位組已存在。

真實世界的範例可能看起來類似於下列範例。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功執行此語句將返回已建立的欄位組ID。 例如 `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

請參閱如何 [在架構編輯器中建立新欄位群組](../../../xdm/ui/resources/field-groups.md#create) 或使用 [方案註冊表API](../../../xdm/api/field-groups.md#create) 以取得替代方法的詳細資訊。

### 刪除欄位組

有時可能需要從架構註冊表中刪除欄位組。 若要這麼做，請執行 `DROP FIELDGROUP` 命令。

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

此 `SHOW FIELDGROUPS` 命令返回包含表名、fieldgroupId和所有者的表。

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

閱讀本檔案後，您更了解如何使用SQL根據衍生屬性建立設定檔和啟用更新的資料集。 您現在可以透過批次擷取工作流程使用此資料集，對您的設定檔資料進行更新。 若要進一步了解將資料擷取至Adobe Experience Platform，請先閱讀 [資料擷取概觀](../../../ingestion/home.md).
