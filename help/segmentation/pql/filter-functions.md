---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；過濾功能；過濾；
solution: Experience Platform
title: PQL過濾器函式
topic-legacy: developer guide
description: 篩選函式用於篩選描述檔查詢語言(PQL)中陣列內的資料。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 濾鏡函式

篩選函式用於篩選[!DNL Profile Query Language](PQL)中陣列內的資料。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 篩選

`[]`(filter)函式允許將過濾器應用於陣列並返回與指定條件匹配的陣列子集。

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

`^`(up)運算子可讓您參照上層篩選器中的屬性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 引數 | 說明 |
| -------- | ----------- |
| `{ARRAY}` | 正在篩選的陣列。 |
| `{FILTER_1}` | 過濾的外層。 |
| `{FILTER_2}` | 過濾的內層 |
| `^{PROPERTY}` | 也正在篩選的屬性。 由於`^`，它正在基於filter1檢查屬性。 |

**範例**

以下PQL查詢獲取至少具有一個SKU等於「PS」 **或**&#x200B;的產品項目且性別為女性的所有事件。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 後續步驟

現在您已經瞭解過濾器函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
