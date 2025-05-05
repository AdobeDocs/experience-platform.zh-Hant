---
title: 查詢服務中資料資產組織的最佳實務
description: 本檔案概述整理資料的邏輯方法，以方便使用查詢服務。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# 在查詢服務中組織資料資產

本檔案提供整理資料資產的最佳實務指引，包括搭配Adobe Experience Platform查詢服務使用的資料集、檢視和暫時表格。 其中涵蓋如何建構您的資料，以及如何存取、更新和刪除此資訊的資訊。

隨著資料資產的成長，在Experience Platform [!DNL Data Lake]中以邏輯方式組織這些資產非常重要。 Query Service可擴充SQL建構，讓您在邏輯上將資料資產分組在沙箱中。 這種組織方法允許在結構描述之間共用資料資產，而不需要實際移動它們。

## 快速入門

在繼續此檔案之前，您應該已經對[查詢服務](../home.md)功能有了充分的瞭解，並且已經閱讀了[使用者介面指南](../ui/user-guide.md)。

## 在查詢服務中組織資料

下列範例示範您可以透過Adobe Experience Platform Query Service使用的建構，以使用標準SQL語法在邏輯上組織您的資料。 您應該先建立資料庫，以作為資料點的容器。 資料庫可以包含一或多個結構描述，而每個結構描述都可以有一或多個資料資產（資料集、檢視、暫存表格等）的參考。 這些參考資料包括資料集之間的任何關係或關聯。

請參閱[查詢編輯器使用手冊](../ui/user-guide.md)，以取得有關如何使用查詢服務UI來建立SQL查詢的詳細指引。

支援下列SQL建構，以邏輯方式在沙箱中組織資料集。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

此範例（為簡短起見，略為截斷）示範這個方法，其中`databaseA`包含結構描述`schema1`。

## 將資料資產與結構描述建立關聯

建立結構描述以做為資料資產的容器後，每個資料集都可以使用標準SQL ALTER TABLE語法，與資料庫中的一或多個結構描述建立關聯。

下列範例將`dataset1`、`dataset2`、`dataset3`和`v1`新增至上一個範例中建立的`databaseA.schema1`容器。

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## 從資料容器存取資料資產

只要適當地限定資料庫名稱，任何[!DNL PostgreSQL]使用者端都可以連線到您使用SHOW關鍵字建立的任何資料結構。 如需有關SHOW關鍵字的詳細資訊，請參閱SQL語法檔案[&#128279;](../sql/syntax.md#show)中的SHOW區段。

「all」是預設的資料庫名稱，其中包含沙箱中的每個資料庫和結構描述容器。 當您使用`dbname="all"`建立[!DNL PostgreSQL]連線時，可以存取您已建立的&#x200B;**任何**&#x200B;資料庫和結構描述，以邏輯方式組織您的資料。

列出`dbname="all"`下的所有資料庫，會顯示三個可用的資料庫。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

列出`dbname="all"`下的所有結構描述，會顯示與沙箱中每個資料庫相關的三個結構描述。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

當您使用`dbname="databaseA"`建立[!DNL PostgreSQL]連線時，您可以存取與該特定資料庫相關聯的任何結構描述，如下列範例所示。

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

點標籤法可讓您存取與特定結構描述相關聯的每個表格，這些結構描述已連線至您選擇的資料庫。 透過連線到`DBNAME = databaseA.schema1;`，會顯示與該特定結構描述(`schema1`)相關聯的所有資料表。 這會提供有關哪個資料集包含哪個表格的資訊。

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

隨著您組織（或沙箱）中的資料資產量增加，有必要從資料容器更新或移除資料資產。 透過使用點標籤法參考適當的資料庫和結構描述名稱，可以從組織容器中移除個別資產。 第一個範例中新增至`databaseA.schema1`的資料表和檢視（`t1`和`v1`），會使用下列範例中的語法移除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 移除資料資產

[DROP TABLE](../sql/syntax.md#drop-table)函式只會在您組織的所有資料庫中存在資料表的單一參考時，從[!DNL Data Lake]實際移除資料資產。

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

閱讀本檔案後，您現在就能更妥善地瞭解搭配Adobe Experience Platform查詢服務使用之資料資產的組織和結構相關最佳實務。 建議您閱讀約[重複資料刪除檔案](../key-concepts/deduplication.md)，繼續瞭解查詢服務的最佳實務。
