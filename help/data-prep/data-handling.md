---
keywords: Experience Platform；首頁；熱門主題；映射csv；映射csv；映射csv；將csv檔案映射到xdm；將csv映射到xdm;ui指南；映射；資料準備；準備資料；
solution: Experience Platform
title: 使用資料準備處理資料格式
description: 本文檔概述了在資料準備中如何處理不同資料類型。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# 使用資料準備處理資料格式

Data Prep可以強健地處理接收到Adobe Experience Platform的不同格式的資料。 本文檔概述了如何使用資料準備處理不同的資料格式。

## 博萊安 {#booleans}

如果源類型是字串，而目標類型是布爾型，則資料準備可以自動分析該值並將源值轉換為布爾型。

值 `y`。 `yes`。 `Y`。 `YES`。 `on`。 `ON`。 `true`, `TRUE` 自動分析 `true`。

值 `n`。 `N`。 `no`。 `NO`。 `off`。 `OFF`。 `false`, `FALSE` 自動分析 `false`。

## 日期 {#dates}

Data Prep支援日期函式，既作為字串，又作為日期時間對象。

### 日期函式格式

date函式將字串和日期時間對象轉換為ISO 8601格式的ZonedDateTime對象。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATE}` | 必填。表示日期的字串。 |
| `{FORMAT}` | 選填. 表示源日期格式的字串。 有關字串格式的詳細資訊，請參閱 [日期/時間格式字串節](#format)。 |
| `{DEFAULT_DATE}` | 選填. 如果提供的日期為空，則返回的預設日期。 |

例如，表達式 `date(orderDate, "yyyy-MM-dd")` 將轉換 `orderDate` 值「2020年12月31日」轉換為日期時間值「2020-12-31」。

### 日期函式轉換

當使用體驗資料模型(XDM)將來自傳入資料的字串欄位映射到方案中的日期欄位時，應明確提及日期格式。 如果未明確提到，Data Prep將嘗試將輸入資料與以下格式匹配以轉換輸入資料。 找到匹配格式後，將停止計算任何後續格式。

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
> 資料準備將嘗試將字串轉換為盡可能好的日期。 但是，這些轉換可能導致不良結果。 例如，字串值「12112020」與模式「MMdyyy」匹配，但用戶可能希望讀取日期時採用模式「ddMMyyyy」。 因此，用戶應明確提及字串的日期格式。

### 日期/時間格式字串 {#format}

下表顯示了為格式字串定義的模式字母。 請注意，這些信件區分大小寫。

| 符號 | 含義 | 簡報 | 範例 |
| ------ | ------- | ------------ | ------- |
| G | 時代 | 文字 | 廣告；安諾·多米尼；A |
| Y | 年，基於ISO周 | 數字 | 1996; 96 |
| y | 年 | 數字 | 2004; 04 |
| M/L | 年月 | 數字/文本 | 7;07;7月；7月；J |
| w | 年中的周 | 數字 | 27 |
| W | 月份的周 | 數字 | 3 |
| D | 年中的某一天 | 數字 | 189 |
| d | 月中的某天 | 數字 | 10 |
| F | 一個月中的星期 | 數字 | 2 |
| E | 星期幾的名稱 | 文字 | 星期二；週二 |
| u | 星期幾，作為數字。 1表示星期一， ..., 7表示星期日 | 數字 | 1 |
| a | AM/PM標籤 | 文字 | PM |
| H | 一天中的小時(0-23) | 數字 | 0 |
| k | 一天中的小時(1-24) | 數字 | 24 |
| K | 上午/下午(0-11) | 數字 | 0 |
| h | 上午/下午(1-12) | 數字 | 12 |
| m | 分鐘 | 數字 | 38 |
| s | 分秒 | 數字 | 44 |
| S | 毫秒 | 數字 | 245 |
| z | 時區 | 一般時區 | 太平洋標準時間；PST;GMT-08:00 |
| Z | 時區 | RFC 822時區 | -0800 |
| X | 時區 | ISO 8601時區 | -08; -0800; -08:00 |
| V | 時區ID | 文字 | 美洲/洛杉磯 |
| O | 時區偏移 | 文字 | GMT+8 |
| 問/問 | 年中的季度 | 數字/文本 | 3;03;第3季度；第三季度 |

## 地圖 {#maps}

中當前不支援映射 [!DNL Data Prep]。
