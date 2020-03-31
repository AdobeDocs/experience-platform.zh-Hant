---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 配置檔案查詢語言(PQL)概述
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 配置檔案查詢語言(PQL)概述

描述檔查詢語言(PQL)是符合Experience Data Model(XDM)的查詢語言，旨在支援對即時客戶描述檔資料的分段查詢的定義和執行。

本指南提供PQL的一般概述，涵蓋格式准則並提供PQL表達式示例。

## PQL查詢格式

PQL查詢具有以下特徵碼：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

輸入參數可以是簡單的基元，例如布林值或字串，或是更複雜的類型，例如物件、陣列或地圖。

PQL運 **算式內** ，有三種不同的參照輸入參數的方式：

### 第一個參數的隱式引用

在以下範例中，由於第一個參數永遠在上下文中，所以可以直接對其建立屬性參考(`homeAddress`)。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 對第一個參數的顯式引用

在以下範例中， `$1` 參考第一個參數。 因此，會參 `$2` 考第二個參數等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用lambda符號使用命名變數

在以下範例中， `Profile` 是變數名稱，可由查詢作者選擇。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文字

PQL支援以下常值類型：

| 常值 | 定義 | 範例 |
| ------- | ---------- | ------- |
| 字串 | 由雙引號圍繞的字元組成的資料類型。 | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| 布林值 | True或false的資料類型。 | `true`, `false` |
| 整數 | 表示整數的資料類型。 可以是正面、負面或零。 | `-201`, `0`, `412` |
| 雙倍 | 表示任何實數的資料類型。 可以是正面、負面或零。 | `-51.24`, `3.14`, `0.6942058` |
| 日期 | 一種資料類型，可用來根據年、月和日建立日期作為整數參數。 格式為 `date(year, month, day)` | `date(2020, 3, 14)` |
| 陣列 | 作為一組其他常值組成的資料類型。 它使用方括弧來分組，使用逗號來分隔不同的值。 <br> **注意：** 您無法直接存取陣列中項目的屬性。 因此，如果您需要訪問陣列中的屬性，則支援的方法是 `select X from array where X.item = ...`。 <br> PQL保留該單 `xEvent` 字以引用連結至描述檔的體驗事件陣列。 | `[1, 4, 7]`, `["US", "CA"]` |
| 相對時間參考 | 可用於形成時間戳記和時間間隔引用的保留字。 <ul><li>現在，今天，昨天，明天</li><li>這個，最後一個，下一個</li><li>之前，之後，從</li><li>毫秒，秒，分鐘，小時，日，周，月，年，十年，世紀／世紀，千年／千年</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL函式

下表概述了支援的PQL功能的不同類別，包括指向進一步文檔的連結以瞭解詳細資訊。

| 類別 | 定義 |
| -------- | ---------- |
| 布林值 | 用於在PQL中實現布爾代數。 有關這些函式的更多資訊，請參見布爾 [函式文檔](./boolean-functions.md)。 |
| 比較 | 用於比較不同的PQL元素。 有關這些函式的更多資訊，請參見 [比較函式文檔](./comparison-functions.md)。 |
| 陣列、清單和設定 | 用於與陣列、清單和集交互。 有關這些函式的詳細資訊，請參 [閱陣列、清單和設定函式文檔](./array-functions.md)。 |
| 地圖 | 用來與地圖互動。 有關這些函式的詳細資訊，請參閱地圖函 [數檔案](./map-functions.md)。 |
| 字串 | 用來與字串互動。 有關這些函式的詳細資訊，請參閱字 [串函式檔案](./string-functions.md)。 |
| 算術 | 用於對PQL元素執行基本算術。 有關這些函式的更多資訊，請參閱算術函 [數檔案](./arithmetic-functions.md) |
| 聚總 | 用於將陣列的結果組合為單一結果。 有關聚合函式的詳細資訊，請參見聚合函 [數文檔](./aggregation-functions.md)。 |
| 日期和時間 | 與日期、時間和日期時間對象一起使用。 有關這些函式的更多資訊，請參閱日 [期／時間函式檔案](./datetime-functions.md)。 |
| 篩選 | 用於篩選陣列內的資料。 有關這些函式的更多資訊，請參閱篩 [選函式文檔](./filter-functions.md)。 |
| 邏輯量詞 | 用於斷言陣列中的條件。 在邏輯量詞文檔中可以找 [到更多資訊](./logical-quantifiers.md)。 |
| 其他 | 不適用於上述任何類別的函式可在其他函式文 [件中找到](./misc-functions.md)。 |

## 後續步驟

現在您已學會如何使用描述檔查詢語言，因此在建立和修改區段時，可以使用PQL。 如需細分的詳細資訊，請閱讀分 [段概觀](../home.md)。