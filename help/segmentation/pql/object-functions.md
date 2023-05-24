---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置檔案查詢語言；對象函式；對象；
solution: Experience Platform
title: PQL對象函式
description: 配置檔案查詢語言(PQL)提供使與對象交互更簡單的功能。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# 物件函式

[!DNL Profile Query Language] (PQL)提供使與對象交互更簡單的函式。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 為空

的 `isNull` 函式確定對象引用是否不存在。

**格式**

```sql
{OBJECT}.isNull()
```

**範例**

以下PQL查詢檢查人員的住宅地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不為空

的 `isNotNull` 函式確定是否存在對象引用。

**格式**

```sql
{OBJECT}.isNotNull()
```

**範例**

以下PQL查詢檢查人員的住宅地址是否存在。

```sql
person.homeAddress.isNotNull()
```

## 後續步驟

現在您已經瞭解了對象函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
