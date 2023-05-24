---
keywords: Experience Platform；首頁；熱門主題；PQL;pql；配置檔案查詢語言
solution: Experience Platform
title: 配置檔案查詢語言(PQL)概述
description: 本指南概括介紹了PQL，包括格式准則，並提供了PQL表達式示例。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是 [!DNL Experience Data Model] (XDM)相容查詢語言，該語言旨在支援分段查詢的定義和執行 [!DNL Real-Time Customer Profile] 資料。

本指南概括介紹了PQL，包括格式准則，並提供了PQL表達式示例。

## PQL查詢格式

PQL查詢具有以下簽名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

輸入參數可以是簡單的基元，如布爾值或字串，也可以是更複雜的類型，如對象、陣列或映射。

在PQL表達式正文中引用輸入參數有三種不同的方法：

### 對第一個參數的隱式引用

在以下示例中，由於第一個參數始終位於上下文中，因此屬性引用(`homeAddress`)可以直接製作。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 對第一個參數的顯式引用

在下面的示例中， `$1` 引用第一個參數。 因此， `$2` 引用第二個參數等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用lambda表示法使用命名變數

在下面的示例中， `Profile` 是變數名，查詢作者可以選擇該變數名。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支援以下文字類型：

| 文字 | 定義 | 範例 |
| ------- | ---------- | ------- |
| 字串 | 一種資料類型，由雙引號環繞的字元組成。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布林值 | 為true或false的資料類型。 | `true`、`false` |
| 整數 | 表示整數的資料類型。 可以是正的、負的或零的。 | `-201`、`0`、`412` |
| 雙倍 | 表示任意實數的資料類型。 可以是正的、負的或零的。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一種資料類型，可用於根據年、月和日作為整數參數建立日期。 它的格式為 `date(year, month, day)` | `date(2020, 3, 14)` |
| 陣列 | 作為一組其他文字值組成的資料類型。 它使用方括弧對不同值進行分組，使用逗號分隔。 <br> **注：** 不能直接訪問陣列中項的屬性。 因此，如果需要訪問陣列內的屬性，支援的方法是 `select X from array where X.item = ...`。 <br> PQL保留該詞 `xEvent` 引用連結到配置檔案的一系列體驗事件。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相對時間引用 | 可用於形成時間戳和時間間隔引用的保留字。 <ul><li>今天，昨天，明天</li><li>下一個</li><li>之前，之後，從</li><li>毫秒、秒、分鐘、小時、天、周、月、年、十年、世紀/千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |


## PQL函式

下表概述了支援的PQL功能的不同類別，包括指向進一步文檔的連結以瞭解更多資訊。

| 類別 | 定義 |
| -------- | ---------- |
| 布林值 | 用於在PQL中實現布爾代數。 有關這些函式的詳細資訊，請參見 [布爾函式文檔](./boolean-functions.md)。 |
| 比較 | 用於比較不同的PQL元素。 有關這些函式的詳細資訊，請參見 [比較函式文檔](./comparison-functions.md)。 |
| 陣列、清單和集 | 用於與陣列、清單和集交互。 有關這些函式的詳細資訊，請參見 [陣列、清單和設定函式文檔](./array-functions.md)。 |
| 地圖 | 用於與地圖交互。 有關這些函式的詳細資訊，請參見 [映射函式文檔](./map-functions.md)。 |
| 字串 | 用於與字串交互。 有關這些函式的詳細資訊，請參見 [字串函式文檔](./string-functions.md)。 |
| 物件 | 用於與對象交互。 有關這些函式的詳細資訊，請參見 [對象函式文檔](./object-functions.md)。 |
| 算術 | 用於對PQL元素執行基本算術。 有關這些函式的詳細資訊，請參見 [算術函式文檔](./arithmetic-functions.md) |
| 彙總 | 用於將陣列結果合併為奇異結果。 有關聚合函式的詳細資訊，請參閱 [聚合函式文檔](./aggregation-functions.md)。 |
| 日期和時間 | 與date 、 time和datetime對象一起使用。 有關這些函式的詳細資訊，請參見 [日期/時間函式文檔](./datetime-functions.md)。 |
| 篩選 | 用於篩選陣列中的資料。 有關這些函式的詳細資訊，請參見 [篩選函式文檔](./filter-functions.md)。 |
| 邏輯量詞 | 用於在陣列中斷言條件。 有關詳細資訊，請參閱 [邏輯量詞文檔](./logical-quantifiers.md)。 |
| 其他 | 在中，可以找到不適合上述任何類別的函式 [雜項函式文檔](./misc-functions.md)。 |

## 後續步驟

既然你已經學會了如何使用 [!DNL Profile Query Language]，可在建立和修改段時使用PQL。 有關細分的詳細資訊，請閱讀 [分段概述](../home.md)。
