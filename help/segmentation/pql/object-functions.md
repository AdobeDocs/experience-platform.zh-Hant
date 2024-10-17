---
solution: Experience Platform
title: PQL物件函式
description: Profile Query Language (PQL)提供的功能可簡化與物件的互動。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 8%

---

# 物件函式

[!DNL Profile Query Language] (PQL)提供的功能可簡化與物件的互動。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 是 Null

`isNull`函式決定物件參考是否不是布林值存在。

**格式**

```sql
{OBJECT}.isNull()
```

**範例**

以下PQL查詢會檢查個人的住家地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不是 Null

`isNotNull`函式決定物件參考是否以布林值存在。

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

現在您已瞭解物件函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
