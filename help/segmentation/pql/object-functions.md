---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 物件函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 5%

---


# 物件函式

[!DNL Profile Query Language] (PQL)提供的功能可簡化與物件的互動。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 為空

該函 `isNull` 數確定對象引用是否不存在。

**Format**

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

**Format**

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