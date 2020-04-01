---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 濾鏡函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 濾鏡函式

篩選函式用於篩選描述檔查詢語言(PQL)中陣列內的資料。 有關其他PQL函式的詳細資訊，請參閱「配置檔案查 [詢語言」概述](./overview.md)。

## 篩選

該 `[]` （過濾器）函式允許將過濾器應用於陣列並返回與指定條件匹配的陣列的子集。

**格式**

```sql
{ARRAY}[filter]
```

**範例**

以下PQL查詢將獲取至少包含一個產品項目（SKU等於「PS」）的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上運算子

( `^` up)運算子可讓您參考上層篩選器中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 過濾的外層。 |
| `{FILTER_2}` | 過濾的內層 |
| `^{PROPERTY}` | 也正在篩選的屬性。 由於 `^`，它正在基於filter1檢查屬性。 |

**範例**

下列PQL查詢會取得至少有一個SKU等於「PS」或 **** 「性別為女性」的產品項目的所有事件。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已經瞭解過濾器函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
