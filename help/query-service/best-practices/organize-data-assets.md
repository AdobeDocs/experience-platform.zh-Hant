---
title: 查詢服務中資料資產組織的最佳實務
description: 本檔案概述組織資料以方便與Query Service搭配使用的邏輯方法。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 在Query Service中組織資料資產

本檔案提供組織資料資產（包括資料集、檢視和臨時表格）的最佳實務指引，以便與Adobe Experience Platform Query Service搭配使用。 它涵蓋如何建構您的資料，以及如何存取、更新和刪除此資訊的資訊。

在Platform中以邏輯方式組織資料資產非常重要 [!DNL Data Lake] 隨著它們的生長。 查詢服務擴展了SQL結構，使您能夠在沙箱中以邏輯方式對資料資產進行分組。 此組織方法可讓您在結構之間共用資料資產，而無須實際移動。

## 快速入門

在繼續使用本檔案之前，您應該對 [查詢服務](../home.md) 功能並已閱讀 [使用者介面指南](../ui/user-guide.md).

## 在查詢服務中組織資料

下列範例示範可透過Adobe Experience Platform Query Service來使用標準SQL語法以邏輯方式組織資料的建構。 首先，您應建立資料庫，作為資料點的容器。 資料庫可以包含一或多個結構，然後每個結構都可以有一或多個資料資產的參考（資料集、檢視、臨時表格等）。 這些參考包含資料集之間的任何關係或關聯。

請參閱 [查詢編輯器使用手冊](../ui/user-guide.md) 有關如何使用查詢服務UI建立SQL查詢的詳細指導。

支援下列SQL結構，以邏輯方式組織沙箱中的資料集。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

範例（稍微截斷簡短）示範此方法，其中 `databaseA` 包含綱要 `schema1`.

## 將資料資產與結構關聯

建立架構以充當資料資產的容器後，每個資料集都可以使用標準SQL ALTER TABLE語法與資料庫中的一個或多個架構相關聯。

下列範例新增 `dataset1`, `dataset2`, `dataset3` 和 `v1` 到 `databaseA.schema1` 容器。

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## 從資料容器存取資料資產

通過適當地限定資料庫名稱， [!DNL PostgreSQL] 客戶端可以連接到您使用SHOW關鍵字建立的任何資料結構。 有關SHOW關鍵字的更多資訊，請參閱 [SQL語法文檔中的SHOW節](../sql/syntax.md#show).

「all」是預設的資料庫名稱，其中包含沙箱中的每個資料庫和架構容器。 當您 [!DNL PostgreSQL] 連接使用 `dbname="all"`，您可以 **any** 您為邏輯組織資料而建立的資料庫和架構。

列出 `dbname="all"` 顯示三個可用的資料庫。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

列出 `dbname="all"` 顯示與沙箱中每個資料庫相關的三個結構。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

當您 [!DNL PostgreSQL] 連接使用 `dbname="databaseA"`，您可以存取與該特定資料庫相關聯的任何架構，如下列範例所示。

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

點標籤法可讓您存取與連接到您所選資料庫的特定架構相關聯的每個表格。 通過連接到 `DBNAME = databaseA.schema1;`，與該特定架構關聯的所有表(`schema1`)。 如此可提供資料集包含哪些表格的資訊。

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

## 更新或移除資料容器中的資料資產

隨著組織（或沙箱）中的資料資產量增加，您就必須更新或移除資料容器中的資料資產。 使用點記號參考適當的資料庫和結構名稱，即可從組織容器中移除個別資產。 表格和檢視(`t1` 和 `v1` ) `databaseA.schema1` 在第一個範例中，會使用下列範例中的語法來移除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 移除資料資產

此 [拖放表](../sql/syntax.md#drop-table) 函式只會以物理方式從 [!DNL Data Lake] 當組織中所有資料庫中都存在對表的單個引用時。

```sql
DROP TABLE databaseA.schema2.t1;
```

### 移除資料資產容器

也可以使用標準SQL函式刪除資料庫和架構。

#### 刪除資料庫

如果對與資料庫相關聯的資料資產有其他引用，則函式在嘗試刪除資料庫時將引發錯誤。

```sql
DROP DATABASE databaseA;
```

#### 移除架構

移除結構時，請注意三個重要事項：

- 移除結構並不會實際刪除任何資料資產，例如表格、檢視或臨時表格。
- 如果目標架構中參考了任何資料資產，且模式為RESTRICT，則會擲回例外狀況。
- 如果目標架構中引用了任何資料資產，且模式為CASCADE，則系統會刪除架構容器引用的所有資料資產，然後刪除架構容器。

```sql
DROP SCHEMA databaseA.schema2;
```

## 後續步驟

閱讀本檔案後，您現在更能了解與Adobe Experience Platform Query Service搭配使用之資料資產的組織與結構相關最佳實務。 建議您透過閱讀 [資料重複資料刪除檔案](../essential-concepts/deduplication.md).
