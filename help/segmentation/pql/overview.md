---
solution: Experience Platform
title: 設定檔查詢語言(PQL)概觀
description: 本指南提供PQL的一般概觀，涵蓋格式化准則並提供範例PQL運算式。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# [!DNL Profile Query Language] (PQL)概觀

[!DNL Profile Query Language] (PQL)是 [!DNL Experience Data Model] 符合(XDM)規範的查詢語言，用於支援細分查詢的定義和執行 [!DNL Real-Time Customer Profile] 資料。

本指南提供PQL的一般概觀，涵蓋格式化准則並提供範例PQL運算式。

## PQL查詢格式

PQL查詢具有下列簽章：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

輸入引數可以是簡單基本值（例如布林值或字串），或是更複雜的型別（例如物件、陣列或對應）。

有三種不同的方式可參照PQL運算式內文中的輸入引數：

### 第一個引數的隱含參照

在以下範例中，由於第一個引數一律位於上下文中，因此屬性參照(`homeAddress`)可直接建立至。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 第一個引數的明確參照

在以下範例中， `$1` 是指第一個引數。 因此， `$2` 會參照第二個引數等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用具名變數，使用Lambda標籤法

在以下範例中， `Profile` 是變數名稱，可由查詢作者選擇。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL常值

PQL支援下列常值型別：

| 常值 | 定義 | 範例 |
| ------- | ---------- | ------- |
| 字串 | 由雙引號包住的字元所組成的資料型別。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布林值 | 為true或false的資料型別。 | `true`、`false` |
| 整數 | 代表整數的資料型別。 可以是正數、負數或零。 | `-201`、`0`、`412` |
| 雙倍 | 代表任何實數的資料型別。 可以是正數、負數或零。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一種資料型別，可用來依據年、月和日建立整數引數的日期。 格式為 `date(year, month, day)` | `date(2020, 3, 14)` |
| 陣列 | 一種資料型別，由一組其他常值組成。 它使用方括弧將不同值分組，並使用逗號分隔不同值。 <br> **注意：** 您無法直接存取陣列中專案的屬性。 因此，如果您需要存取陣列中的屬性，支援的方法為 `select X from array where X.item = ...`. <br> PQL會保留字詞 `xEvent` 以參照連結至設定檔的體驗事件陣列。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相對時間參照 | 可用來形成時間戳記和時間間隔參照的保留字。 <ul><li>現在、今天、昨天、明天</li><li>這個、最後一個、下一個</li><li>之前、之後、從</li><li>毫秒、秒、分鐘、小時、天、周、月、年、十年、世紀/世紀、千年/千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |

## PQL函式

下表概述不同類別的支援PQL函式，包括進一步檔案的連結，以取得詳細資訊。

| 類別 | 定義 |
| -------- | ---------- |
| 布林值 | 用來在PQL中實作布林代數。 有關這些函式的詳細資訊，請參閱 [布林函式檔案](./boolean-functions.md). |
| 比較 | 用來比較不同的PQL元素。 有關這些函式的詳細資訊，請參閱 [比較函式檔案](./comparison-functions.md). |
| 陣列、清單和設定 | 用於與陣列、清單和集合互動。 有關這些函式的詳細資訊，請參閱 [陣列、清單和設定函式檔案](./array-functions.md). |
| 地圖 | 用於與地圖互動。 有關這些函式的詳細資訊，請參閱 [地圖函式檔案](./map-functions.md). |
| 字串 | 用於和字串互動。 有關這些函式的詳細資訊，請參閱 [字串函式檔案](./string-functions.md). |
| 物件 | 用於與物件互動。 有關這些函式的詳細資訊，請參閱 [物件函式檔案](./object-functions.md). |
| 算術 | 用於對PQL元素執行基本算術。 有關這些函式的詳細資訊，請參閱 [算術函式檔案](./arithmetic-functions.md) |
| 彙總 | 用於將陣列的結果組合成單一結果。 有關彙總函式的詳細資訊，請參閱 [彙總函式檔案](./aggregation-functions.md). |
| 日期和時間 | 與日期、時間和日期時間物件搭配使用。 有關這些函式的詳細資訊，請參閱 [日期/時間函式檔案](./datetime-functions.md). |
| 篩選 | 用於篩選陣列中的資料。 有關這些函式的詳細資訊，請參閱 [篩選函式檔案](./filter-functions.md). |
| 邏輯數量詞 | 用來判斷陣列中的條件。 如需詳細資訊，請參閱 [邏輯數量詞檔案](./logical-quantifiers.md). |
| 其他 | 不符合上述任何類別的函式，可以在 [雜項函式檔案](./misc-functions.md). |

## 後續步驟

現在您已瞭解如何使用 [!DNL Profile Query Language]中，您可在建立和修改區段定義時使用PQL。 如需區段的詳細資訊，請參閱 [分段總覽](../home.md).
