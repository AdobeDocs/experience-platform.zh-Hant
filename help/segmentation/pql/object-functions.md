---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 物件函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 物件函式

描述檔查詢語言(PQL)提供多種功能，讓與物件的互動更簡單。 有關其他PQL函式的詳細資訊，請參閱「配置檔案查 [詢語言」概述](./overview.md)。

## 為空

該函 `isNull` 數確定對象引用是否不存在。

**格式**

```sql
{OBJECT}.isNull()
```

**範例**

以下PQL查詢會檢查人員的家庭地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 非空值

該函 `isNotNull` 數確定是否存在對象引用。

**格式**

```sql
{OBJECT}.isNotNull()
```

**範例**

以下PQL查詢會檢查人員的家庭地址是否存在。

```sql
person.homeAddress.isNotNull()
```

## 後續步驟

現在您已經瞭解了對象函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。