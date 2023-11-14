---
title: 查詢服務中資料資產組織的最佳實務
description: 本檔案概述整理資料的邏輯方法，以方便使用查詢服務。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 6e2be299e3c1c0dfa2832ead22cdeaea0ca83591
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 在查詢服務中組織資料資產

本檔案提供整理資料資產的最佳實務指引，包括搭配Adobe Experience Platform查詢服務使用的資料集、檢視和暫時表格。 其中涵蓋如何建構您的資料，以及如何存取、更新和刪除此資訊的資訊。

在Platform內以邏輯方式組織資料資產很重要 [!DNL Data Lake] 隨著客戶成長。 Query Service可擴充SQL建構，讓您在邏輯上將資料資產分組在沙箱中。 這種組織方法允許在結構描述之間共用資料資產，而不需要實際移動它們。

## 快速入門

在繼續閱讀本檔案之前，您應該已充分瞭解 [查詢服務](../home.md) 功能並已閱讀 [使用者介面指南](../ui/user-guide.md).

## 在查詢服務中組織資料

下列範例示範您可以透過Adobe Experience Platform Query Service使用的建構，以使用標準SQL語法在邏輯上組織您的資料。 您應該先建立資料庫，以作為資料點的容器。 資料庫可以包含一或多個結構描述，而每個結構描述都可以有一或多個資料資產（資料集、檢視、暫存表格等）的參考。 這些參考資料包括資料集之間的任何關係或關聯。

請參閱 [查詢編輯器使用手冊](../ui/user-guide.md) 以取得有關如何使用查詢服務UI來建立SQL查詢的詳細指引。

支援下列SQL建構，以邏輯方式在沙箱中組織資料集。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

此範例（為簡短起見，稍微截斷了一下）示範此方法，其中 `databaseA` 包含結構描述 `schema1`.

## 將資料資產與結構描述建立關聯

建立結構描述以做為資料資產的容器後，每個資料集都可以使用標準SQL ALTER TABLE語法，與資料庫中的一或多個結構描述建立關聯。

下列範例新增 `dataset1`， `dataset2`， `dataset3` 和 `v1` 至 `databaseA.schema1` 容器建立在上一個範例中。

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## 從資料容器存取資料資產

適當地確認資料庫名稱，任何 [!DNL PostgreSQL] 使用者端可以使用SHOW關鍵字連線到您建立的任何資料結構。 如需SHOW關鍵字的詳細資訊，請參閱 [SQL語法檔案中的SHOW區段](../sql/syntax.md#show).

「all」是預設的資料庫名稱，其中包含沙箱中的每個資料庫和結構描述容器。 當您建立 [!DNL PostgreSQL] 連線使用 `dbname="all"`，您可以存取 **任何** 您用來以邏輯方式組織資料的資料庫和綱要。

列出所有資料庫於 `dbname="all"` 顯示三個可用的資料庫。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

列出下的所有結構描述 `dbname="all"` 顯示與沙箱中每個資料庫相關的三個結構描述。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

當您建立 [!DNL PostgreSQL] 連線使用 `dbname="databaseA"`，您可以存取與該特定資料庫相關聯的任何結構描述，如以下範例所示。

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

點標籤法可讓您存取與特定結構描述相關聯的每個表格，這些結構描述已連線至您選擇的資料庫。 透過連線到 `DBNAME = databaseA.schema1;`，所有與該特定結構描述關聯的表格(`schema1`)中顯示。 這會提供有關哪個資料集包含哪個表格的資訊。

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

## 從資料容器更新或移除資料資產

隨著您組織（或沙箱）中的資料資產量增加，有必要從資料容器更新或移除資料資產。 透過使用點標籤法參考適當的資料庫和結構描述名稱，可以從組織容器中移除個別資產。 表格和檢視(`t1` 和 `v1` 分別)新增至 `databaseA.schema1` 在第一個範例中，會使用下列範例中的語法來移除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 移除資料資產

此 [放置表格](../sql/syntax.md#drop-table) 函式只會從實體上移除資料資產 [!DNL Data Lake] 當對表格的單一參考存在於組織中的所有資料庫中時。

```sql
DROP TABLE databaseA.schema2.t1;
```

### 移除資料資產容器

也可以使用標準SQL函式來移除資料庫和結構描述。

#### 移除資料庫

如果有其他與資料庫相關聯的資料資產參考，函式在嘗試移除資料庫時將擲回錯誤。

```sql
DROP DATABASE databaseA;
```

#### 移除結構描述

移除結構時，有三個重要的考量事項需要注意：

- 移除結構描述並不會實際刪除任何資料資產，例如表格、檢視表或暫時表格。
- 如果目標結構描述中有參考的任何資料資產，且模式為RESTRICT，則會擲回例外狀況。
- 如果目標結構描述中有參考的任何資料資產，且模式為CASCADE，則系統會移除結構描述容器參考的所有資料資產，然後刪除結構描述容器。

```sql
DROP SCHEMA databaseA.schema2;
```

## 後續步驟

閱讀本檔案後，您現在就能更妥善地瞭解搭配Adobe Experience Platform查詢服務使用之資料資產的組織和結構相關最佳實務。 建議您閱讀關於，以繼續瞭解查詢服務的最佳實務 [重複資料刪除檔案](../essential-concepts/deduplication.md).
