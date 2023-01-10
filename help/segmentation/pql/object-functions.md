---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；物件函式；物件；
solution: Experience Platform
title: PQL對象函式
description: 配置檔案查詢語言(PQL)提供了一些功能，使與對象的交互更簡單。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# 物件函式

[!DNL Profile Query Language] (PQL)提供的功能使與對象的交互更簡單。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 為null

此 `isNull` 函式確定對象引用是否不存在。

**格式**

```sql
{OBJECT}.isNull()
```

**範例**

以下PQL查詢會檢查人員的家庭地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 非空

此 `isNotNull` 函式確定對象引用是否存在。

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

現在您已了解物件函式，可以在PQL查詢中使用這些函式。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
