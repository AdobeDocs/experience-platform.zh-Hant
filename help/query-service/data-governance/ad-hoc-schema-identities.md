---
title: 在即席資料集中設定主標識
description: Adobe Experience Platform查詢服務允許您通過SQL ALTER TABLE命令直接為ad hoc模式資料集欄位設定標識或主標識。 該文檔說明如何使用ALTER TABLE命令設定主標識或次標識。
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 在即席資料集中設定主標識

Adobe Experience Platform查詢服務允許您使用SQL的約束將資料集列標籤為主標識或次標識 `ALTER TABLE` 的子菜單。 您可以使用此功能確保標籤的欄位符合資料隱私要求。 此命令允許您直接通過SQL添加或刪除主標識表列和次標識表列的約束。

## 快速入門

將資料集列標籤為主標識或次標識需要瞭解 `ALTER TABLE` SQL命令和對資料隱私要求的良好理解。 在繼續本文檔之前，請查看以下文檔：

* [SQL語法指南 `ALTER TABLE` 命令](../sql/syntax.md)。
* [資料治理概述](../../data-governance/home.md) 的子菜單。

## 新增限制 {#add-constraints}

的 `ALTER TABLE` 命令允許您將資料集列標籤為個人身份，然後使用該標籤作為主要身份，方法是使用SQL更新關聯的元資料。 當通過SQL而不是通過平台UI直接從架構建立資料集時，此功能特別有用。 該命令可用於確保平台中的資料操作符合資料使用策略。

**範例**

下面的示例將約束添加到現有 `t1` 的子菜單。 的值 `id` 列現在標籤為主標識 `IDFA` 命名空間。 標識命名空間是聲明欄位所表示的標識資料類型的關鍵字。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二個示例確保 `id` 列標籤為輔助標識。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 刪除約束 {#drop-constraints}

也可以使用 `ALTER TABLE` 的子菜單。

**範例**

以下示例刪除了 `c1` 列標籤為現有 `t1` 的子菜單。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，刪除標識約束時使用的語法相同。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 顯示標識

使用元資料命令 `show identities` 命令行介面中，以顯示一個表，其中每個屬性都被指定為標識。

```shell
> show identities;
```

下面顯示了返回的表的示例。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

以下清單說明了在使用XDM時更新現有資料集中標識的重要注意事項。

* 要將列指定為標識， **必須** 還定義要保留為列元資料的命名空間。
* XDM不支援在命名空間屬性中指定列名。
* 如果架構使用 `identityMap` XDM欄位，根或頂級 `identityMap` 對象 **必須** 標籤為身份或主身份。
