---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；對象函式；對象；
solution: Experience Platform
title: PQL對象函式
topic: developer guide
description: 描述檔查詢語言(PQL)提供多種功能，讓與物件的互動更簡單。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---


# 物件函式

[!DNL Profile Query Language] (PQL)提供的功能可簡化與物件的互動。有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 為空

`isNull`函式確定對象引用是否不存在。

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

`isNotNull`函式確定是否存在對象引用。

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

現在您已經瞭解了對象函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。