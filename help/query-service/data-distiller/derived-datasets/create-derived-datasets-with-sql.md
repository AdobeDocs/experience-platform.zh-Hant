---
title: 使用SQL建立衍生資料集
description: 瞭解如何使用SQL建立為設定檔啟用的衍生資料集，以及如何將資料集用於即時客戶設定檔和分段服務。
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# 使用SQL建立衍生資料集

瞭解如何使用SQL查詢來操縱和轉換現有資料集的資料，以建立為設定檔啟用的衍生資料集。 此工作流程提供高效率的替代方法，可以為您的Real-time Customer Profile業務使用案例建立衍生資料集。

本檔案概述各種方便使用的SQL擴充功能，這些擴充功能會產生衍生的資料集，以與即時客戶設定檔搭配使用。 工作流程簡化了您原本必須透過各種API呼叫或Experience Platform UI互動完成的程式。

一般來說，產生和發佈即時客戶個人檔案的衍生資料集會涉及以下步驟：

* 建立身分名稱空間（如果尚未存在）。
* 如有必要，請建立資料型別以儲存衍生的資料集。
* 使用該資料型別建立欄位群組以儲存衍生的資料集資訊。
* 使用先前建立的名稱空間建立或指派主要身分資料行。
* 使用先前建立的欄位群組和資料型別建立結構描述。
* 使用您的結構描述建立新資料集，並視需要為設定檔啟用它。
* 可選擇將資料集標示為已啟用設定檔。

完成上述步驟後，您就可以填入資料集了。 如果您為設定檔啟用資料集，也可以建立區段來參照新資料集並開始產生深入分析。

「查詢服務」可讓您使用SQL查詢來執行上述所有動作。 這包括在必要時變更資料集和欄位群組。

## 建立表格，並選取為設定檔啟用該表格的選項 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查詢假設使用預先存在的名稱空間。

使用「建立表格為選取」(CTAS)查詢來建立資料集、指派資料型別、設定主要身分、建立結構描述，並標籤為已啟用設定檔。 以下範例SQL陳述式會建立資料集，並供Real-Time Customer Data Platform (Real-Time CDP)使用。 您的SQL查詢將遵循以下範例中顯示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

支援的資料型別為：布林值、日期、日期時間、文字、浮點數、bigint、整數、對應、陣列和結構/列。

下方的SQl程式碼區塊提供範例，可定義結構/列、對應和陣列資料型別。 第一行示範列語法。 第二行示範對應語法，第三行示範陣列語法。

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

或者，也可以透過Experience Platform UI為設定檔啟用資料集。 如需將資料集標示為已啟用設定檔的詳細資訊，請參閱[啟用即時客戶設定檔的資料集檔案](../../../catalog/datasets/user-guide.md#enable-profile)。

在下列範例查詢中，`decile_table`資料集是以`id`作為主要身分資料行建立，且名稱空間為`IDFA`。 它也有對應資料型別名為`decile1Month`的欄位。 已針對設定檔啟用建立的資料表(`decile_table`)。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

成功執行查詢時，資料集ID會傳回至主控台，如下列範例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

在`CREATE TABLE`命令上使用`label='PROFILE'`來建立啟用設定檔的資料集。 `upsert`功能預設為開啟。 可以使用`ALTER`命令覆寫`upsert`功能，如下列範例所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

請參閱SQl語法檔案，以取得有關使用[ALTER TABLE](../../sql/syntax.md#alter-table)命令和[標籤作為CTAS查詢](../../sql/syntax.md#create-table-as-select)一部分的詳細資訊。

## 協助透過SQL管理衍生資料集的建構

透過SQL管理衍生資料集時，以下說明的功能非常有用。

### 變更要為設定檔啟用的現有資料集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL建構可用來讓現有的資料集為設定檔啟用。 需要同時在結構描述和對應的資料集中新增啟用設定檔的標籤。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>成功執行`ALTER TABLE`命令時，主控台會傳回`ALTER SUCCESS`。

### 將主要身分新增至現有資料集 {#add-primary-identity}

將資料集中的現有欄標示為主要身分集，否則會導致錯誤。 若要使用SQL設定主要身分，請使用下面顯示的查詢格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的範例中，`id2`是`test1_dataset`中的現有資料行。

### 停用設定檔的資料集 {#disable-dataset-for-profile}

如果您要針對設定檔用途停用表格，則必須使用DROP指令。 以下是使用`DROP`的範例SQL陳述式。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL陳述式提供使用API呼叫的有效替代方法。 如需詳細資訊，請參閱檔案，瞭解如何[使用資料集API](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile)停用資料集以搭配Real-Time CDP使用。

### 允許更新資料集並為其插入功能 {#enable-upsert-functionality-for-dataset}

UPSERT指令可讓您插入新記錄或更新表格中的現有資料。 具體來說，如果表格中已存在指定的值，它可讓您更新現有的列，或者如果指定的值尚未存在，則可插入新列。

以下是使用正確格式的範例陳述式。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL陳述式提供使用API呼叫的有效替代方法。 如需詳細資訊，請參閱檔案，瞭解如何[使用資料集API](../../../catalog/datasets/enable-upsert.md#enable-the-dataset)啟用資料集以搭配Real-Time CDP和UPSERT使用。

### 停用資料集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

這個命令會停用更新資料集並將資料列插入資料集中的功能。

以下是使用正確格式的範例陳述式。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 顯示與每個表格關聯的其他表格資訊 {#show-labels-for-tables}

為啟用設定檔的資料集保留其他中繼資料。 使用`SHOW TABLES`命令來顯示額外的`labels`欄，該欄提供與資料表關聯的任何標籤的資訊。

此命令的輸出範例如下所示：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

您可從範例中看出`table_with_a_decile`已為設定檔啟用，並套用標籤，例如[&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset)，[&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) （如先前所述）。

### 使用SQL建立欄位群組

現在可以透過使用SQL來建立欄位群組。 這是在Experience Platform UI中使用結構描述編輯器，或向結構描述登入進行API呼叫的替代方式。

下面顯示建立欄位群組的範例陳述式。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>如果陳述式中未提供`label`旗標，或欄位群組已存在，則透過SQL建立欄位群組將會失敗。
>請確定查詢包含`IF NOT EXISTS`子句，以避免查詢失敗，因為欄位群組已經存在。

真實世界的範例看起來可能類似於下面所示的範例。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功執行此陳述式會傳回建立的欄位群組ID。 例如 `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

如需其他方法的詳細資訊，請參閱檔案，瞭解如何在結構描述編輯器[&#128279;](../../../xdm/ui/resources/field-groups.md#create)中建立新欄位群組[結構描述登入API](../../../xdm/api/field-groups.md#create)。

### 放置欄位群組

有時可能需要從結構描述登入中移除欄位群組。 這是透過使用欄位群組識別碼執行`DROP FIELDGROUP`命令來完成。

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

例如：

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>如果欄位群組不存在，透過SQL刪除欄位群組將會失敗。 請確定陳述式包含`IF EXISTS`子句，以避免查詢失敗。

### 顯示表格的所有欄位群組名稱和ID

`SHOW FIELDGROUPS`命令會傳回包含資料表名稱、fieldgroupId和擁有者的資料表。

此命令的輸出範例如下所示：

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

閱讀本檔案後，您對於如何使用SQL建立設定檔及根據衍生資料集啟用更新插入的資料集有了更深入的瞭解。 您現在已準備好將此資料集與批次擷取工作流程搭配使用，以更新您的設定檔資料。 若要進一步瞭解如何將資料擷取至Adobe Experience Platform，請先閱讀[資料擷取概觀](../../../ingestion/home.md)。
