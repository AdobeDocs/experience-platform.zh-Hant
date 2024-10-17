---
solution: Experience Platform
title: PQL篩選器函式
description: 篩選器函式是用來篩選Profile Query Language (PQL)陣列中的資料。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 7c282594e66c8c7700471a94947448fd91596814
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---

# 篩選函式

篩選函式用於篩選[!DNL Profile Query Language] (PQL)陣列中的資料。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 篩選器

`[]` （篩選器）函式允許將篩選器套用至陣列，並傳回符合指定條件的陣列子集。 因此，此函式傳回陣列。

**格式**

```sql
{ARRAY}[filter]
```

**範例**

以下PQL查詢會取得至少有一個產品專案的SKU等於「PS」的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up運運算元

`^` (up)運運算元可讓您參照上層篩選中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 篩選的外層。 |
| `{FILTER_2}` | 篩選的內部圖層 |
| `^{PROPERTY}` | 也正在篩選的屬性。 由於`^`，它正在根據filter1檢查屬性。 |

**範例**

下列PQL查詢取得至少有一個產品專案的SKU等於「PS」**或**&#x200B;具有性別為女性之人員的所有事件。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已瞭解篩選函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
