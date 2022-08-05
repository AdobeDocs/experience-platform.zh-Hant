---
keywords: Experience Platform；首頁；熱門主題；映射csv；映射csv；將csv檔案映射到xdm；將csv映射到xdm;ui指南；映射；映射欄位；映射函式；
solution: Experience Platform
title: 資料準備映射函式
topic-legacy: overview
description: 本文檔介紹了與資料準備一起使用的映射功能。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: a48072d2c418588a05397e991c1a2e17eee4c028
workflow-type: tm+mt
source-wordcount: '4286'
ht-degree: 3%

---

# 資料準備映射函式

資料準備函式可用於根據在源欄位中輸入的內容計算和計算值。

## 欄位

欄位名稱可以是任何合法標識符 — Unicode字母和數字的無限長序列，以字母、美元符號開頭(`$`)，或下划線字元(`_`)。 變數名稱也區分大小寫。

如果欄位名不遵循此約定，則必須用 `${}`。 因此，例如，如果欄位名稱是&quot;First Name&quot;或&quot;First.Name&quot;，則必須將該名稱換成 `${First Name}` 或 `${First.Name}` 分別進行。

此外，如果欄位名稱 **任何** 在以下保留關鍵字中，必須用 `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

子域內的資料可以使用點表示法訪問。 例如，如果 `name` 對象，訪問 `firstName` 欄位，使用 `name.firstName`。

## 函式清單

下表列出了所有支援的映射函式，包括示例表達式及其結果輸出。

### 字串函式 {#string}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 連接給定字串。 | <ul><li>字串：將連接的字串。</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;the&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 爆炸 | 根據規則運算式拆分字串並返回一組部件。 可以選擇包括regex以拆分字串。 預設情況下，拆分解析為「，」。 以下分隔符 **需要** 要一起逃跑 `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` 如果包含多個字元作為分隔符，則分隔符將被視為多字元分隔符。 | <ul><li>字串： **必需** 需要拆分的字串。</li><li>規則運算式： *可選* 可用於拆分字串的規則運算式。</li></ul> | explode(STRING, REGEX) | explode（&quot;你好！&quot;, &quot;） | `["Hi,", "there"]` |
| 安裝 | 返回子字串的位置/索引。 | <ul><li>輸入： **必需** 正在搜索的字串。</li><li>子字串： **必需** 在字串中搜索的子字串。</li><li>開始位置(_P): *可選* 在字串中開始查找的位置。</li><li>具體值： *可選* 要從起始位置查找的第n個出現。 預設情況下為1。 </li></ul> | instr(INPUT、SUBSTRING、START_POSITION、OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| 更換 | 如果原始字串中存在，則替換搜索字串。 | <ul><li>輸入： **必需** 輸入字串。</li><li>查找(_F): **必需** 要在輸入中查找的字串。</li><li>替換(_R): **必需** 將替換&quot;TO_FIND&quot;中值的字串。</li></ul> | replacestr(INPUT、TO_FIND、TO_REPLACE) | replacestr(&quot;這是字串retest&quot;、&quot;re&quot;、&quot;replace&quot;) | &quot;這是字串替換test&quot; |
| substr | 返回給定長度的子字串。 | <ul><li>輸入： **必需** 輸入字串。</li><li>START_INDEX: **必需** 子字串開始的輸入字串的索引。</li><li>長度： **必需** 子字串的長度。</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;這是子字串test&quot;, 7, 8) | &quot; a subst&quot; |
| 低/<br>案 | 將字串轉換為小寫。 | <ul><li>輸入： **必需** 將轉換為小寫的字串。</li></ul> | 低（輸入） | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;你好&quot; |
| 上<br>酶 | 將字串轉換為大寫。 | <ul><li>輸入： **必需** 將轉換為大寫的字串。</li></ul> | 上（輸入） | upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;你好&quot; |
| split | 在分隔符上拆分輸入字串。 以下分隔符 **需求** 要一起逃跑 `\`: `\`。 如果包含多個分隔符，則字串將拆分 **任何** 的子菜單。 | <ul><li>輸入： **必需** 要拆分的輸入字串。</li><li>分隔符： **必需** 用於拆分輸入的字串。</li></ul> | 拆分（輸入，分隔符） | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符聯接對象清單。 | <ul><li>分隔符： **必需** 將用於連接對象的字串。</li><li>對象： **必需** 要聯接的字串陣列。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;你好世界&quot; |
| lpad | 將字串的左側與另一給定字串相加。 | <ul><li>輸入： **必需** 要塞的繩子。 此字串可以為Null。</li><li>計數： **必需** 要填充的字串的大小。</li><li>填充： **必需** 用填充輸入的字串。 如果為空或空，則它將被視為單個空格。</li></ul> | lpad(INPUT、COUNT、PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | 將字串的右側與另一個給定字串相加。 | <ul><li>輸入： **必需** 要塞的繩子。 此字串可以為Null。</li><li>計數： **必需** 要填充的字串的大小。</li><li>填充： **必需** 用填充輸入的字串。 如果為空或空，則它將被視為單個空格。</li></ul> | rpad(INPUT、COUNT、PADDING) | rpad(&quot;bat&quot;、8、&quot;yz&quot;) | &quot;巴特茲&quot; |
| 左 | 獲取給定字串的前&quot;n&quot;個字元。 | <ul><li>字串： **必需** 您要獲取的第一個&quot;n&quot;字元的字串。</li><li>計數： **必需**&#x200B;要從字串獲取的&quot;n&quot;字元。</li></ul> | left（字串，計數） | left(&quot;abcde&quot;, 2 | &quot;ab&quot; |
| 右 | 獲取給定字串的最後一個&quot;n&quot;字元。 | <ul><li>字串： **必需** 要獲取的最後一個&quot;n&quot;字元的字串。</li><li>計數： **必需**&#x200B;要從字串獲取的&quot;n&quot;字元。</li></ul> | right（字串，COUNT） | right(&quot;abcde&quot;, 2 | &quot;de&quot; |
| 短線 | 從字串開頭刪除空白。 | <ul><li>字串： **必需** 要從中刪除空白的字串。</li></ul> | ltrim(STRING) | ltrim(&quot;hello&quot;) | &quot;你好&quot; |
| 修剪 | 從字串的末尾刪除空白。 | <ul><li>字串： **必需** 要從中刪除空白的字串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;你好&quot; |
| trim | 從字串的開頭和結尾刪除空格。 | <ul><li>字串： **必需** 要從中刪除空白的字串。</li></ul> | trim(STRING) | trim(&quot;hello &quot;) | &quot;你好&quot; |
| 等於 | 比較兩個字串以確認它們是否相等。 此函式區分大小寫。 | <ul><li>STRING1: **必需** 要比較的第一個字串。</li><li>STRING2: **必需** 要比較的第二個字串。</li></ul> | 字串1&#x200B;。equals(&#x200B;STRING2) | &quot;string1&quot; &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比較兩個字串以確認它們是否相等。 此函式為 **不** 區分大小寫。 | <ul><li>STRING1: **必需** 要比較的第一個字串。</li><li>STRING2: **必需** 要比較的第二個字串。</li></ul> | 字串1&#x200B;。equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot; &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### 規則運算式函式

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 抽取_regex | 根據規則運算式從輸入字串中提取組。 | <ul><li>字串： **必需** 從中提取組的字串。</li><li>規則運算式： **必需** 希望組匹配的規則運算式。</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)」) | [&quot;E259,E259B_009,1_1&quot;,&quot;E259&quot;,&quot;1_1&quot;] |
| 匹配_regex | 檢查字串是否與輸入的規則運算式匹配。 | <ul><li>字串： **必需** 您正在檢查的字串與規則運算式匹配。</li><li>規則運算式： **必需** 您所比較的規則運算式。</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)」) | 真 |

{style=&quot;table-layout:auto&quot;&quot;

### 散列函式 {#hashing}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 沙1 | 使用安全散列算法1(SHA-1)獲取輸入並生成散列值。 | <ul><li>輸入： **必需** 要散列的純文字檔案。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT、CHARSET) | sha1(&quot;my text&quot;、&quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B;48690840c5dfcce3c80 |
| 沙256 | 使用安全散列算法256(SHA-256)獲取輸入並生成散列值。 | <ul><li>輸入： **必需** 要散列的純文字檔案。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;、&quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 ee6a39af&#x200B;698154a83a586ee270a0d372104 |
| 沙512 | 使用安全散列算法512(SHA-512)獲取輸入並生成散列值。 | <ul><li>輸入： **必需** 要散列的純文字檔案。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512（輸入、字元集） | sha512(&quot;my text&quot;、&quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B;708bf11b4232bb21d2a8704ada2cd7b367dd078a89 &#x200B;a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | 使用MD5獲取輸入並生成散列值。 | <ul><li>輸入： **必需** 要散列的純文字檔案。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5（輸入、字元集） | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B;e9bd0198d03ba6852c7 |
| 32哥斯大黎加科朗 | 輸入使用循環冗餘校驗(CRC)算法來生成32位循環碼。 | <ul><li>輸入： **必需** 要散列的純文字檔案。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | CRC32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;&quot;

### URL函式 {#url}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 從給定URL返回協定。 如果輸入無效，則返回null。 | <ul><li>URL: **必需** 需要從中提取協定的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 返回給定URL的主機。 如果輸入無效，則返回null。 | <ul><li>URL: **必需** 需要從中提取主機的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform &#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 返回給定URL的埠。 如果輸入無效，則返回null。 | <ul><li>URL: **必需** 需要從中提取埠的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 返回給定URL的路徑。 預設情況下，返回完整路徑。 | <ul><li>URL: **必需** 需要從中提取路徑的URL。</li><li>完整路徑(_P): *可選* 一個布爾值，它確定是否返回完整路徑。 如果設定為false，則只返迴路徑的結尾。</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | 返回給定URL的查詢字串，作為查詢字串名稱和查詢字串值的映射。 | <ul><li>URL: **必需** 您試圖從中獲取查詢字串的URL。</li><li>錨點： **必需** 確定將對查詢字串中的錨點執行什麼操作。 可以是三個值之一：&quot;retain&quot;、&quot;remove&quot;或&quot;append&quot;。<br><br>如果值為「retain」，則錨點將附加到返回的值。<br>如果值為&quot;remove&quot;，則錨點將從返回的值中刪除。<br>如果值為「append」，則錨點將作為單獨的值返回。</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;retain&quot;<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;<br>get_url_query_str&#x200B;(&quot;foo://example.com &#x200B;:8042/over/the&#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;&quot;

### 日期和時間函式 {#date-and-time}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。 有關 `date` 函式可在 [資料格式處理指南](./data-handling.md#dates)。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 檢索當前時間。 |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | 檢索當前Unix時間。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式設定輸入日期的格式。 | <ul><li>日期： **必需** 要格式化的輸入日期（作為ZonedDateTime對象）。</li><li>格式： **必需** 要將日期更改為的格式。</li></ul> | 格式（日期，格式） | 格式(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH&quot;:mm:ss&quot;) | `2019-10-23 11:24:35` |
| 格式 | 根據指定的格式將時間戳轉換為日期字串。 | <ul><li>時間戳： **必需** 要格式化的時間戳。 此操作以毫秒為單位。</li><li>格式： **必需** 希望時間戳成為的格式。</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX」) | `2019-10-23T11:24:35.000Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字串。</li><li>格式： **必需** 表示源日期格式的字串。**注：** 這是 **不** 表示要將日期字串轉換為的格式。 </li><li>預設日期： **必需** 如果提供的日期為空，則返回預設日期。</li></ul> | date(DATE、FORMAT、DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字串。</li><li>格式： **必需** 表示源日期格式的字串。**注：** 這是 **不** 表示要將日期字串轉換為的格式。 </li></ul> | 日期（日期，格式） | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字串。</li></ul> | 日期（日期） | 日期(&quot;2019-10-23 11:24&quot;) | 「2019-10-23T11:24:00Z」 |
| 日期/部分 | 檢索日期的部分。 支援以下元件值： <br><br>&quot;年&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;季度&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;月&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;日常年&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;天&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;周&quot;<br>&quot;w&quot;<br>&quot;w&quot;<br><br>&quot;工作日&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;小時&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;分鐘&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;第二&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;毫秒&quot;<br>&quot;ms&quot; | <ul><li>元件： **必需** 表示日期部分的字串。 </li><li>日期： **必需** 日期，採用標準格式。</li></ul> | date_part&#x200B;（元件，日期） | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12英吋)) | 10 |
| set_date_part | 在給定日期替換元件。 接受以下元件： <br><br>&quot;年&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;月&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;天&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;小時&quot;<br>&quot;hh&quot;<br><br>&quot;分鐘&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;第二&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>元件： **必需** 表示日期部分的字串。 </li><li>值： **必需** 為給定日期的元件設定的值。</li><li>日期： **必需** 日期，採用標準格式。</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797英吋) | 「2016-04-09T11:44:44Z」 |
| make_date_time | 從部件建立日期。 此函式也可以使用make_timestamp來誘導。 | <ul><li>年： **必需** 年份，以四位數字寫。</li><li>月： **必需** 月份。 允許的值為1到12。</li><li>日： **必需** 那天。 允許的值為1到31。</li><li>小時： **必需** 時間。 允許的值為0到23。</li><li>分鐘： **必需** 一分鐘。 允許的值為0到59。</li><li>納秒： **必需** 納秒值。 允許的值為0到99999999。</li><li>時區： **必需** 日期時間的時區。</li></ul> | make_date_time&#x200B;(YEAR、MONTH、DAY、HOUR、MINUTE、SECOND、NS、TIMEZONE) | make_date_time&#x200B;(2019、10、17、11、55、12、999，「America/Los_Angeles」) | `2019-10-17T11:55:12Z` |
| 區域_日期_到utc | 將任意時區中的日期轉換為UTC中的日期。 | <ul><li>日期： **必需** 您嘗試轉換的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 將日期從一個時區轉換為另一個時區。 | <ul><li>日期： **必需** 您嘗試轉換的日期。</li><li>區域： **必需** 您嘗試將日期轉換為的時區。</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### 層次 — 對象 {#objects}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 為空 | 檢查對象是否為空。 | <ul><li>輸入： **必需** 您嘗試檢查的對象為空。</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | 假 |
| 陣列_到對象 | 建立對象清單。 | <ul><li>輸入： **必需** 鍵對和陣列對的分組。</li></ul> | arrays_to_object(INPUT) | 需要樣本 | 需要樣本 |
| 到對象 | 根據給定的平面鍵/值對建立對象。 | <ul><li>輸入： **必需** 鍵/值對的平面清單。</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;、&quot;John&quot;、&quot;lastName&quot;、&quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 從輸入字串建立對象。 | <ul><li>字串： **必需** 正在分析以建立對象的字串。</li><li>VALUE_DELIMITER: *可選* 分隔欄位與值的分隔符。 預設分隔符為 `:`。</li><li>欄位分隔符： *可選* 分隔欄位值對的分隔符。 預設分隔符為 `,`。</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName=John,lastName=Doe,phone=123 456 7890&quot;, &quot;=&quot;, &quot;,&quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| 包含鍵 | 檢查源資料中是否存在對象。 **注：** 此函式替換已棄用 `is_set()` 的子菜單。 | <ul><li>輸入： **必需** 如果源資料中存在要檢查的路徑。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | 真 |
| 取消 | 將屬性值設定為 `null`。 當您不想將欄位複製到目標架構時，應使用此選項。 |  | nullify() | nullify() | `null` |
| 獲取密鑰 | 解析鍵/值對並返回所有鍵。 | <ul><li>對象： **必需** 將從中提取鍵的對象。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;):《傲慢與偏見》，《第二本書》：「1984」) | `["book1", "book2"]` |
| get_values | 解析鍵/值對並根據給定鍵返回字串的值。 | <ul><li>字串： **必需** 要分析的字串。</li><li>密鑰： **必需** 必須提取值的鍵。</li><li>VALUE_DELIMITER: **必需** 分隔欄位和值的分隔符。 如果 `null` 或提供空字串，此值為 `:`。</li><li>欄位分隔符： *可選* 分隔欄位和值對的分隔符。 如果 `null` 或提供空字串，此值為 `,`。</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values（\&quot;firstName - John,lastName - Cena，電話 — 555 420 8692\&quot;, \&quot;-\&quot;, \&quot;,\&quot;） | 約翰 |

{style=&quot;table-layout:auto&quot;&quot;

有關對象複製功能的資訊，請參見一節 [下](#object-copy)。

### 層次 — 陣列 {#arrays}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 凝聚 | 返回給定陣列中的第一個非空對象。 | <ul><li>輸入： **必需** 要查找的第一個非空對象的陣列。</li></ul> | 合併(INPUT) | coalesce(null、null、null、null、&quot;first&quot;、null、&quot;second&quot;) | &quot;第一個&quot; |
| 第一 | 檢索給定陣列的第一個元素。 | <ul><li>輸入： **必需** 要查找的第一個元素的陣列。</li></ul> | 第一個（輸入） | first(&quot;1&quot;、&quot;2&quot;、&quot;3&quot;) | &quot;1&quot; |
| 最後 | 檢索給定陣列的最後一個元素。 | <ul><li>輸入： **必需** 要查找的最後一個元素的陣列。</li></ul> | last(INPUT) | last(&quot;1&quot;、&quot;2&quot;、&quot;3&quot; | &quot;3&quot; |
| 添加到陣列 | 將元素添加到陣列的末尾。 | <ul><li>陣列： **必需** 要添加元素的陣列。</li><li>值：要追加到陣列的元素。</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | 添加到陣列&#x200B;([「a」、「b」], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| 連接陣列 | 將陣列相互組合。 | <ul><li>陣列： **必需** 要添加元素的陣列。</li><li>值：要追加到父陣列的陣列。</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | join_arrays&#x200B;([「a」、「b」]。 [&#39;c&#39;]。 [「d」、「e」]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| 到陣列 | 獲取輸入清單並將其轉換為陣列。 | <ul><li>INCLUDE_NULLS: **必需** 一個布爾值，用於指示是否在響應陣列中包括空值。</li><li>值： **必需** 要轉換為陣列的元素。</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1,null, 2, 3) | `[1, 2, 3]` |
| 大小 | 返回輸入的大小。 | <ul><li>輸入： **必需** 您嘗試查找的對象大小。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函式用於將整個輸入陣列中的所有元素附加到Profile中陣列的末尾。 此函式為 **僅** 在更新期間適用。 如果在插入的上下文中使用，此函式將按原樣返回輸入。 | <ul><li>陣列： **必需** 要在配置檔案中追加陣列的陣列。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123、456] |
| upsert_array_replace | 此函式用於替換陣列中的元素。 此函式為 **僅** 在更新期間適用。 如果在插入的上下文中使用，此函式將按原樣返回輸入。 | <ul><li>陣列： **必需** 要替換配置檔案中的陣列的陣列。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123、456] |

{style=&quot;table-layout:auto&quot;&quot;

### 邏輯運算子 {#logical-operators}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 解碼 | 如果給定一個鍵和一個按陣列拼合的鍵值對清單，則函式將在找到鍵時返回值，或在陣列中存在時返回預設值。 | <ul><li>密鑰： **必需** 要匹配的密鑰。</li><li>OPTIONS: **必需** 鍵/值對的拼合陣列。 （可選）可以在結尾處放置預設值。</li></ul> | decode(KEY,OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 如果給定的stateCode是&quot;ca&quot;, &quot;California&quot;。<br>如果給定的stateCode是&quot;pa&quot;, &quot;Pennsylvania&quot;。<br>如果stateCode與以下項不匹配，則「N/A」。 |
| 如果 | 計算給定的布爾表達式並根據結果返回指定的值。 | <ul><li>表達式： **必需** 正在計算的布爾表達式。</li><li>TRUE_VALUE: **必需** 如果表達式的計算結果為true，則返回的值。</li><li>FALSE_VALUE: **必需** 如果表達式的計算結果為false，則返回的值。</li></ul> | iif(EXPRESSION、TRUE_VALUE、FALSE_VALUE) | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)、&quot;True&quot;、&quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;&quot;

### 彙總 {#aggregation}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 返回給定參數的最小值。 使用自然排序。 | <ul><li>OPTIONS: **必需** 可以相互比較的一個或多個對象。</li></ul> | min(OPTIONS) | min(3、1、4) | 1 |
| max | 返回給定參數的最大值。 使用自然排序。 | <ul><li>OPTIONS: **必需** 可以相互比較的一個或多個對象。</li></ul> | 最大(OPTIONS) | 最大值(3、1、4) | 4 |

{style=&quot;table-layout:auto&quot;&quot;

### 類型轉換 {#type-conversions}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 到 | 將字串轉換為BigInteger。 | <ul><li>字串： **必需** 要轉換為BigInteger的字串。</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| 到十進位 | 將字串轉換為Double。 | <ul><li>字串： **必需** 要轉換為Double的字串。</li></ul> | to_decimal（字串） | to_decimal(&quot;20.5&quot;) | 二十點五 |
| 至浮點 | 將字串轉換為浮點。 | <ul><li>字串： **必需** 要轉換為浮點的字串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| 到整數 | 將字串轉換為整數。 | <ul><li>字串： **必需** 要轉換為整數的字串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;&quot;

### JSON函式 {#json}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to對象 | 從給定字串反序列化JSON內容。 | <ul><li>字串： **必需** 要反序列化的JSON字串。</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;:&quot;Doe&quot;}) | 表示JSON的對象。 |

{style=&quot;table-layout:auto&quot;&quot;

### 特別行動 {#special-operations}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid/uuid<br>GUID | 生成偽隨機ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

{style=&quot;table-layout:auto&quot;&quot;

### 用戶代理函式 {#user-agent}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 示例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 從用戶代理字串中提取作業系統名稱。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 從用戶代理字串中提取作業系統的主要版本。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B;s(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 從用戶代理字串中提取作業系統的版本。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 從用戶代理字串中提取作業系統的名稱和版本。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 從用戶代理字串中提取代理版本。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 從用戶代理字串中提取代理名稱和主要版本。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 從用戶代理字串中提取代理名稱。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 從用戶代理字串中提取設備類。 | <ul><li>USER_AGENT: **必需** 用戶代理字串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0(iPhone;CPUiPhoneOS 5_1_1如MacOS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 電話 |

{style=&quot;table-layout:auto&quot;&quot;

### 對象副本 {#object-copy}

>[!TIP]
>
>當源中的對象映射到XDM中的對象時，將自動應用對象複製功能。 用戶無需執行其他操作。

可以使用對象複製功能自動複製對象的屬性，而不對映射進行更改。 例如，如果源資料的結構為：

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

以及XDM結構：

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

然後，映射變為：

```json
address -> addr
address.line1 -> addr.addrLine1
```

在上例中， `city` 和 `state` 屬性也會在運行時自動攝取，因為 `address` 對象映射到 `addr`。 如果要建立 `line2` XDM結構中的屬性，您的輸入資料還包含 `line2` 的 `address` 對象，則也會自動攝入該對象，而無需手動更改映射。

要確保自動映射工作，必須滿足以下先決條件：

* 應映射父級對象；
* 必須在XDM架構中建立新屬性；
* 新屬性在源架構和XDM架構中應具有匹配的名稱。

如果未滿足任何先決條件，則必須使用資料準備手動將源架構映射到XDM架構。