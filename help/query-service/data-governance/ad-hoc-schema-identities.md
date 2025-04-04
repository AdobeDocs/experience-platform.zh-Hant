---
title: 在臨時資料集中設定主要身分
description: Adobe Experience Platform查詢服務可讓您直接透過SQL ALTER TABLE命令，為臨機操作結構描述資料集欄位設定身分或主要身分。 本檔案說明如何使用ALTER TABLE指令來設定主要身分或次要身分。
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 在臨時資料集中設定主要身分

Adobe Experience Platform查詢服務可讓您使用SQL `ALTER TABLE`命令的限制將資料集資料行標示為主要或次要身分。 您可以使用此功能來確保標幟的欄位符合資料隱私權要求。 這個命令可讓您直接透過SQL新增或刪除主要和次要識別表格資料行的限制。

## 快速入門

若要將資料集資料行標示為主要或次要身分，必須瞭解`ALTER TABLE` SQL命令，並充分瞭解資料隱私權需求。 在繼續本檔案之前，請先檢閱下列檔案：

* [ `ALTER TABLE`命令的SQL語法指南](../sql/syntax.md)。
* [資料控管概觀](../../data-governance/home.md)以取得詳細資訊。

## 新增限制 {#add-constraints}

`ALTER TABLE`命令可讓您將資料集資料行標示為人員身分，然後使用SQL更新關聯的中繼資料，將該標籤作為主要身分使用。 若資料集是透過SQL建立，而非直接透過Experience Platform UI從結構描述建立，此方法會特別實用。 命令可用來確保您在Experience Platform中的資料作業符合資料使用原則。

**範例**

下列範例將限制新增至現有的`t1`資料表。 `id`資料行的值現在標籤為`IDFA`名稱空間下的主要身分。 身分名稱空間是關鍵字，可宣告欄位代表的身分資料型別。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二個範例可確保將`id`資料行標示為次要身分。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 卸除限制 {#drop-constraints}

也可以使用`ALTER TABLE`命令從資料表資料行移除限制。

**範例**

下列範例移除在現有`t1`資料表中必須將`c1`資料行標示為主要身分的要求。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，移除身分限制時，會使用相同的語法。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 顯示身分

使用命令列介面中的中繼資料命令`show identities`顯示具有指派為身分識別的每個屬性的表格。

```shell
> show identities;
```

以下顯示傳回表格的範例。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

以下清單說明使用XDM時更新現有資料集中的身分的重要考量事項。

* 若要將資料行指定為身分，您&#x200B;**必須**&#x200B;同時定義要保留為資料行中繼資料的名稱空間。
* XDM不支援在名稱空間屬性中指定欄名稱。
* 如果您的結構描述使用`identityMap` XDM欄位，根或頂層`identityMap`物件&#x200B;**必須**&#x200B;標示為身分或主要身分。
