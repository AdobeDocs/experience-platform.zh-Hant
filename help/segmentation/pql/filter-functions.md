---
solution: Experience Platform
title: PQL篩選函式
description: 篩選函式是用來篩選設定檔查詢語言(PQL)陣列中的資料。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 4%

---

# 篩選函式

篩選函式是用來篩選陣列中的資料，在 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 篩選

此 `[]` （篩選）函式可將篩選套用至陣列，並傳回符合指定條件的陣列子集。

**格式**

```sql
{ARRAY}[filter]
```

**範例**

以下PQL查詢會取得至少一個產品專案的SKU等於「PS」的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up運運算元

此 `^` (up)運運算元可讓您參照上層篩選中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 篩選的外層。 |
| `{FILTER_2}` | 篩選的內部圖層 |
| `^{PROPERTY}` | 也正在篩選的屬性。 由於 `^`，則會根據filter1檢查屬性。 |

**範例**

以下PQL查詢會取得至少一個產品專案的SKU等於「PS」的所有事件 **或** 有一個性別為女性的人。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已瞭解篩選函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
