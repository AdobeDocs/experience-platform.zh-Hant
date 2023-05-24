---
title: 查詢服務中資料資產組織的最佳做法
description: 本文檔概述了組織資料以便於查詢服務使用的邏輯方法。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 在查詢服務中組織資料資產

本文檔提供了關於組織資料資產（包括資料集、視圖和臨時表）的最佳做法的指導，以便與Adobe Experience Platform查詢服務一起使用。 它包括如何構造資料以及如何訪問、更新和刪除此資訊的資訊。

在平台內按邏輯組織資料資產非常重要 [!DNL Data Lake] 隨著它們的生長。 查詢服務擴展了SQL結構，使您可以在沙箱中對資料資產進行邏輯分組。 這種組織方法允許在架構之間共用資料資產，而無需物理地移動它們。

## 快速入門

在繼續本文檔之前，您應對 [查詢服務](../home.md) 功能並已閱讀 [用戶介面指南](../ui/user-guide.md)。

## 在查詢服務中組織資料

以下示例演示了通過Adobe Experience Platform查詢服務可用於使用標準SQL語法對資料進行邏輯組織的結構。 您應首先建立一個資料庫，作為資料點的容器。 資料庫可以包含一個或多個模式，然後每個模式都可以有一個或多個對資料資產（資料集、視圖、臨時表等）的引用。 這些引用包括資料集之間的任何關係或關聯。

查看 [查詢編輯器使用手冊](../ui/user-guide.md) 有關如何使用查詢服務UI建立SQL查詢的詳細指導。

支援以下SQL結構以邏輯地組織沙箱中的資料集。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

示例（為簡單起見，稍作截斷）演示了此方法 `databaseA` 包含架構 `schema1`。

## 將資料資產與架構關聯

建立模式以用作資料資產的容器後，每個資料集都可以使用標準SQL ALTER TABLE語法與資料庫中的一個或多個模式相關聯。

下面的示例添加 `dataset1`。 `dataset2`。 `dataset3` 和 `v1` 到 `databaseA.schema1` 在上例中建立的容器。

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## 從資料容器訪問資料資產

通過適當限定資料庫名稱， [!DNL PostgreSQL] 客戶端可以連接到您使用SHOW關鍵字建立的任何資料結構。 有關SHOW關鍵字的詳細資訊，請參閱 [SQL語法文檔中的SHOW節](../sql/syntax.md#show)。

「all」是預設的資料庫名稱，其中包含沙盒中的每個資料庫和架構容器。 當你做 [!DNL PostgreSQL] 連接使用 `dbname="all"`，您可以 **任何** 建立的資料庫和架構，以邏輯地組織資料。

列出所有資料庫 `dbname="all"` 顯示三個可用資料庫。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

列出所有架構 `dbname="all"` 顯示與沙箱中每個資料庫相關的三個架構。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

當你做 [!DNL PostgreSQL] 連接使用 `dbname="databaseA"`，可以訪問與該特定資料庫關聯的任何架構，如下例所示。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

使用點表示法可以訪問與連接到所選資料庫的特定架構關聯的每個表。 通過連接到 `DBNAME = databaseA.schema1;`，所有與特定架構關聯的表(`schema1`)。 這提供了哪些資料集包含哪個表的資訊。

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## 從資料容器更新或刪除資料資產

隨著組織（或沙盒）中的資料資產量的增長，有必要更新或刪除資料容器中的資料資產。 通過使用點符號引用適當的資料庫和架構名稱，可以從組織容器中刪除單個資產。 表和視圖(`t1` 和 `v1` 分別) `databaseA.schema1` 在第一個示例中，使用以下示例中的語法刪除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 刪除資料資產

的 [刪除表](../sql/syntax.md#drop-table) 函式僅從物理上刪除資料資產 [!DNL Data Lake] 當組織中所有資料庫都存在對表的單個引用時。

```sql
DROP TABLE databaseA.schema2.t1;
```

### 刪除資料資產容器

還可以使用標準SQL函式刪除資料庫和模式。

#### 刪除資料庫

如果對與資料庫關聯的資料資產有其他引用，則函式在嘗試刪除資料庫時將引發錯誤。

```sql
DROP DATABASE databaseA;
```

#### 刪除架構

刪除架構時需要注意三個重要注意事項：

- 刪除架構不會實際刪除任何資料資產，如表、視圖或臨時表。
- 如果目標架構中引用了任何資料資產，且模式為RESTRICT，則會引發異常。
- 如果目標架構中引用了任何資料資產，且該模式為CASCADE，則系統將刪除該架構容器引用的所有資料資產，然後刪除該架構容器。

```sql
DROP SCHEMA databaseA.schema2;
```

## 後續步驟

通過閱讀本文檔，您現在可以更好地瞭解與Adobe Experience Platform查詢服務一起使用的資料資產的組織和結構方面的最佳做法。 建議通過閱讀有關 [重複資料消除文檔](../essential-concepts/deduplication.md)。
