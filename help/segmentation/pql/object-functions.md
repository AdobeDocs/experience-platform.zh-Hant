---
solution: Experience Platform
title: PQL物件函式
description: 設定檔查詢語言(PQL)提供的函式可簡化與物件的互動。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 6%

---

# 物件函式

[!DNL Profile Query Language] (PQL)提供可簡化與物件互動的函式。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 為空

此 `isNull` 函式決定物件參考是否不存在。

**格式**

```sql
{OBJECT}.isNull()
```

**範例**

以下PQL查詢會檢查個人的住家地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不是Null

此 `isNotNull` 函式決定物件參考是否存在。

**格式**

```sql
{OBJECT}.isNotNull()
```

**範例**

以下PQL查詢會檢查人員的住家地址是否存在。

```sql
person.homeAddress.isNotNull()
```

## 後續步驟

現在您已瞭解物件函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
