---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm;ui指南；對應程式；對應；對應欄位；對應函式；
solution: Experience Platform
title: 資料準備映射函式
description: 本文檔介紹與資料準備一起使用的映射函式。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: da7eff7966679635efa71cbbd33768ef4f412241
workflow-type: tm+mt
source-wordcount: '4557'
ht-degree: 3%

---

# 資料準備映射函式

資料準備函式可用於根據在源欄位中輸入的內容計算和計算值。

## 欄位

欄位名稱可以是任何法律識別碼 — Unicode字母和數字的無限長序列，以字母開頭，貨幣符號(`$`)或底線字元(`_`)。 變數名稱也區分大小寫。

如果欄位名稱未遵循此慣例，則欄位名稱必須以包住 `${}`. 因此，例如，如果欄位名稱為「名字」或「名字」，則名稱必須包裝如下 `${First Name}` 或 `${First\.Name}` 分別為5個。

>[!TIP]
>
>與階層互動時，如果子屬性具有句點(`.`)，您必須使用反斜線(`\`)以逸出特殊字元。 如需詳細資訊，請參閱 [逸出特殊字元](home.md#escape-special-characters).

此外，如果欄位名稱為 **any** 在下列保留的關鍵字中，必須將其包住 `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

子欄位內的資料可使用點記號來存取。 例如，如果 `name` 對象，訪問 `firstName` 欄位，使用 `name.firstName`.

## 函式清單

下表列出所有支援的映射函式，包括示例表達式及其產生的輸出。

### 字串函式 {#string}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 串連指定的字串。 | <ul><li>字串：將串連的字串。</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 爆炸 | 根據規則運算式分割字串，並傳回一組部分。 可選擇包含分割字串的規則運算式。 依預設，拆分解析為「，」。 下列分隔字元 **需要** 被逸出 `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` 如果您包含多個字元作為分隔字元，分隔字元將視為多字元分隔字元。 | <ul><li>字串： **必填** 需要拆分的字串。</li><li>REGEX: *可選* 可用來分割字串的規則運算式。</li></ul> | explode（字串， REGEX） | explode（&quot;嗨，那兒！&quot;, &quot; &quot;） | `["Hi,", "there"]` |
| instr | 傳回子字串的位置/索引。 | <ul><li>輸入： **必填** 正在搜尋的字串。</li><li>子字串： **必填** 在字串內搜尋的子字串。</li><li>START_POSITION: *可選* 要開始查看字串的位置。</li><li>發生次數： *可選* 要從開始位置尋找的第n個出現次數。 預設為1。 </li></ul> | instr（INPUT，子字串， START_POSITION, OCCURRENCE） | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 如果原始字串中存在，則替換搜索字串。 | <ul><li>輸入： **必填** 輸入字串。</li><li>TO_FIND: **必填** 要在輸入內查詢的字串。</li><li>TO_REPLACE: **必填** 將替換&quot;TO_FIND&quot;中值的字串。</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr（&quot;這是字串re test&quot;、&quot;re&quot;、&quot;replace&quot;） | &quot;這是字串替換測試&quot; |
| substr | 傳回指定長度的子字串。 | <ul><li>輸入： **必填** 輸入字串。</li><li>START_INDEX: **必填** 子字串開始的輸入字串的索引。</li><li>長度： **必填** 子字串的長度。</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr（&quot;這是子字串測試&quot;, 7, 8） | &quot; a subst&quot; |
| lower /<br>lcase | 將字串轉換為小寫。 | <ul><li>輸入： **必填** 將轉換為小寫的字串。</li></ul> | lower(INPUT) | lower(&quot;HeLo&quot;)<br>lcase(&quot;HeLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | 將字串轉換為大寫。 | <ul><li>輸入： **必填** 將轉換為大寫的字串。</li></ul> | upper(INPUT) | upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLo&quot;) | &quot;HELLO&quot; |
| split | 在分隔符上分割輸入字串。 下列分隔符號 **需求** 被逸出 `\`: `\`. 如果您包含多個分隔字元，字串將依 **any** 字串中顯示的分隔字元。 | <ul><li>輸入： **必填** 即將分割的輸入字串。</li><li>分隔符： **必填** 用於分割輸入的字串。</li></ul> | 拆分（輸入，分隔符） | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符聯接對象清單。 | <ul><li>分隔符： **必填** 將用於連接對象的字串。</li><li>對象： **必填** 要連結的字串陣列。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | 「你好世界」 |
| lpad | 將字串的左側與另一個指定字串固定。 | <ul><li>輸入： **必填** 被補出來的繩子。 此字串可以為null。</li><li>計數： **必填** 要填補的字串大小。</li><li>邊框間距： **必填** 用填充輸入的字串。 如果為空或空，則會將其視為單一空格。</li></ul> | lpad（輸入，計數，填充） | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | 將字串的右側與另一個指定字串固定。 | <ul><li>輸入： **必填** 被補出來的繩子。 此字串可以為null。</li><li>計數： **必填** 要填補的字串大小。</li><li>邊框間距： **必填** 用填充輸入的字串。 如果為空或空，則會將其視為單一空格。</li></ul> | rpad（輸入，計數，填充） | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| lef | 取得指定字串的第一個&quot;n&quot;字元。 | <ul><li>字串： **必填** 您要取得的第一個&quot;n&quot;字元的字串。</li><li>計數： **必填**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | left（字串，計數） | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| 右 | 取得指定字串的最後&quot;n&quot;個字元。 | <ul><li>字串： **必填** 您要取得的最後一個&quot;n&quot;字元的字串。</li><li>計數： **必填**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | right（字串，計數） | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | 從字串的開頭移除空白字元。 | <ul><li>字串： **必填** 您要移除空格的字串。</li></ul> | ltrim(STRING) | ltrim(&quot;hello&quot;) | &quot;hello&quot; |
| rtrim | 移除字串結尾的空白字元。 | <ul><li>字串： **必填** 您要移除空格的字串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | 從字串的開頭和結尾移除空白字元。 | <ul><li>字串： **必填** 您要移除空格的字串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 等於 | 比較兩個字串以確認其是否相等。 此函式區分大小寫。 | <ul><li>字串1: **必填** 您要比較的第一個字串。</li><li>字串2: **必填** 您要比較的第二個字串。</li></ul> | 字串1&#x200B;.equals(&#x200B;STRING2) | &quot;string1&quot;&#x200B;。等於&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比較兩個字串以確認其是否相等。 此函式為 **not** 區分大小寫。 | <ul><li>字串1: **必填** 您要比較的第一個字串。</li><li>字串2: **必填** 您要比較的第二個字串。</li></ul> | 字串1&#x200B;.equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;&#x200B;。equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### 規則運算式函式

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根據規則運算式從輸入字串中擷取群組。 | <ul><li>字串： **必填** 從中提取組的字串。</li><li>REGEX: **必填** 您要群組相符的規則運算式。</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)」) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | 檢查字串是否與輸入的規則運算式相符。 | <ul><li>字串： **必填** 您要檢查的字串與規則運算式相符。</li><li>REGEX: **必填** 要比較的規則運算式。</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)」) | true |

{style="table-layout:auto"}

### 雜湊函式 {#hashing}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 使用安全雜湊演算法1(SHA-1)取用輸入並產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B;48690840c5dfcce3c80 |
| sha256 | 使用安全雜湊演算法256(SHA-256)取用輸入並產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256（輸入，字元集） | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 使用安全雜湊演算法512(SHA-512)取用輸入並產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512（輸入，字元集） | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B;708bf11b4232bb21d2a8704ada2cdd7b367dd0788a89&#x200B;a5c908cfe377b1072a7ff7b36d8a8fd24d16 |
| md5 | 取用輸入，並使用MD5產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5（輸入，字元集） | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B;e9bd0198d03ba6852c7 |
| crc32 | 取用輸入使用循環冗餘校驗(CRC)算法來產生32位循環碼。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### URL函式 {#url}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 從指定URL傳回通訊協定。 如果輸入無效，則返回null。 | <ul><li>URL: **必填** 需要擷取通訊協定的URL。</li></ul> | get_url_protocol(&#x200B;URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 傳回指定URL的主機。 如果輸入無效，則返回null。 | <ul><li>URL: **必填** 需要擷取主機的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host(&#x200B;&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 傳回指定URL的連接埠。 如果輸入無效，則返回null。 | <ul><li>URL: **必填** 需要擷取連接埠的URL。</li></ul> | get_url_port(URL) | get_url_port(&#x200B;&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 傳回指定URL的路徑。 依預設，會傳回完整路徑。 | <ul><li>URL: **必填** 需要擷取路徑的URL。</li><li>完整路徑(_P): *可選* 一個布林值，它確定是否返回完整路徑。 若設為false，則只會傳迴路徑的結尾。</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;/home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | 傳回指定URL的查詢字串，作為查詢字串名稱和查詢字串值的映射。 | <ul><li>URL: **必填** 您嘗試從中取得查詢字串的URL。</li><li>錨點： **必填** 決定要對查詢字串中的錨點執行什麼動作。 可以是三個值的其中之一：&quot;retain&quot;、&quot;remove&quot;或&quot;append&quot;。<br><br>如果值為「retain」，則錨點會附加至傳回的值。<br>如果值為「remove」，則會從傳回值中移除錨點。<br>如果值為「append」，則錨點會以個別值傳回。</li></ul> | get_url_query_str(&#x200B;URL，錨點) | get_url_query_str(&#x200B;&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;retain&quot;<br>get_url_query_str(&#x200B;&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;<br>get_url_query_str&#x200B;(&quot;foo://example.com &#x200B;:8042/over/thre &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | 此函式以URL作為輸入，並以ASCII字元替換或編碼特殊字元。 有關特殊字元的詳細資訊，請閱讀 [特殊字元清單](#special-characters) 在本檔案附錄中。 | <ul><li>URL: **必填** 輸入URL，其中包含您要替換的特殊字元，或用ASCII字元進行編碼。</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022」) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | 此函式會將URL視為輸入，並將ASCII字元解碼為特殊字元。  有關特殊字元的詳細資訊，請閱讀 [特殊字元清單](#special-characters) 在本檔案附錄中。 | <ul><li>URL: **必填** 要解碼為特殊字元的ASCII字元的輸入URL。</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### 日期和時間函式 {#date-and-time}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。 有關 `date` 函式，可在 [資料格式處理指南](./data-handling.md#dates).

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 擷取目前時間。 |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | 檢索當前Unix時間。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式設定輸入日期的格式。 | <ul><li>日期： **必填** 要格式化的輸入日期（作為ZonedDateTime對象）。</li><li>格式： **必填** 您要將日期變更為的格式。</li></ul> | 格式（日期，格式） | 格式(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | 根據指定格式將時間戳轉換為日期字串。 | <ul><li>時間戳： **必填** 要格式化的時間戳記。 這會以毫秒為單位寫入。</li><li>格式： **必填** 您希望時間戳記變成的格式。</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;THH:mm:ss.SSX」) | `2019-10-23T11:24:35.000Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li><li>格式： **必填** 代表來源日期格式的字串。**注意：** 確實如此 **not** 代表您要將日期字串轉換為的格式。 </li><li>DEFAULT_DATE: **必填** 如果提供的日期為空，則返回預設日期。</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li><li>格式： **必填** 代表來源日期格式的字串。**注意：** 確實如此 **not** 代表您要將日期字串轉換為的格式。 </li></ul> | 日期（日期，格式） | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime對象（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li></ul> | 日期（日期） | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11&quot;:24:00Z」 |
| date_part | 擷取日期的部分。 支援下列元件值： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;毫秒&quot;<br>&quot;SSS&quot; | <ul><li>元件： **必填** 代表日期部分的字串。 </li><li>日期： **必填** 日期，採用標準格式。</li></ul> | date_part(&#x200B;元件，日期) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12英吋) | 10 |
| set_date_part | 在指定日期中取代元件。 接受下列元件： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>元件： **必填** 代表日期部分的字串。 </li><li>值： **必填** 為指定日期的元件設定的值。</li><li>日期： **必填** 日期，採用標準格式。</li></ul> | set_date_part(&#x200B;元件，值，日期) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797″) | &quot;2016-04-09T11&quot;:44:44Z」 |
| make_date_time | 從零件建立日期。 您也可以使用make_timestamp來誘導此函式。 | <ul><li>年： **必填** 以四位數寫的年份。</li><li>月： **必填** 月份。 允許的值是1到12。</li><li>日： **必填** 那天。 允許的值是1到31。</li><li>小時： **必填** 那個小時。 允許的值為0到23。</li><li>分鐘： **必填** 分鐘。 允許的值為0到59。</li><li>納秒： **必填** 納秒值。 允許的值為0到999999999。</li><li>時區： **必填** 日期時間的時區。</li></ul> | make_date_time(&#x200B;年、月、日、小時、分鐘、秒、納秒、時區) | make_date_time(&#x200B;2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 將任何時區的日期轉換為UTC的日期。 | <ul><li>日期： **必填** 您嘗試轉換的日期。</li></ul> | zone_date_to_utc(&#x200B;DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 將日期從一個時區轉換為另一個時區。 | <ul><li>日期： **必填** 您嘗試轉換的日期。</li><li>區域： **必填** 您嘗試將日期轉換為的時區。</li></ul> | zone_date_to_zone(&#x200B;DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### 層次 — 對象 {#objects}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 檢查對象是否為空。 | <ul><li>輸入： **必填** 您要檢查的對象為空。</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 建立對象清單。 | <ul><li>輸入： **必填** 密鑰對和陣列對的分組。</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 根據給定的平面索引鍵/值配對建立對象。 | <ul><li>輸入： **必填** 索引鍵/值組的平面清單。</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 從輸入字串建立物件。 | <ul><li>字串： **必填** 正在解析以建立對象的字串。</li><li>VALUE_DELIMITER: *可選* 將欄位與值分開的分隔字元。 預設分隔字元為 `:`.</li><li>FIELD_DELIMITER: *可選* 分隔欄位值組的分隔字元。 預設分隔字元為 `,`.</li></ul> | str_to_object(&#x200B;字串， VALUE_DELIMITER, FIELD_DELIMITER) **附註**:您可以使用 `get()` 函式與 `str_to_object()` 來擷取字串中索引鍵的值。 | <ul><li>範例#1:str_to_object(&quot;firstName - John ;lastName - ;- 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>範例#2:str_to_object(&quot;firstName - John ;lastName - ;phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;)。get(&quot;firstName&quot;)</li></ul> | <ul><li>範例#1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>範例#2:「約翰」</li></ul> |
| contains_key | 檢查對象是否存在於源資料中。 **注意：** 此函式會取代已棄用的 `is_set()` 函式。 | <ul><li>輸入： **必填** 要檢查的路徑（如果它存在於源資料中）。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 取消 | 將屬性的值設定為 `null`. 當您不想將欄位複製到目標架構時，應使用此欄位。 |  | nullify() | nullify() | `null` |
| get_keys | 剖析索引鍵/值組並傳回所有索引鍵。 | <ul><li>對象： **必填** 將從中擷取鍵值的物件。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;):《傲慢與偏見》、《書2》：《1984年》) | `["book1", "book2"]` |
| get_values | 分析索引鍵/值配對，並根據指定索引鍵傳回字串的值。 | <ul><li>字串： **必填** 要分析的字串。</li><li>索引鍵： **必填** 必須擷取值的索引鍵。</li><li>VALUE_DELIMITER: **必填** 分隔欄位和值的分隔字元。 若 `null` 或空白字串，則此值為 `:`.</li><li>FIELD_DELIMITER: *可選* 分隔欄位和值組的分隔字元。 若 `null` 或空白字串，則此值為 `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | 約翰 |

{style="table-layout:auto"}

有關對象複製功能的資訊，請參閱 [low](#object-copy).

### 階層 — 陣列 {#arrays}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 合併 | 傳回指定陣列中的第一個非空物件。 | <ul><li>輸入： **必填** 要查找的第一個非空對象的陣列。</li></ul> | 合併（輸入） | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | 擷取指定陣列的第一個元素。 | <ul><li>輸入： **必填** 您要尋找的第一個元素的陣列。</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 最近 | 擷取指定陣列的最後一個元素。 | <ul><li>輸入： **必填** 您要尋找的最後一個元素的陣列。</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 將元素新增至陣列結尾。 | <ul><li>陣列： **必填** 要新增元素的陣列。</li><li>值：要附加到陣列的元素。</li></ul> | add_to_array(&#x200B;ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | 將陣列彼此結合。 | <ul><li>陣列： **必填** 要新增元素的陣列。</li><li>值：要附加到父陣列的陣列。</li></ul> | join_arrays(&#x200B;陣列，值) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | 取用輸入清單並將其轉換為陣列。 | <ul><li>INCLUDE_NULLS: **必填** 指示是否在響應陣列中包括空值的布爾值。</li><li>值： **必填** 要轉換為陣列的元素。</li></ul> | to_array(&#x200B;INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | 傳回輸入的大小。 | <ul><li>輸入： **必填** 您要尋找大小的物件。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函式用於將整個輸入陣列中的所有元素附加到配置檔案中陣列的末尾。 此函式為 **僅限** 適用。 如果用於插入的上下文，則此函式將按原樣返回輸入。 | <ul><li>陣列： **必填** 要在配置檔案中附加陣列的陣列。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | 此函式可用來取代陣列中的元素。 此函式為 **僅限** 適用。 如果用於插入的上下文，則此函式將按原樣返回輸入。 | <ul><li>陣列： **必填** 要替換配置檔案中陣列的陣列。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |

{style="table-layout:auto"}

### 邏輯運算子 {#logical-operators}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 解碼 | 在提供以陣列扁平化的索引鍵和索引鍵值配對清單的情況下，如果找到索引鍵，函式會傳回值，如果陣列中存在預設值，則會傳回預設值。 | <ul><li>索引鍵： **必填** 要匹配的密鑰。</li><li>OPTIONS: **必填** 平面化的索引鍵/值組陣列。 （可選）可將預設值放在結尾。</li></ul> | decode(KEY,OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 如果提供的stateCode是「ca」、「California」。<br>如果給定的stateCode是&quot;pa&quot;，則為&quot;Pennsylvania&quot;。<br>如果stateCode不符合下列項目，則為「N/A」。 |
| ii | 計算給定的布爾表達式，並根據結果返回指定值。 | <ul><li>運算式： **必填** 要評估的布林表達式。</li><li>TRUE_VALUE: **必填** 如果運算式評估為true，則會傳回的值。</li><li>FALSE_VALUE: **必填** 如果運算式評估為false，則傳回的值。</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### 彙總 {#aggregation}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 返回給定參數的最小值。 使用自然排序。 | <ul><li>OPTIONS: **必填** 可相互比較的一個或多個對象。</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 傳回指定引數的最大值。 使用自然排序。 | <ul><li>OPTIONS: **必填** 可相互比較的一個或多個對象。</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### 類型轉換 {#type-conversions}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 將字串轉換為BigInteger。 | <ul><li>字串： **必填** 要轉換為BigInteger的字串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 將字串轉換為Double。 | <ul><li>字串： **必填** 要轉換為Double的字串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 將字串轉換為浮點數。 | <ul><li>字串： **必填** 要轉換為Float的字串。</li></ul> | to_float(STRING) | to_float(「12.3456」) | 12.34566 |
| to_integer | 將字串轉換為整數。 | <ul><li>字串： **必填** 要轉換為整數的字串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON函式 {#json}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 從指定字串反序列化JSON內容。 | <ul><li>字串： **必填** 要反序列化的JSON字串。</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;:&quot;Doe&quot;}) | 代表JSON的物件。 |

{style="table-layout:auto"}

### 特別行動 {#special-operations}

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 產生偽隨機ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style="table-layout:auto"}

### 用戶代理函式 {#user-agent}

下表中包含的任何使用者代理函式都可傳回下列任一值：

* 手機 — 螢幕較小的行動裝置（通常&lt; 7英吋）
* 行動 — 尚未識別的行動裝置。 此行動裝置可以是電子閱讀器、平板電腦、手機、手錶等。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 從用戶代理字串中提取作業系統名稱。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | iOS |
| ua_os_version_major | 從使用者代理字串中擷取作業系統的主要版本。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B;s(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | iOS 5 |
| ua_os_version | 從使用者代理字串中擷取作業系統的版本。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | 5.1.1 |
| ua_os_name_version | 從用戶代理字串中提取作業系統的名稱和版本。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | iOS 5.1.1 |
| ua_agent_version | 從用戶代理字串中提取代理版本。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | 5.1 |
| ua_agent_version_major | 從用戶代理字串中提取代理名稱和主版本。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | Safari 5 |
| ua_agent_name | 從用戶代理字串中提取代理名。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | Safari |
| ua_device_class | 從用戶代理字串中提取設備類。 | <ul><li>USER_AGENT: **必填** 使用者代理字串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(如Mac OS X)AppleWebKit/534.46（KHTML如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3」) | 電話 |

{style="table-layout:auto"}

### 對象副本 {#object-copy}

>[!TIP]
>
>當來源中的物件對應至XDM中的物件時，會自動套用物件複製功能。 使用者無需執行其他動作。

您可以使用對象複製功能自動複製對象的屬性，而不對映射進行更改。 例如，如果源資料的結構為：

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

以及以下項目的XDM結構：

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

然後對應變成：

```json
address -> addr
address.line1 -> addr.addrLine1
```

在上例中， `city` 和 `state` 屬性也會在執行階段自動擷取，因為 `address` 物件已對應至 `addr`. 如果您要建立 `line2` 屬性，而您的輸入資料也包含 `line2` 在 `address` 物件，則也會自動擷取物件，而無需手動變更對應。

為確保自動對應正常運作，必須符合下列必要條件：

* 應映射父級對象；
* 必須在XDM架構中建立新屬性；
* 新屬性在來源架構和XDM架構中應具有相符的名稱。

如果未滿足任何先決條件，則必須使用資料準備手動將來源架構對應至XDM架構。

## 附錄

以下提供有關使用資料準備映射函式的其他資訊

### 特殊字元 {#special-characters}

下表概述保留字元及其對應的編碼字元清單。

| 保留字元 | 編碼字元 |
| --- | --- |
| 空間 | %20 |
| ! | %21 |
| 」 | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| ： | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}