---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；對應csv檔案至xdm；將csv對應至xdm;ui指南；對應程式；資料準備；資料準備；準備資料；
solution: Experience Platform
title: 使用資料準備處理資料格式
description: 本檔案概述在資料準備中處理不同資料類型的方式。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# 使用資料準備處理資料格式

資料準備功能可穩健處理擷取至Adobe Experience Platform的不同格式資料。 本檔案概述資料準備處理不同資料格式的方式。

## 布勒安 {#booleans}

如果源類型是字串，而目標類型是布爾值，則資料準備可以自動分析值並將源值轉換為布爾值。

值 `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`，和 `TRUE` 會自動剖析 `true`.

值 `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`，和 `FALSE` 會自動剖析 `false`.

## 日期 {#dates}

資料準備支援日期函式，既作為字串，也作為日期時間對象。

### 日期函式格式

日期函式將字串和日期時間對象轉換為ISO 8601格式化的ZonedDateTime對象。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATE}` | 必填。代表日期的字串。 |
| `{FORMAT}` | 選填. 代表來源日期格式的字串。 如需字串格式的詳細資訊，請參閱 [日期/時間格式字串區段](#format). |
| `{DEFAULT_DATE}` | 選填. 如果提供的日期為null，則要傳回的預設日期。 |

例如，運算式 `date(orderDate, "yyyy-MM-dd")` 將轉換 `orderDate` 值「2020年12月31日」轉換為日期時間值「2020-12-31」。

### 日期函式轉換

使用Experience Data Model(XDM)將來自傳入資料的字串欄位對應至結構中的日期欄位時，應明確提及日期格式。 如果未明確提及，資料準備將嘗試將輸入資料與以下格式進行匹配，以便轉換該資料。 找到相符的格式後，將停止評估任何後續格式。

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
> 「資料準備」會盡量將字串轉換為日期。 但是，這些轉換可能會產生不樂見的結果。 例如，字串值&quot;12112020&quot;與模式&quot;MMddyyyy&quot;相符，但使用者可能打算以模式&quot;ddMMyyyy&quot;讀取日期。 因此，使用者應明確提及字串的日期格式。

### 日期/時間格式字串 {#format}

下表顯示為格式字串定義的模式字母。 請注意，這些字母區分大小寫。

| 符號 | 含義 | 簡報 | 範例 |
| ------ | ------- | ------------ | ------- |
| G | 時代 | 文字 | 廣告；安諾·多米尼；A |
| Y | 年，根據ISO周 | 數字 | 1996; 96 |
| y | 年 | 數字 | 2004; 04 |
| M/L | 月份 | 數字/文字 | 7;07;7月；7月；J |
| w | 一年中的周 | 數字 | 27 |
| W | 當月的第一週 | 數字 | 3 |
| D | 一年當中的第幾天 | 數字 | 189 |
| d | 當月某日 | 數字 | 10 |
| F | 一個月中的某天 | 數字 | 2 |
| E | 星期的名稱 | 文字 | 星期二；星期二 |
| u | 一週中的某天，作為數字。 1代表星期一， ..., 7代表星期日 | 數字 | 1 |
| a | AM/PM標籤 | 文字 | PM |
| H | 小時(0-23) | 數字 | 0 |
| k | 一天中的小時(1-24) | 數字 | 24 |
| K | 上午/下午時間(0-11) | 數字 | 0 |
| h | 上午/下午時(1-12) | 數字 | 12 |
| m | 分鐘 | 數字 | 38 |
| s | 第二 | 數字 | 44 |
| S | 毫秒 | 數字 | 245 |
| z | 時區 | 一般時區 | 太平洋標準時間；PST;GMT-08:00 |
| Z | 時區 | RFC 822時區 | -0800 |
| X | 時區 | ISO 8601時區 | -08; -0800; -08:00 |
| V | 時區ID | 文字 | 美國/洛杉磯 |
| O | 時區偏移 | 文字 | GMT+8 |
| Q/q | 季別 | 數字/文字 | 3;03;第三季度；第3季度 |

## 地圖 {#maps}

目前不支援地圖 [!DNL Data Prep].
