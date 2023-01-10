---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；篩選功能；篩選；
solution: Experience Platform
title: PQL篩選器功能
description: 篩選函式可用來篩選設定檔查詢語言(PQL)中的陣列內的資料。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 篩選函式

篩選函式可用來篩選 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 篩選

此 `[]` (filter)函式允許將篩選器應用於陣列，並返回與指定條件匹配的陣列的子集。

**格式**

```sql
{ARRAY}[filter]
```

**範例**

以下PQL查詢將獲取至少包含一個產品項且SKU等於「PS」的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上運算子

此 `^` (up)運算子可讓您參照上層篩選器中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 過濾的外層。 |
| `{FILTER_2}` | 過濾的內層 |
| `^{PROPERTY}` | 也正在篩選的屬性。 由於 `^`，則會根據filter1檢查屬性。 |

**範例**

以下PQL查詢將獲取至少包含一個產品項且SKU等於「PS」的所有事件 **或** 有一個性別為女性的人。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已了解篩選功能，可以在PQL查詢中使用這些功能。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
