---
keywords: Experience Platform；主題；熱門主題；分段；分段；分段服務；PQL;PQL；配置檔案查詢語言；過濾功能；過濾器；
solution: Experience Platform
title: PQL篩選器函式
description: 篩選器函式用於篩選配置檔案查詢語言(PQL)中陣列內的資料。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 篩選器函式

篩選函式用於篩選中的陣列內的資料 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 篩選

的 `[]` (filter)函式允許將篩選器應用於陣列並返回與指定條件匹配的陣列子集。

**格式**

```sql
{ARRAY}[filter]
```

**範例**

以下PQL查詢將獲取至少包含一個SKU等於「PS」的產品項的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 上運算子

的 `^` (up)運算子允許您引用篩選器上級中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 過濾的外層。 |
| `{FILTER_2}` | 過濾的內層 |
| `^{PROPERTY}` | 正在篩選的屬性。 由於 `^`，它正在檢查基於filter1的屬性。 |

**範例**

以下PQL查詢將獲取至少包含一個SKU等於「PS」的產品項的所有事件 **或** 有一個性別為女性的人。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已經瞭解了篩選器函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
