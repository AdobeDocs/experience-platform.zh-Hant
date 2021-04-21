---
keywords: Experience Platform；首頁；熱門主題；PQL;pql；配置檔案查詢語言
solution: Experience Platform
title: 配置檔案查詢語言(PQL)概述
topic-legacy: developer guide
description: 本指南提供PQL的一般概述，涵蓋格式准則並提供PQL表達式示例。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是一種 [!DNL Experience Data Model] (XDM)相容的查詢語言，旨在支援資料分段查詢的定義和 [!DNL Real-time Customer Profile] 執行。

本指南提供PQL的一般概述，涵蓋格式准則並提供PQL表達式示例。

## PQL查詢格式

PQL查詢具有以下特徵碼：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

輸入參數可以是簡單的基元，例如布林值或字串，或是更複雜的類型，例如物件、陣列或地圖。

PQL表達式內文中有三種不同的輸入參數引用方法：

### 第一個參數的隱式引用

在以下範例中，由於第一個參數永遠在上下文中，所以可以直接對其建立屬性參考(`homeAddress`)。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 對第一個參數的顯式引用

在以下範例中，`$1`是指第一個參數。 因此，`$2`會參照第二個參數等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用lambda符號使用命名變數

在以下範例中，`Profile`是變數名稱，可由查詢作者選擇。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文字

PQL支援以下常值類型：

| 常值 | 定義 | 範例 |
| ------- | ---------- | ------- |
| 字串 | 由雙引號圍繞的字元組成的資料類型。 | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| 布林值 | True或false的資料類型。 | `true`, `false` |
| 整數 | 表示整數的資料類型。 可以是正面、負面或零。 | `-201`,  `0`  `412` |
| 雙倍 | 表示任何實數的資料類型。 可以是正面、負面或零。 | `-51.24`,  `3.14`  `0.6942058` |
| Date | 一種資料類型，可用來根據年、月和日建立日期作為整數參數。 格式為`date(year, month, day)` | `date(2020, 3, 14)` |
| 陣列 | 作為一組其他常值組成的資料類型。 它使用方括弧來分組，使用逗號來分隔不同的值。<br> **注意：** 您無法直接存取陣列中項目的屬性。因此，如果您需要訪問陣列中的屬性，則支援的方法為`select X from array where X.item = ...`。 <br> PQL保留該字詞 `xEvent` 以引用連結至描述檔的體驗事件陣列。 | `[1, 4, 7]`的  `["US", "CA"]` |
| 相對時間參考 | 可用於形成時間戳記和時間間隔引用的保留字。 <ul><li>現在，今天，昨天，明天</li><li>這個，最後一個，下一個</li><li>之前，之後，從</li><li>毫秒，秒，分鐘，小時，日，周，月，年，十年，世紀／世紀，千年／千年</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`  `X.timestamp occurs <= 3 days before now` |


## PQL函式

下表概述了支援的PQL功能的不同類別，包括指向進一步文檔的連結以瞭解詳細資訊。

| 類別 | 定義 |
| -------- | ---------- |
| 布林值 | 用於在PQL中實現布爾代數。 有關這些函式的詳細資訊，請參閱[布爾函式文檔](./boolean-functions.md)。 |
| 比較 | 用於比較不同的PQL元素。 有關這些函式的詳細資訊，請參閱[比較函式文檔](./comparison-functions.md)。 |
| 陣列、清單和設定 | 用於與陣列、清單和集交互。 有關這些函式的詳細資訊，請參閱[array、list和set functions文檔](./array-functions.md)。 |
| 地圖 | 用來與地圖互動。 有關這些函式的詳細資訊，請參閱[map函式文檔](./map-functions.md)。 |
| 字串 | 用來與字串互動。 有關這些函式的詳細資訊，請參閱[string functions document](./string-functions.md)。 |
| 物件 | 用於與物件互動。 有關這些函式的詳細資訊，請參見[object functions document](./object-functions.md)。 |
| 算術 | 用於對PQL元素執行基本算術。 有關這些函式的詳細資訊，請參閱[算術函式文檔](./arithmetic-functions.md) |
| 彙總 | 用於將陣列的結果組合為單一結果。 有關聚合函式的詳細資訊，請參見[聚合函式文檔](./aggregation-functions.md)。 |
| 日期和時間 | 與日期、時間和日期時間對象一起使用。 有關這些函式的詳細資訊，請參閱[date/time函式文檔](./datetime-functions.md)。 |
| 篩選 | 用於篩選陣列內的資料。 有關這些函式的詳細資訊，請參閱[filter functions文檔](./filter-functions.md)。 |
| 邏輯量詞 | 用於斷言陣列中的條件。 有關詳細資訊，請參閱[邏輯量詞文檔](./logical-quantifiers.md)。 |
| 其他 | 在[雜項函式文檔](./misc-functions.md)中可找到不符合上述任何類別的函式。 |

## 後續步驟

現在您已學會如何使用[!DNL Profile Query Language]，您可以在建立和修改區段時使用PQL。 如需細分的詳細資訊，請閱讀[分段概觀](../home.md)。
