---
keywords: Experience Platform;home；熱門主題；map csv;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;date;date函式；dates;
solution: Experience Platform
title: 日期函式
topic: overview
description: 本檔案介紹資料準備使用的日期功能。
translation-type: tm+mt
source-git-commit: 28c13101be37c5c7680c5d46005509bfd122018f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 16%

---


# 日期函式

「資料準備」支援日期函式，包括字串和日期時間對象。

## 日期函式轉換

當使用Experience Data Model(XDM)將傳入資料的字串欄位對應至結構中的日期欄位時，應明確提及日期格式。 如果未明確提及，「資料準備」會嘗試將輸入資料與下列格式相符，以轉換該資料。 找到符合的格式後，將停止評估任何後續格式。

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
> 「資料準備」會盡量將字串轉換為日期。 但是，這些轉換可能會導致不理想的結果。 例如，字串值&quot;12112020&quot;與模式&quot;MMddyyyy&quot;相符，但使用者可能想要將日期與模式&quot;ddMMyyyy&quot;一起讀取。 因此，使用者應明確提及字串的日期格式。

## 日期／時間格式字串

下表顯示為格式字串定義的模式字母。 請注意，字母區分大小寫。

| 符號 | 意義 | 簡報 | 範例 |
| ------ | ------- | ------------ | ------- |
| G | 時代 | 文字 | 廣告；安諾·多米尼；A |
| Y | 年，根據ISO周 | 數字 | 1996年；96 |
| y | 年 | 數字 | 2004年；04 |
| M/L | 年度月份 | 數字／文字 | 7;07;7月；7月；J |
| w | 年度中的一週 | 數字 | 27 |
| W | 當月的星期 | 數字 | 3 |
| D | 年度日 | 數字 | 189 |
| d | 當月日 | 數字 | 10 |
| F | 一個月中的一週中的某天 | 數字 | 2 |
| E | 一週中某天的名稱 | 文字 | 星期二；星期二 |
| u | 星期幾，作為數字。 1代表星期一， ..., 7代表星期日 | 數字 | 1 |
| a | AM/PM標籤 | 文字 | PM |
| H | 一天中的小時(0-23) | 數字 | 0 |
| k | 一天中的小時(1-24) | 數字 | 24 |
| K | 上午／下午(0-11) | 數字 | 0 |
| h | 上午／下午(1-12) | 數字 | 12 |
| m | 每小時分鐘 | 數字 | 38 |
| s | 分秒必爭 | 數字 | 44 |
| S | 毫秒 | 數字 | 245 |
| z | 時區 | 一般時區 | 太平洋標準時間；PST;GMT-08:00 |
| Z | 時區 | RFC 822時區 | -0800 |
| X | 時區 | ISO 8601時區 | -08;-0800;-08:00 |
| V | 時區ID | 文字 | 美洲／洛杉磯 |
| O | 時區偏移 | 文字 | GMT+8 |
| Q/q | 年度第四季 | 數字／文字 | 3;03;第3季度；第三季度 |

**範例**

運算式`date(orderDate, "yyyy-MM-dd")`會將`orderDate`值&quot;Decer 31st, 2020&quot;轉換為日期時間值&quot;2020-12-31&quot;。