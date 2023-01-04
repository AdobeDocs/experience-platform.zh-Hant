---
keywords: Experience Platform；首頁；熱門主題；PQL;PQL；設定檔查詢語言
solution: Experience Platform
title: 配置檔案查詢語言(PQL)概述
topic-legacy: developer guide
description: 本指南提供PQL的一般概述，包括格式設定指南，並提供PQL運算式的範例。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是 [!DNL Experience Data Model] (XDM)相容的查詢語言，其設計為支援 [!DNL Real-Time Customer Profile] 資料。

本指南提供PQL的一般概述，包括格式設定指南，並提供PQL運算式的範例。

## PQL查詢格式

PQL查詢具有以下簽名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

輸入參數可以是簡單的基元，如布林值或字串，或更複雜的類型，如對象、陣列或映射。

有三種不同的方式可以參照PQL運算式內文中的輸入參數：

### 對第一個參數的隱式引用

在以下範例中，由於第一個參數一律在內容中，因此屬性參照(`homeAddress`)即可直接進行。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 對第一個參數的顯式引用

在以下範例中， `$1` 是指第一個參數。 因此， `$2` 會指第二個參數等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 命名變數的用法，使用lambda記號

在以下範例中， `Profile` 是變數名稱，查詢作者可選擇此名稱。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支援以下常值類型：

| 常值 | 定義 | 範例 |
| ------- | ---------- | ------- |
| 字串 | 由雙引號包住的字元組成的資料類型。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布林值 | 資料類型為true或false。 | `true`、`false` |
| 整數 | 代表整數的資料類型。 可以是正、負或零。 | `-201`、`0`、`412` |
| 雙倍 | 代表任何實數的資料類型。 可以是正、負或零。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一種資料類型，可用來根據年、月和日建立日期，作為整數參數。 格式為 `date(year, month, day)` | `date(2020, 3, 14)` |
| 陣列 | 由一組其他常值組成的資料類型。 它使用方括弧來分組，並以逗號來分隔不同的值。 <br> **注意：** 您無法直接存取陣列內項目的屬性。 因此，如果您需要存取陣列內的屬性，則支援的方法為 `select X from array where X.item = ...`. <br> PQL保留單詞 `xEvent` 以參照連結至設定檔的體驗事件陣列。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相對時間參考 | 可用來形成時間戳記和時間間隔參考的保留字。 <ul><li>今天，昨天，明天</li><li>這個，最後一個</li><li>之前，之後，從</li><li>毫秒，秒，分鐘，小時，日，周，月，年，十年，世紀/世紀，千年/千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |


## PQL函式

下表概述支援的PQL功能的不同類別，包括指向進一步文檔的連結，以了解更多資訊。

| 類別 | 定義 |
| -------- | ---------- |
| 布林值 | 用於在PQL中實現布爾代數。 如需這些函式的詳細資訊，請參閱 [布爾函式文檔](./boolean-functions.md). |
| 比較 | 用於比較不同的PQL元素。 如需這些函式的詳細資訊，請參閱 [比較函式文檔](./comparison-functions.md). |
| 陣列、清單和設定 | 用於與陣列、清單和集交互。 如需這些函式的詳細資訊，請參閱 [陣列、清單和設定函式文檔](./array-functions.md). |
| 地圖 | 用來與地圖互動。 如需這些函式的詳細資訊，請參閱 [映射函式文檔](./map-functions.md). |
| 字串 | 用來與字串互動。 如需這些函式的詳細資訊，請參閱 [字串函式文檔](./string-functions.md). |
| 物件 | 用於與物件互動。 如需這些函式的詳細資訊，請參閱 [對象函式文檔](./object-functions.md). |
| 算術 | 用於對PQL元素執行基本算術。 如需這些函式的詳細資訊，請參閱 [算術函式文檔](./arithmetic-functions.md) |
| 彙總 | 用於將陣列的結果合併為奇異結果。 有關聚合函式的詳細資訊，請參見 [聚合函式文檔](./aggregation-functions.md). |
| 日期和時間 | 與日期、時間和日期時間對象一起使用。 如需這些函式的詳細資訊，請參閱 [日期/時間函式文檔](./datetime-functions.md). |
| 篩選 | 用於篩選陣列內的資料。 如需這些函式的詳細資訊，請參閱 [篩選函式文檔](./filter-functions.md). |
| 邏輯量詞 | 用於斷言陣列內的條件。 如需詳細資訊，請參閱 [邏輯量化符文檔](./logical-quantifiers.md). |
| 其他 | 若不符合上述任何類別，可在 [雜項功能檔案](./misc-functions.md). |

## 後續步驟

既然你已經學會了如何使用 [!DNL Profile Query Language]，可在建立和修改區段時使用PQL。 如需分段的詳細資訊，請參閱 [細分概述](../home.md).
