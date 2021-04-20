---
keywords: Experience Platform;home；熱門主題；map csv;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: 資料準備映射函式
topic: overview
description: 本文檔介紹與「資料準備」一起使用的映射功能。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
translation-type: tm+mt
source-git-commit: c3939d4ce30bf12748b898f461a166f28f010abf
workflow-type: tm+mt
source-wordcount: '3798'
ht-degree: 3%

---

# 資料準備映射函式

「資料準備」功能可用來根據在來源欄位中輸入的內容來計算和計算值。

## 欄位

欄位名稱可以是任何合法識別碼- Unicode字母和數字的不限長度序列，以字母、美元符號(`$`)或底線字元(`_`)開頭。 變數名稱也區分大小寫。

如果欄位名稱未遵循此慣例，欄位名稱必須用`${}`包裝。 因此，例如，如果欄位名稱為「名字」或「名字」，則名稱必須分別包裝為`${First Name}`或`${First.Name}`。

此外，如果欄位名稱是下列保留關鍵字的&#x200B;**any**，則必須用`${}`包裝：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

子欄位內的資料可使用點記號來存取。 例如，如果有`name`物件，則要存取`firstName`欄位，請使用`name.firstName`。

## 函式清單

下表列出所有支援的映射函式，包括範例運算式及其產生的輸出。

### 字串函式{#string}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 串連指定的字串。 | <ul><li>字串：將串連的字串。</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 爆炸 | 根據規則運算式分割字串，並傳回部件陣列。 可選擇包含規則運算式以分割字串。 預設情況下，拆分解析為&quot;,&quot;。 下列分隔字元&#x200B;**需要**&#x200B;以`\`逸出：`+, ?, ^, |, ., [, (, {, ), *, $, \`如果您包含多個字元作為分隔字元，分隔字元將視為多字元分隔字元。 | <ul><li>字串：**必要**&#x200B;需要分割的字串。</li><li>REGEX:*可選*&#x200B;可用於拆分字串的規則運算式。</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot;) | `["Hi,", "there"]` |
| instr | 傳回子字串的位置／索引。 | <ul><li>輸入：**必要**&#x200B;正在搜索的字串。</li><li>子字串：**Required**&#x200B;在字串中搜尋的子字串。</li><li>START_POSITION:*可選*&#x200B;要開始查找字串的位置。</li><li>具體值：*可選*&#x200B;從開始位置尋找的第n個出現點。 預設為1。 </li></ul> | instr（INPUT，子字串， START_POSITION, OCCURRENCE） | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 如果原始字串中有搜尋字串，請取代該搜尋字串。 | <ul><li>輸入：**必要**&#x200B;輸入字串。</li><li>TO_FIND:**必要**&#x200B;要在輸入內查找的字串。</li><li>TO_REPLACE:**Required**&#x200B;將取代&quot;TO_FIND&quot;中值的字串。</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;這是字串替換測試&quot; |
| substr | 傳回指定長度的子字串。 | <ul><li>輸入：**必要**&#x200B;輸入字串。</li><li>START_INDEX:**Required**&#x200B;子字串開始的輸入字串索引。</li><li>長度：**必要**&#x200B;子字串的長度。</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /&lt;a0/lcase<br> | 將字串轉換為小寫。 | <ul><li>輸入：**必要**&#x200B;將轉換為小寫的字串。</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /&lt;a0/ucase<br> | 將字串轉換為大寫。 | <ul><li>輸入：**必要**&#x200B;將轉換為大寫的字串。</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | 在分隔符上拆分輸入字串。 以下分隔符&#x200B;**需要**&#x200B;以`\`逸出：`\`。 如果您包含多個分隔字元，字串將分割在字串中所顯示之分隔字元的&#x200B;**any**&#x200B;上。 | <ul><li>輸入：**必要**&#x200B;將要拆分的輸入字串。</li><li>分隔符號：**必要**&#x200B;用於拆分輸入的字串。</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符連接對象清單。 | <ul><li>分隔符號：**Required**&#x200B;將用於連接對象的字串。</li><li>對象：**必要**&#x200B;要連接的字串陣列。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | 將字串的左側與另一個指定字串相貼。 | <ul><li>輸入：**必要**&#x200B;要填補的字串。 此字串可以是null。</li><li>計數：**必要**&#x200B;要填補的字串大小。</li><li>填充：**Required**&#x200B;用來加入輸入的字串。 如果為null或空白，則會視為單一空格。</li></ul> | lpad（輸入、計數、填充） | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | 將字串的右側與另一個指定字串貼齊。 | <ul><li>輸入：**必要**&#x200B;要填補的字串。 此字串可以是null。</li><li>計數：**必要**&#x200B;要填補的字串大小。</li><li>填充：**Required**&#x200B;用來加入輸入的字串。 如果為null或空白，則會視為單一空格。</li></ul> | rpad（輸入、計數、填充） | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | 取得指定字串的第一個&quot;n&quot;字元。 | <ul><li>字串：**Required**&#x200B;您要取得的第一個&quot;n&quot;字元的字串。</li><li>計數：**必要**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | left（字串，計數） | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | 取得指定字串的最後一個&quot;n&quot;字元。 | <ul><li>字串：**Required**&#x200B;您要取得最後&quot;n&quot;字元的字串。</li><li>計數：**必要**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | 從字串開頭移除空格。 | <ul><li>字串：**Required**&#x200B;您要從中刪除空格的字串。</li></ul> | ltrim(STRING) | ltrim(&quot;hello&quot;) | &quot;hello&quot; |
| rtrim | 從字串結尾移除空格。 | <ul><li>字串：**Required**&#x200B;您要從中刪除空格的字串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | 從字串的開頭和結尾移除空格。 | <ul><li>字串：**Required**&#x200B;您要從中刪除空格的字串。</li></ul> | trim(STRING) | trim(&quot;hello &quot;) | &quot;hello&quot; |
| 等於 | 比較兩個字串以確認其是否相等。 此函式區分大小寫。 | <ul><li>STRING1:**必要**&#x200B;您要比較的第一個字串。</li><li>STRING2:**必要**&#x200B;您要比較的第二個字串。</li></ul> | STRING1&#x200B;.equals(&#x200B;STRING2) | &quot;string1&quot;&#x200B;。equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比較兩個字串以確認其是否相等。 此函式區分&#x200B;**not**&#x200B;大小寫。 | <ul><li>STRING1:**必要**&#x200B;您要比較的第一個字串。</li><li>STRING2:**必要**&#x200B;您要比較的第二個字串。</li></ul> | STRING1&#x200B;.equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;&#x200B;。equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### 規則運算式函式

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根據規則運算式，從輸入字串擷取群組。 | <ul><li>字串：**Required**&#x200B;您要從中提取組的字串。</li><li>REGEX:**必要**&#x200B;您希望群組相符的規則運算式。</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot;&#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;、&quot;E259&quot;、&quot;1_1&quot;] |
| matches_regex | 檢查字串是否與輸入的規則運算式相符。 | <ul><li>字串：**Required**&#x200B;您正在檢查的字串與規則運算式相符。</li><li>REGEX:**必要**&#x200B;您要比較的規則運算式。</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### 散列函式{#hashing}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 使用安全雜湊算法1(SHA-1)輸入並產生雜湊值。 | <ul><li>輸入：**必要**&#x200B;要雜湊的純文字檔案。</li><li>字元集：*可選*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | 使用安全雜湊演算法256(SHA-256)輸入並產生雜湊值。 | <ul><li>輸入：**必要**&#x200B;要雜湊的純文字檔案。</li><li>字元集：*可選*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B; e6a39af698154a83a586ee270a0d372104 |
| sha512 | 使用安全雜湊演算法512(SHA-512)輸入並產生雜湊值。 | <ul><li>輸入：**必要**&#x200B;要雜湊的純文字檔案。</li><li>字元集：*可選*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232b21d2a8704ada2cdcd7b367dd078a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | 使用MD5輸入並產生雜湊值。 | <ul><li>輸入：**必要**&#x200B;要雜湊的純文字檔案。</li><li>字元集：*可選*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | 輸入使用循環冗餘校驗(CRC)算法產生32位循環碼。 | <ul><li>輸入：**必要**&#x200B;要雜湊的純文字檔案。</li><li>字元集：*可選*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL函式{#url}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 從指定URL傳回通訊協定。 如果輸入無效，則返回null。 | <ul><li>URL:**必要**&#x200B;需要提取協定的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 傳回指定URL的主機。 如果輸入無效，則返回null。 | <ul><li>URL:**必要**&#x200B;需要提取主機的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 傳回指定URL的連接埠。 如果輸入無效，則返回null。 | <ul><li>URL:**必要**&#x200B;需要從中提取埠的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 傳回指定URL的路徑。 預設會傳回完整路徑。 | <ul><li>URL:**必要**&#x200B;需要擷取路徑的URL。</li><li>完整路徑：*可選*&#x200B;一個布爾值，它確定是否返回完整路徑。 如果設為false，則只會傳迴路徑的結尾。</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | 傳回指定URL的查詢字串。 | <ul><li>URL:**必要**&#x200B;您嘗試從中取得查詢字串的URL。</li><li>錨點：**Required**&#x200B;決定如何使用查詢字串中的錨點。 可以是三個值之一：&quot;retain&quot;、&quot;remove&quot;或&quot;append&quot;。<br><br>如果值為&quot;retain&quot;，則錨點會附加至傳回的值。<br>如果值為&quot;remove&quot;，則錨點將從傳回的值中移除。<br>如果值是「附加」，則錨點會傳回為個別值。</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_&#x200B;str(&quot;foo://example.com:8042&#x200B;/over/there?name&#x200B; nose&quot;, &quot;retain&quot;)&lt;a0/&#x200B;>get_url_str&#x200B;=get_query ronesi&quot;, &quot;ret_ret other?name=ferret#nosi&quot;)<br>get_url_url_url_ur_r_0(8_rerer_&#x200B;_serer_0(8_serererererer(2 foo://example.com#nose&quot;, &quot;append&quot;)<br> | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### 日期和時間函式{#date-and-time}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。 有關`date`函式的更多資訊，請參閱[資料格式處理指南](./data-handling.md#dates)的日期部分。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 檢索當前時間。 |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 檢索當前Unix時間。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式格式化輸入日期。 | <ul><li>日期：**Required**&#x200B;您要格式化的輸入日期，作為ZonedDateTime物件。</li><li>格式：**必要**&#x200B;您要將日期變更為的格式。</li></ul> | 格式（日期，格式） | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 根據指定的格式將時間戳轉換為日期字串。 | <ul><li>時間戳記：**必要**&#x200B;您要格式化的時間戳記。 以毫秒為單位寫入。</li><li>格式：**Required**&#x200B;您希望將時間戳更改為的格式。</li></ul> | dformat&#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | 「2019年10月23日11:24」 |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期：**必要**&#x200B;代表日期的字串。</li><li>格式：**Required**&#x200B;代表日期格式的字串。</li><li>DEFAULT_DATE:**Required**&#x200B;如果提供的日期為null，則返回預設日期。</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期：**必要**&#x200B;代表日期的字串。</li><li>格式：**Required**&#x200B;代表日期格式的字串。</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期：**必要**&#x200B;代表日期的字串。</li></ul> | 日期（日期） | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | 擷取日期的部分。 支援下列元件值：<br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;q&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;&lt;dydya1111>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;a29/>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;毫秒&quot;<br>&quot;ms&quot;<br><br> | <ul><li>元件：**必要**&#x200B;代表日期部分的字串。 </li><li>日期：**必要**&#x200B;日期，以標準格式。</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 在指定日期中替換元件。 接受下列元件：<br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br> | <ul><li>元件：**必要**&#x200B;代表日期部分的字串。 </li><li>值：**Required**&#x200B;要為指定日期的元件設定的值。</li><li>日期：**必要**&#x200B;日期，以標準格式。</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | 從零件建立日期。 此函式也可使用make_timestamp來感應。 | <ul><li>年：**必填**&#x200B;年份，以四位數字寫入。</li><li>月份：**必要**&#x200B;月份。 允許的值是1到12。</li><li>日：**必要**&#x200B;日。 允許的值是1到31。</li><li>小時：**必要**&#x200B;小時。 允許的值為0到23。</li><li>分鐘：**必要**&#x200B;分鐘。 允許的值是0到59。</li><li>納秒：**必要**&#x200B;納秒值。 允許的值為0到999999999。</li><li>時區：**必要**&#x200B;日期時間的時區。</li></ul> | make_date_time&#x200B;(YEAR、MONTH、DAY、HOUR、MINUTE、SECOND、NS、TIMEZONE) | make_date_time&#x200B;(2019、10、17、11、55、12、999、「America/Los_Angeles」) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 將任何時區中的日期轉換為UTC中的日期。 | <ul><li>日期：**必要**&#x200B;您嘗試轉換的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 將日期從一個時區轉換為另一個時區。 | <ul><li>日期：**必要**&#x200B;您嘗試轉換的日期。</li><li>區域：**必要**&#x200B;您嘗試將日期轉換為的時區。</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### 層次——對象{#objects}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | 傳回輸入的大小。 | <ul><li>輸入：**Required**&#x200B;您要尋找大小的物件。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 檢查對象是否為空。 | <ul><li>輸入：**Required**&#x200B;您嘗試檢查的物件為空。</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | 建立對象清單。 | <ul><li>輸入：**必需**&#x200B;鍵和陣列對的分組。</li></ul> | arrays_to_object(INPUT) | 需要樣本 | 需要樣本 |
| to_object | 根據給定的平面鍵／值對建立對象。 | <ul><li>輸入：**Required**&#x200B;鍵／值對的平面清單。</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;、&quot;John&quot;、&quot;lastName&quot;、&quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 從輸入字串建立對象。 | <ul><li>字串：**Required**&#x200B;正在解析以建立對象的字串。</li><li>VALUE_DELIMITER:*可選*&#x200B;分隔欄位與值的分隔字元。 預設分隔字元為`:`。</li><li>FIELD_DELIMITER:*可選*&#x200B;分隔欄位值對的分隔字元。 預設分隔字元為`,`。</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | 電話- 123 456 7890&quot;、&quot;-&quot;、&quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 檢查源資料中是否存在對象。 | <ul><li>輸入：**必要**&#x200B;要檢查的路徑（如果它存在於源資料中）。</li></ul> | is_set(INPUT) | is_set&#x200B;(&quot;evars.evar.field1&quot;) | true |
| 抵消 | 將屬性的值設定為`null`。 當您不想將欄位複製到目標架構時，應使用此功能。 |  | nullify() | nullify() | `null` |

{style=&quot;table-layout:auto&quot;}

### 層次——陣列{#arrays}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 聚結 | 返回給定陣列中的第一個非空對象。 | <ul><li>輸入：**Required**&#x200B;要查找的第一個非空對象的陣列。</li></ul> | 合併（輸入） | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | 檢索給定陣列的第一個元素。 | <ul><li>輸入：**Required**&#x200B;您要尋找的第一個元素的陣列。</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 檢索給定陣列的最後一個元素。 | <ul><li>輸入：**Required**&#x200B;您要查找的最後一個元素的陣列。</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 將元素添加到陣列末尾。 | <ul><li>陣列：**Required**&#x200B;您要新增元素的陣列。</li><li>值：要附加到陣列的元素。</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| join_arrays | 將陣列彼此結合。 | <ul><li>陣列：**Required**&#x200B;您要新增元素的陣列。</li><li>值：要附加到父陣列的陣列。</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;] |
| to_array | 獲取輸入清單並將其轉換為陣列。 | <ul><li>INCLUDE_NULLS:**Required**&#x200B;指示是否在響應陣列中包含空值的布爾值。</li><li>值：**必需**&#x200B;要轉換為陣列的元素。</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### 邏輯運算子{#logical-operators}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 解碼 | 給定一個鍵和一個作為陣列平面化的鍵值對清單，如果找到鍵，該函式將返回該值，如果在陣列中存在，則返回預設值。 | <ul><li>索引鍵：**必要**&#x200B;要匹配的密鑰。</li><li>OPTIONS:**必要**&#x200B;鍵／值對的平面化陣列。 （可選）預設值可以放在結尾。</li></ul> | decode(KEY,OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennylvania&quot;, &quot;N/A&quot;) | 如果stateCode是&quot;ca&quot;，則為&quot;California&quot;。<br>如果給定的stateCode是&quot;pa&quot;，則為&quot;Pennylvania&quot;。<br>如果stateCode不符合下列項目，則為&quot;N/A&quot;。 |
| if | 評估給定的布爾表達式，並根據結果返回指定的值。 | <ul><li>運算式：**必要**&#x200B;正在評估的布林運算式。</li><li>TRUE_VALUE:**必要**&#x200B;運算式評估為true時傳回的值。</li><li>FALSE_VALUE:**必要**&#x200B;運算式評估為false時傳回的值。</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | if(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### 彙總 {#aggregation}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 返回給定參數的最小值。 使用自然排序。 | <ul><li>OPTIONS:**Required**&#x200B;一個或多個可相互比較的對象。</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 返回給定參數的最大值。 使用自然排序。 | <ul><li>OPTIONS:**Required**&#x200B;一個或多個可相互比較的對象。</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### 類型轉換{#type-conversions}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 將字串轉換為BigInteger。 | <ul><li>字串：**Required**&#x200B;要轉換為BigInteger的字串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;100000.34&quot;) | 100000.34 |
| to_decimal | 將字串轉換為Double。 | <ul><li>字串：**必要**&#x200B;要轉換為Double的字串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 將字串轉換為浮點數。 | <ul><li>字串：**Required**&#x200B;要轉換為浮點數的字串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 將字串轉換為整數。 | <ul><li>字串：**必要**&#x200B;要轉換為整數的字串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON函式{#json}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 從指定字串反序列化JSON內容。 | <ul><li>字串：**必要**&#x200B;要取消序列化的JSON字串。</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; :&quot;Doe&quot;}) | 表示JSON的物件。 |

{style=&quot;table-layout:auto&quot;}

### 特殊操作{#special-operations}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /&lt;a0/ guid<br> | 產生偽隨機ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### 用戶代理函式{#user-agent}

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 從用戶代理字串中提取作業系統名稱。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | iOS |
| ua_os_version_major | 從用戶代理字串中提取作業系統的主要版本。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | iOS 5 |
| ua_os_version | 從用戶代理字串中提取作業系統的版本。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | 5.1.1 |
| ua_os_name_version | 從用戶代理字串中提取作業系統的名稱和版本。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | iOS 5.1.1 |
| ua_agent_version | 從用戶代理字串中提取代理版本。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | 5.1 |
| ua_agent_version_major | 從用戶代理字串中提取代理名稱和主版本。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | Safari 5 |
| ua_agent_name | 從用戶代理字串中提取代理名。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | Safari |
| ua_device_class | 從用戶代理字串中提取設備類。 | <ul><li>USER_AGENT:**必要**&#x200B;使用者代理字串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英吋) | 電話 |

{style=&quot;table-layout:auto&quot;}
