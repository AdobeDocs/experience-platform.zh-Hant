---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm；ui指南；對應程式；對應；資料準備；資料準備；
solution: Experience Platform
title: 使用「資料準備」處理資料格式
description: 本檔案概述「資料準備」中處理不同資料型別的方式。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: a49140853124f4f7beee87a739c8e670838947f4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 8%

---

# 使用「資料準備」處理資料格式

「資料準備」可以強健地處理擷取到Adobe Experience Platform中的不同格式資料。 本檔案概述使用「資料準備」處理不同資料格式的方式。

## 布林值 {#booleans}

如果來源型別是字串，而目標型別是布林值，資料準備可以自動剖析值並將來源值轉換為布林值。

值`y`、`yes`、`Y`、`YES`、`on`、`ON`、`true`和`TRUE`會自動剖析為`true`。

值`n`、`N`、`no`、`NO`、`off`、`OFF`、`false`和`FALSE`會自動剖析為`false`。

## 日期 {#dates}

「資料準備」支援日期函式，包括字串和日期時間物件。

### 日期函式格式

date函式會將字串與日期時間物件轉換為格式為ISO 8601的ZonedDateTime物件。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATE}` | 必填。代表日期的字串。 |
| `{FORMAT}` | 選填。 代表來源日期格式的字串。 在[日期/時間格式字串區段](#format)中可以找到更多有關字串格式的資訊。 |
| `{DEFAULT_DATE}` | 選填。 如果提供的日期為Null，則會傳回預設日期。 |

例如，運算式`date(orderDate, "yyyy-MM-dd")`會將「2020年12月31日」的`orderDate`值轉換為「2020-12-31」的日期時間值。

### 日期函式轉換

當來自傳入資料的字串欄位對應到使用Experience Data Model (XDM)的結構描述中的日期欄位時，應明確提及日期格式。 如果未明確提及，「資料準備」會嘗試將輸入資料與下列格式比對，以轉換該資料。 找到相符的格式後，就會停止評估任何後續格式。

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> 「資料準備」會儘可能將字串轉換為日期。 不過，這些轉換可能會導致不良結果。 例如，字串值「12112020」符合模式「MMddyyyy」，但使用者可能希望日期以模式「ddMMyyyy」讀取。 因此，使用者應明確提及字串的日期格式。

### 日期/時間格式字串 {#format}

>[!TIP]
>
>目前，如果日期值是以下格式，批次擷取的日期函式會移除毫秒： `2024-05-05 20:39:00.005` PST。 若要保留毫秒，請使用此格式： `2024-05-05 20:39:00.005-0800`

下表顯示格式字串定義的圖樣字母。 請注意，字母區分大小寫。

| 符號 | 含義 | 簡報 | 範例 |
| ------ | ------- | ------------ | ------- |
| G | 時代 | 文字 | AD； Anno Domini； A |
| Y | 年，根據ISO周 | 數字 | 1996； 96 |
| y | 年 | 數字 | 2004； 04 |
| 公尺/公尺 | 月份 | 數字/文字 | 7；07；7月；7月；J |
| w | 一年中的周 | 數字 | 27 |
| W | 當月第幾週 | 數字 | 3 |
| D | 一年當中的第幾天 | 數字 | 189 |
| d | 當月日期 | 數字 | 10 |
| F | 一個月中的星期幾 | 數字 | 2 |
| E | 一週中某天的名稱 | 文字 | 星期二；星期二 |
| u | 星期幾（以數字表示）。 1代表星期一， ...， 7代表星期日 | 數字 | 1 |
| 一 | AM/PM標籤 | 文字 | 下午 |
| H | 一天中的小時(0-23) | 數字 | 0 |
| k | 一天中的小時(1-24) | 數字 | 24 |
| K | 上午/下午的小時(0-11) | 數字 | 0 |
| h | 上午/下午的小時(1-12) | 數字 | 12 |
| m | 一小時中的分鐘 | 數字 | 38 |
|   | 一分鐘中的秒 | 數字 | 44 |
| S | 毫秒 | 數字 | 245 |
| z | 時區 | 一般時區 | 太平洋標準時間；PST；GMT-08:00 |
| Z | 時區 | rfc 822時區 | -0800 |
| X | 時區 | ISO 8601時區 | -08； -0800； -08:00 |
| V | 時區ID | 文字 | 美洲/洛杉磯 |
| O | 時區位移 | 文字 | GMT+8 |
| Q/q | 季別 | 數字/文字 | 第3季；03；Q3；第3季 |

## 地圖 {#maps}

[!DNL Data Prep]目前不支援對應。
