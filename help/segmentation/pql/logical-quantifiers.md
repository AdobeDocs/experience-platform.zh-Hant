---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置式查詢語言；邏輯量詞；邏輯量詞；
solution: Experience Platform
title: PQL邏輯量詞
description: 邏輯量詞可用於在配置檔案查詢語言(PQL)中用陣列來斷言條件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# 邏輯量詞函式

邏輯量詞可用於在中用陣列斷言條件 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 存在

的 `exists` 函式確定在滿足所提供條件的情況下，在陣列中存在項。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 返回的可選表達式，用於篩選陣列中的值。 |

**範例**

以下PQL查詢將獲取價格超過$50或SKU為「PS」的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 全民

的 `forall` 函式確定陣列中滿足所有給定條件的所有項。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 返回的可選表達式，用於篩選陣列中的值。 |

**範例**

以下PQL查詢將獲取價格超過$50且SKU為「PS」的所有事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 後續步驟

現在您已經瞭解了邏輯量詞，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
