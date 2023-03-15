---
title: 在Ad Hoc資料集中設定主要身分
description: Adobe Experience Platform Query Service可讓您直接透過SQL ALTER TABLE命令，為臨機架構資料集欄位設定身分或主要身分。 該文檔說明如何使用ALTER TABLE命令來設定主標識或次標識。
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 在隨選資料集中設定主要身分

Adobe Experience Platform Query Service可讓您使用SQL的限制，將資料集欄標示為主要或次要身分 `ALTER TABLE` 命令。 您可以使用此功能，確保已標幟欄位符合資料隱私權要求。 此命令允許您直接通過SQL添加或刪除主標識表列和次標識表列的約束。

## 快速入門

將資料集欄標示為主要或次要身分識別時，必須了解 `ALTER TABLE` SQL命令，並且對資料隱私要求有很好的了解。 繼續閱讀本檔案之前，請先檢閱下列檔案：

* [適用於 `ALTER TABLE` 命令](../sql/syntax.md).
* [資料控管概觀](../../data-governance/home.md) 以取得更多資訊。

## 新增限制 {#add-constraints}

此 `ALTER TABLE` 命令允許您將資料集列標籤為人員的標識，然後使用該標籤作為主標識，方法是使用SQL更新相關元資料。 當資料集是透過SQL建立，而非直接透過Platform UI從結構建立時，這特別實用。 命令可用來確保您的Platform資料操作符合資料使用原則。

**範例**

下面的示例向現有 `t1` 表格。 的值 `id` 欄現在會標示為下方的主要身分 `IDFA` 命名空間。 身分命名空間是宣告欄位所代表身分資料類型的關鍵字。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二個範例可確保 `id` 欄標示為次要身分。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 拖放限制 {#drop-constraints}

您也可以使用 `ALTER TABLE` 命令。

**範例**

下列範例移除 `c1` 欄中標籤為現有主要標識 `t1` 表格。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，移除身分限制時會使用相同語法。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 顯示身分

使用中繼資料命令 `show identities` 從命令行介面顯示一個表，其中包含作為標識分配的每個屬性。

```shell
> show identities;
```

以下顯示返回表的示例。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

下列清單說明使用XDM時，更新現有資料集中身分識別的重要考量事項。

* 要將列指定為標識，請 **必須** 也可定義要保留為欄中繼資料的命名空間。
* XDM不支援在命名空間屬性中指定欄名稱。
* 如果您的結構使用 `identityMap` XDM欄位、根或頂層 `identityMap` 物件 **必須** 標示為身分或主要身分。
