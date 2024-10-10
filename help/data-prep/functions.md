---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm；ui指南；對應程式；對應；對應欄位；對應函式；
solution: Experience Platform
title: 資料準備對應函式
description: 本檔案將介紹與「資料準備」搭配使用的對應函式。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 830aa01828785a9ae4dea71078ee418fc510253c
workflow-type: tm+mt
source-wordcount: '6028'
ht-degree: 2%

---

# 資料準備對應函式

「資料準備」函式可用於根據來源欄位中輸入的內容計算值。

## 欄位

欄位名稱可以是任何合法的識別碼 — 以字母、美元符號(`$`)或底線字元(`_`)開頭的無限制長度的Unicode字母和數字序列。 變數名稱也區分大小寫。

如果欄位名稱不遵循此慣例，欄位名稱必須以`${}`包住。 因此，舉例來說，如果欄位名稱為「First Name」或「First.Name」，則名稱必須分別包裝為`${First Name}`或`${First\.Name}`。

>[!TIP]
>
>與階層互動時，如果子屬性有句點(`.`)，您必須使用反斜線(`\`)來逸出特殊字元。 如需詳細資訊，請閱讀[逸出特殊字元](home.md#escape-special-characters)的指南。

如果欄位名稱是下列保留關鍵字中的&#x200B;**any**，則必須以`${}{}`括住：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

此外，保留關鍵字也包含此頁面上列出的任何對應函式。

可以使用點標籤法存取子欄位中的資料。 例如，如果有`name`物件，若要存取`firstName`欄位，請使用`name.firstName`。

## 函式清單

下表列出所有支援的對映函式，包括範例運算式及其產生的輸出。

### 字串函式 {#string}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 串連指定的字串。 | <ul><li>STRING：要串連的字串。</li></ul> | concat(STRING_1， STRING_2) | concat(&quot;Hi， &quot;， &quot;there&quot;， &quot;！&quot;) | `"Hi, there!"` |
| 爆炸 | 根據規則運算式分割字串並傳回部分陣列。 可選擇加入規則運算式以分割字串。 依預設，分割會解析為「，」。 下列分隔符號&#x200B;**需要**&#x200B;以`\`逸出： `+, ?, ^, \|, ., [, (, {, ), *, $, \`如果您包含多個字元作為分隔符號，則會將分隔符號視為多字元分隔符號。 | <ul><li>字串： **必要**&#x200B;需要分割的字串。</li><li>REGEX： *Optional*&#x200B;可用來分割字串的規則運算式。</li></ul> | explode(STRING， REGEX) | explode(&quot;Hi， there！&quot;， &quot;) | `["Hi,", "there"]` |
| instr | 傳回子字串的位置/索引。 | <ul><li>輸入： **必要**&#x200B;正在搜尋的字串。</li><li>SUBSTRING： **必要**&#x200B;正在字串中搜尋的子字串。</li><li>START_POSITION： *Optional*&#x200B;開始檢視字串的位置。</li><li>發生次數： *選擇性*&#x200B;從開始位置尋找的第n個發生次數。 預設為1。 </li></ul> | instr(INPUT， SUBSTRING， START_POSITION， OCCURRENCE) | instr(「adobe.com」， 「com」) | 6 |
| 取代者 | 取代搜尋字串（如果存在於原始字串中）。 | <ul><li>輸入： **必要**&#x200B;輸入字串。</li><li>TO_FIND： **必要**&#x200B;要在輸入中查詢的字串。</li><li>TO_REPLACE： **必要**&#x200B;將取代&quot;TO_FIND&quot;中值的字串。</li></ul> | 取代器(INPUT， TO_FIND， TO_REPLACE) | replacestr(&quot;this is a string re test&quot;， &quot;re&quot;， &quot;replace&quot;) | 「這是字串取代測試」 |
| substr | 傳回指定長度的子字串。 | <ul><li>輸入： **必要**&#x200B;輸入字串。</li><li>START_INDEX： **必要**&#x200B;子字串開始的輸入字串索引。</li><li>長度： **必要**&#x200B;子字串的長度。</li></ul> | substr(INPUT， START_INDEX， LENGTH) | substr（「這是子字串測試」，7、8） | 「一個子集」 |
| 小寫/<br>lcase | 將字串轉換為小寫。 | <ul><li>INPUT： **必要**&#x200B;將轉換為小寫的字串。</li></ul> | lower(INPUT) | lower(&quot;HeLlO&quot;)<br>lcase(&quot;HeLlO&quot;) | &quot;hello&quot; |
| upper /<br>ucase | 將字串轉換為大寫。 | <ul><li>INPUT： **必要**&#x200B;將轉換為大寫的字串。</li></ul> | upper(INPUT) | upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLo&quot;) | &quot;HELLO&quot; |
| split | 在分隔符號上分割輸入字串。 下列分隔符號&#x200B;**需要**&#x200B;以`\`逸出： `\`。 如果您包含多個分隔符號，字串將會分割到字串中存在的&#x200B;**any**&#x200B;個分隔符號上。 **注意：**&#x200B;此函式只會從字串傳回非Null索引，無論是否有分隔符號。 如果產生的陣列中需要所有索引（包括null），請改用「爆炸」函式。 | <ul><li>INPUT： **必要**&#x200B;要分割的輸入字串。</li><li>SEPARATOR： **必要**&#x200B;用來分割輸入的字串。</li></ul> | split(INPUT， SEPARATOR) | split(「Hello world」，「 」) | `["Hello", "world"]` |
| 加入 | 使用分隔符號聯結物件清單。 | <ul><li>分隔符號： **必要**&#x200B;用來加入物件的字串。</li><li>物件： **必要**&#x200B;將聯結的字串陣列。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | 「Hello world」 |
| lpad | 將字串的左側與其他指定字串貼齊。 | <ul><li>INPUT： **必要**&#x200B;要填補的字串。 此字串可以是Null。</li><li>計數： **必要**&#x200B;要填補的字串大小。</li><li>PADDING： **必要**&#x200B;用來填補輸入的字串。 如果為Null或空白，則會視為單一空格。</li></ul> | lpad(INPUT， COUNT， PADDING) | lpad(&quot;bat&quot;， 8， &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | 將字串的右側與其他指定字串貼齊。 | <ul><li>INPUT： **必要**&#x200B;要填補的字串。 此字串可以是Null。</li><li>計數： **必要**&#x200B;要填補的字串大小。</li><li>PADDING： **必要**&#x200B;用來填補輸入的字串。 如果為Null或空白，則會視為單一空格。</li></ul> | rpad（輸入、計數、內距） | rpad(&quot;bat&quot;， 8， &quot;yz&quot;) | &quot;batyzyzy&quot; |
| 左側 | 取得指定字串的前「n」個字元。 | <ul><li>字串： **必要**&#x200B;您要取得前「n」個字元的字串。</li><li>計數： **必要**&#x200B;您要從字串取得的「n」個字元。</li></ul> | left(STRING， COUNT) | left(&quot;abcde&quot;， 2) | &quot;ab&quot; |
| 右 | 取得指定字串的最後「n」個字元。 | <ul><li>字串： **必要**&#x200B;您要取得最後「n」個字元的字串。</li><li>計數： **必要**&#x200B;您要從字串取得的「n」個字元。</li></ul> | right(STRING， COUNT) | right(&quot;abcde&quot;， 2) | &quot;de&quot; |
| ltrim | 移除字串開頭的空格。 | <ul><li>字串： **必要**&#x200B;您要移除空白字元的字串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 移除字串結尾的空格。 | <ul><li>字串： **必要**&#x200B;您要移除空白字元的字串。</li></ul> | rtrim(STRING) | rtrim(「hello 」) | &quot;hello&quot; |
| trim | 移除字串開頭和結尾的空格。 | <ul><li>字串： **必要**&#x200B;您要移除空白字元的字串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 等於 | 比較兩個字串以確認是否相等。 此函式區分大小寫。 | <ul><li>STRING1： **必要**&#x200B;您要比較的第一個字串。</li><li>STRING2： **必要**&#x200B;您要比較的第二個字串。</li></ul> | STRING1&#x200B;。equals(&#x200B;STRING2) | &quot;string1&quot;。 &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比較兩個字串以確認是否相等。 此函式&#x200B;**不區分**&#x200B;大小寫。 | <ul><li>STRING1： **必要**&#x200B;您要比較的第一個字串。</li><li>STRING2： **必要**&#x200B;您要比較的第二個字串。</li></ul> | STRING1&#x200B;。equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;。 &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### 規則運算式函式

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根據規則運算式，從輸入字串中擷取群組。 | <ul><li>字串： **必要**&#x200B;您正在擷取群組的字串。</li><li>REGEX： **必要**&#x200B;您希望群組比對的規則運算式。</li></ul> | extract_regex(STRING， REGEX) | extract_regex&#x200B;(&quot;E259，E259B_009,1_1&quot;&#x200B;， &quot;([^，]+)，[^，]*，([^，]+)&quot;) | [「E259，E259B_009,1_1」、「E259」、「1_1」] |
| matches_regex | 檢查字串是否符合輸入的規則運算式。 | <ul><li>字串： **必要**&#x200B;您正在檢查的字串符合規則運算式。</li><li>REGEX： **必要**&#x200B;您要比較的規則運算式。</li></ul> | matches_regex(STRING， REGEX) | matches_regex(&quot;E259，E259B_009,1_1&quot;， &quot;([^，]+)，[^，]*，([^，]+)&quot;) | true |

{style="table-layout:auto"}

### 雜湊函式 {#hashing}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 接受輸入並使用安全雜湊演演算法1 (SHA-1)產生雜湊值。 | <ul><li>輸入： **必要**&#x200B;要雜湊的純文字。</li><li>CHARSET： *選擇性*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT， CHARSET) | sha1（「我的文字」、「UTF-8」） | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | 接受輸入並使用安全雜湊演演算法256 (SHA-256)產生雜湊值。 | <ul><li>輸入： **必要**&#x200B;要雜湊的純文字。</li><li>CHARSET： *選擇性*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256（輸入，字元集） | sha256（「我的文字」、「UTF-8」） | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 接受輸入並使用安全雜湊演演算法512 (SHA-512)產生雜湊值。 | <ul><li>輸入： **必要**&#x200B;要雜湊的純文字。</li><li>CHARSET： *選擇性*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512（輸入，字元集） | sha512（「我的文字」、「UTF-8」） | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b386d4fd2ff68a fd24d16 |
| md5 | 接受輸入並使用MD5產生雜湊值。 | <ul><li>輸入： **必要**&#x200B;要雜湊的純文字。</li><li>CHARSET： *選擇性*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5（輸入，字元集） | md5（「我的文字」、「UTF-8」） | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 取得輸入使用循環冗餘檢查(CRC)演演算法來產生32位元循環代碼。 | <ul><li>輸入： **必要**&#x200B;要雜湊的純文字。</li><li>CHARSET： *選擇性*&#x200B;字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT， CHARSET) | crc32（「我的文字」，「UTF-8」） | 8df92e80 |

{style="table-layout:auto"}

### URL函式 {#url}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 從指定的URL傳回通訊協定。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必要**&#x200B;需要擷取通訊協定的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | 傳回指定URL的主機。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必要**&#x200B;需要擷取主機的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 傳回指定URL的連線埠。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必要**&#x200B;需要擷取連線埠的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | 傳回指定URL的路徑。 依預設，會傳回完整路徑。 | <ul><li>URL： **必要**&#x200B;需要從中擷取路徑的URL。</li><li>FULL_PATH： *Optional*&#x200B;判斷是否傳回完整路徑的布林值。 若設為false，則僅傳迴路徑的結尾。</li></ul> | get_url_path&#x200B;(URL， FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B;employee.csv&quot; |
| get_url_query_str | 傳回指定URL的查詢字串，作為查詢字串名稱和查詢字串值的對應。 | <ul><li>URL： **必要**&#x200B;您嘗試從中取得查詢字串的URL。</li><li>錨點： **必要**&#x200B;決定要如何處理查詢字串中的錨點。 可以是下列三個值之一：「保留」、「移除」或「附加」。<br><br>如果值為「保留」，則錨點會附加至傳回的值。<br>如果值為「remove」，則會從傳回的值中移除錨點。<br>如果值為「附加」，則錨點會以個別值的形式傳回。</li></ul> | get_url_query_str&#x200B;(URL， ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there？name=&#x200B;ferret#nose&quot;， &quot;retain&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B; &#x200B; &#x200B; &#x200B; &#x200B;/over/there？name=ferret#nose&quot;， &quot;remove&quot;)<br>get_url_query_str(&quot;foo://example.com：8042/over/there？name=ferret#nose&quot;， &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | 此函式以URL作為輸入，並使用ASCII字元取代或編碼特殊字元。 如需特殊字元的詳細資訊，請參閱本檔案附錄中的[特殊字元清單](#special-characters)。 | <ul><li>URL： **必要**&#x200B;您要取代或編碼為ASCII字元的輸入URL （含特殊字元）。</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>：//example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | 此函式以URL作為輸入，並將ASCII字元解碼為特殊字元。  如需特殊字元的詳細資訊，請參閱本檔案附錄中的[特殊字元清單](#special-characters)。 | <ul><li>URL： **必要**&#x200B;您要解碼成特殊字元的輸入URL （含ASCII字元）。</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>：//example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### 日期和時間函式 {#date-and-time}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。 在[資料格式處理指南](./data-handling.md#dates)的日期區段中，可以找到有關`date`函式的詳細資訊。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 擷取目前時間。 | | now() | now() | `2021-10-26T10:10:24Z` |
| 時間戳記 | 擷取目前的Unix時間。 | | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式設定輸入日期的格式。 | <ul><li>日期： **必要**&#x200B;您要格式化的輸入日期（ZonedDateTime物件）。</li><li>格式： **必要**&#x200B;您想要將日期變更為的格式。</li></ul> | format（日期，格式） | 格式(2019-10-23T11:24:00+00:00， &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | 根據指定格式將時間戳記轉換為日期字串。 | <ul><li>時間戳記： **必要**&#x200B;您要格式化的時間戳記。 這是以毫秒為單位寫入。</li><li>格式： **必要**&#x200B;您要時間戳記變成的格式。</li></ul> | dformat(TIMESTAMP， FORMAT) | dformat(1571829875000， &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必要**&#x200B;代表日期的字串。</li><li>格式： **必要**&#x200B;代表來源日期格式的字串。**注意：**&#x200B;這並&#x200B;**不**&#x200B;代表您要將日期字串轉換成的格式。 </li><li>DEFAULT_DATE： **必要**&#x200B;如果提供的日期為Null，則傳回預設日期。</li></ul> | date(DATE， FORMAT， DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;， now()) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必要**&#x200B;代表日期的字串。</li><li>格式： **必要**&#x200B;代表來源日期格式的字串。**注意：**&#x200B;這並&#x200B;**不**&#x200B;代表您要將日期字串轉換成的格式。 </li></ul> | 日期（日期，格式） | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必要**&#x200B;代表日期的字串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | 「2019-10-23T11:24:00Z」 |
| date_part | 擷取日期部分。 支援下列元件值： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;SSS&quot;<br> | <ul><li>元件： **必要**&#x200B;代表日期一部分的字串。 </li><li>日期： **必要**&#x200B;日期（標準格式）。</li></ul> | date_part&#x200B;(COMPONENT， DATE) | date_part(&quot;MM&quot;， date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 取代指定日期中的元件。 接受下列元件： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>元件： **必要**&#x200B;代表日期一部分的字串。 </li><li>值： **必要**&#x200B;為指定日期的元件設定的值。</li><li>日期： **必要**&#x200B;日期（標準格式）。</li></ul> | set_date_part&#x200B;(COMPONENT， VALUE， DATE) | set_date_part(&quot;m&quot;， 4， date(&quot;2016-11-09T11:44:44.797&quot;) | 「2016-04-09T11:44:44Z」 |
| make_date_time | 從零件建立日期。 此函式也可以使用make_timestamp感生。 | <ul><li>YEAR： **必填**&#x200B;以四位數寫入的年份。</li><li>月份： **必要**&#x200B;月份。 允許的值為1到12。</li><li>日： **必要**&#x200B;日。 允許的值為1到31。</li><li>小時： **必要**&#x200B;小時。 允許的值為0到23。</li><li>MINUTE： **必要**&#x200B;分鐘。 允許值為0到59。</li><li>NANOSECOND： **必要**&#x200B;納秒的值。 允許的值為0到999999999。</li><li>時區： **必要**&#x200B;日期時間的時區。</li></ul> | make_date_time&#x200B;（年、月、日、小時、分鐘、秒、納秒、時區） | make_date_time&#x200B;（2019， 10， 17， 11， 55， 12， 999， &quot;美洲/洛杉磯&quot;） | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 將任何時區的日期轉換為UTC格式的日期。 | <ul><li>日期： **必要**&#x200B;您嘗試轉換的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 將日期從一個時區轉換為另一個時區。 | <ul><li>日期： **必要**&#x200B;您嘗試轉換的日期。</li><li>ZONE： **必要**&#x200B;您嘗試將日期轉換為的時區。</li></ul> | zone_date_to_zone&#x200B;(DATE， ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### 階層 — 物件 {#objects}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 檢查物件是否為空白。 | <ul><li>輸入： **必要**&#x200B;您嘗試檢查的物件是空的。</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 建立物件清單。 | <ul><li>INPUT： **必要**&#x200B;索引鍵和陣列配對的群組。</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 根據指定的平面索引鍵/值配對建立物件。 | <ul><li>INPUT： **必要**&#x200B;索引鍵/值配對的平面清單。</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;， &quot;John&quot;， &quot;lastName&quot;， &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 從輸入字串建立物件。 | <ul><li>字串： **必要**&#x200B;正在剖析以建立物件的字串。</li><li>VALUE_DELIMITER： *Optional*&#x200B;將欄位與值分開的分隔符號。 預設分隔字元為`:`。</li><li>FIELD_DELIMITER： *Optional*&#x200B;分隔欄位值配對的分隔符號。 預設分隔字元為`,`。</li></ul> | str_to_object&#x200B;(STRING， VALUE_DELIMITER， FIELD_DELIMITER) **注意**：您可以使用`get()`函式搭配`str_to_object()`來擷取字串中索引鍵的值。 | <ul><li>範例#1： str_to_object(&quot;firstName - John ； lastName - ； - 123 345 7890&quot;， &quot;-&quot;， &quot;；&quot;)</li><li>範例#2： str_to_object(&quot;firstName - John ； lastName - ； phone - 123 456 7890&quot;， &quot;-&quot;， &quot;；&quot;)。get(&quot;firstName&quot;)</li></ul> | <ul><li>範例#1：`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>範例#2： &quot;John&quot;</li></ul> |
| contains_key | 檢查物件是否存在於來源資料中。 **注意：**&#x200B;此函式會取代已棄用的`is_set()`函式。 | <ul><li>INPUT： **必要**&#x200B;要檢查的路徑是否存在於來源資料中。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 無效 | 將屬性的值設定為`null`。 當您不想將欄位複製到目標結構描述時，就應該使用此專案。 | | nullify() | nullify() | `null` |
| get_keys | 剖析索引鍵/值配對並傳回所有索引鍵。 | <ul><li>物件： **必要**&#x200B;將從中擷取金鑰的物件。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;： &quot;Pride and Impance&quot;， &quot;book2&quot;： &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 根據指定的索引鍵，剖析索引鍵/值配對並傳回字串的值。 | <ul><li>字串： **必要**&#x200B;您要剖析的字串。</li><li>索引鍵： **必要**&#x200B;必須擷取值的索引鍵。</li><li>VALUE_DELIMITER： **必要**&#x200B;分隔欄位與值的分隔符號。 若提供`null`或空字串，則此值為`:`。</li><li>FIELD_DELIMITER： *Optional*&#x200B;分隔欄位和值配對的分隔符號。 若提供`null`或空字串，則此值為`,`。</li></ul> | get_values(STRING， KEY， VALUE_DELIMITER， FIELD_DELIMITER) | get_values(\&quot;firstName - John ， lastName - Cena ， phone - 555 420 8692\&quot;， \&quot;firstName\&quot;， \&quot;-\&quot;， \&quot;，\&quot;) | John |
| map_get_values | 接受地圖和按鍵輸入。 如果輸入是單一索引鍵，則函式會傳回與該索引鍵相關聯的值。 如果輸入為字串陣列，則函式會傳回與所提供索引鍵對應的所有值。 如果傳入的對應有重複的索引鍵，則傳回值必須刪除重複的索引鍵並傳回唯一值。 | <ul><li>對應： **必要**&#x200B;輸入對應資料。</li><li>索引鍵： **必要**&#x200B;索引鍵可以是單一字串或字串陣列。 如果提供任何其他基本型別（資料/數字），則會將其視為字串。</li></ul> | get_values(MAP， KEY) | 如需程式碼範例，請參閱[附錄](#map_get_values)。 | |
| map_has_keys | 如果提供一個或多個輸入鍵，則函式傳回true。 如果提供字串陣列作為輸入，則函式在找到的第一個鍵上傳回true。 | <ul><li>對應： **必要**&#x200B;輸入對應資料</li><li>索引鍵： **必要**&#x200B;索引鍵可以是單一字串或字串陣列。 如果提供任何其他基本型別（資料/數字），則會將其視為字串。</li></ul> | map_has_keys(MAP， KEY) | 如需程式碼範例，請參閱[附錄](#map_has_keys)。 | |
| add_to_map | 接受至少兩個輸入。 可提供任意數量的地圖作為輸入。 「資料準備」會傳回單一對應，其中包含來自所有輸入的所有索引鍵/值組。 如果一個或多個索引鍵重複（在相同對應中或跨對應），資料準備會去除重複的索引鍵，因此第一個索引鍵/值組會按照它們在輸入中傳遞的順序持續存在。 | 對應： **必要**&#x200B;輸入對應資料。 | add_to_map(MAP 1， MAP 2， MAP 3， ...) | 如需程式碼範例，請參閱[附錄](#add_to_map)。 | |
| object_to_map （語法1） | 使用此函式來建立對應資料型別。 | <ul><li>索引鍵： **必要**&#x200B;索引鍵必須是字串。 如果提供其他任何基本值（例如整數或日期），則會自動轉換為字串並視為字串。</li><li>ANY_TYPE： **必要**&#x200B;參考任何支援的XDM資料型別，但Map除外。</li></ul> | object_to_map(KEY， ANY_TYPE， KEY， ANY_TYPE， ... ) | 如需程式碼範例，請參閱[附錄](#object_to_map)。 | |
| object_to_map （語法2） | 使用此函式來建立對應資料型別。 | <ul><li>物件： **必要**&#x200B;您可以提供內送物件或物件陣列，並以索引鍵指向物件內的屬性。</li></ul> | object_to_map(OBJECT) | 如需程式碼範例，請參閱[附錄](#object_to_map)。 |
| object_to_map （語法3） | 使用此函式來建立對應資料型別。 | <ul><li>物件： **必要**&#x200B;您可以提供內送物件或物件陣列，並以索引鍵指向物件內的屬性。</li></ul> | object_to_map(OBJECT_ARRAY， ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | 如需程式碼範例，請參閱[附錄](#object_to_map)。 |

{style="table-layout:auto"}

如需物件複製功能的詳細資訊，請參閱下方[小節](#object-copy)。

### 階層 — 陣列 {#arrays}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 合併 | 傳回給定陣列中的第一個非null物件。 | <ul><li>INPUT： **必要**&#x200B;您要尋找的第一個非null物件的陣列。</li></ul> | coalesce(INPUT) | coalesce(null， null， null， first， null， second) | &quot;first&quot; |
| 第一 | 擷取給定陣列的第一個元素。 | <ul><li>INPUT： **必要**&#x200B;您要尋找第一個元素的陣列。</li></ul> | first(INPUT) | first(&quot;1&quot;， &quot;2&quot;， &quot;3&quot;) | &quot;1&quot; |
| 最後 | 擷取給定陣列的最後一個元素。 | <ul><li>INPUT： **必要**&#x200B;您要尋找最後一個元素的陣列。</li></ul> | last(INPUT) | last(&quot;1&quot;， &quot;2&quot;， &quot;3&quot;) | 「3」 |
| add_to_array | 將元素新增至陣列結尾。 | <ul><li>ARRAY： **必要**&#x200B;您要新增元素的陣列。</li><li>VALUES：您要附加至陣列的元素。</li></ul> | add_to_array&#x200B;(ARRAY， VALUES) | add_to_array&#x200B;([&#39;a&#39;， &#39;b&#39;]， &#39;c&#39;， &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| join_array | 將陣列彼此結合。 | <ul><li>ARRAY： **必要**&#x200B;您要新增元素的陣列。</li><li>VALUES：您要附加至父陣列的陣列。</li></ul> | join_arrays&#x200B;(ARRAY， VALUES) | join_arrays&#x200B;([&#39;a&#39;， &#39;b&#39;]， [&#39;c&#39;]， [&#39;d&#39;， &#39;e&#39;]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;] |
| to_array | 採用輸入清單並將其轉換為陣列。 | <ul><li>INCLUDE_NULLS： **必要**&#x200B;布林值，表示是否要在回應陣列中包含null。</li><li>值： **必要**&#x200B;要轉換成陣列的元素。</li></ul> | to_array&#x200B;(INCLUDE_NULLS， VALUES) | to_array(false， 1， null， 2， 3) | `[1, 2, 3]` |
| 大小_of | 傳回輸入的大小。 | <ul><li>輸入： **必要**&#x200B;您嘗試尋找大小的物件。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函式用於將整個輸入陣列中的所有元素附加到Profile中陣列的結尾。 此函式僅&#x200B;**適用於更新期間**。 如果在插入內容中使用，此函式會依原樣傳回輸入。 | <ul><li>陣列： **必要**&#x200B;要在設定檔中附加陣列的陣列。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123， 456] |
| upsert_array_replace | 此函式用於取代陣列中的元素。 此函式僅&#x200B;**適用於更新期間**。 如果在插入內容中使用，此函式會依原樣傳回輸入。 | <ul><li>陣列： **必要**&#x200B;要取代設定檔中陣列的陣列。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123， 456] |
| [!BADGE 僅目的地]{type=Informative} array_to_string | 使用指定的分隔符號聯結陣列中元素的字串表示法。 如果陣列是多維度的，則會在聯結前將其平面化。 **注意**：此函式用於目的地。 如需詳細資訊，請參閱[檔案](../destinations/ui/export-arrays-calculated-fields.md)。 | <ul><li>SEPARATOR： **必要**&#x200B;用來聯結陣列中元素的分隔符號。</li><li>ARRAY： **必要**&#x200B;要聯結的陣列（平面化之後）。</li></ul> | array_to_string(SEPARATOR， ARRAY) | `array_to_string(";", ["Hello", "world"])` | 「Hello；world」 |
| [!BADGE 僅目的地]{type=Informative} filterArray* | 根據述詞篩選指定的陣列。 **注意**：此函式用於目的地。 如需詳細資訊，請參閱[檔案](../destinations/ui/export-arrays-calculated-fields.md)。 | <ul><li>陣列： **必要**&#x200B;要篩選的陣列</li><li>述詞： **必要**&#x200B;要套用至指定陣列之每個專案的述詞。 | filterArray(ARRAY， PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5， 7] |
| [!BADGE 僅目的地]{type=Informative} transformArray* | 根據述詞轉換指定的陣列。 **注意**：此函式用於目的地。 如需詳細資訊，請參閱[檔案](../destinations/ui/export-arrays-calculated-fields.md)。 | <ul><li>陣列： **必要**&#x200B;要轉換的陣列。</li><li>述詞： **必要**&#x200B;要套用至指定陣列之每個專案的述詞。 | transformArray(ARRAY， PREDICATE) | ` transformArray([5, 6, 7], x -> x + 1)` | [6， 7， 8] |
| [!BADGE 只限目的地]{type=Informatic} flattenArray* | 將指定的（多維）陣列平面化為一維陣列。 **注意**：此函式用於目的地。 如需詳細資訊，請參閱[檔案](../destinations/ui/export-arrays-calculated-fields.md)。 | <ul><li>陣列： **必要**&#x200B;要平面化的陣列。</li></ul> | flattenArray(ARRAY) | flattenArray([[[&#39;a&#39;， &#39;b&#39;]， [&#39;c&#39;， &#39;d&#39;]]， [[&#39;e&#39;]， [&#39;f&#39;]]]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;、&#39;f&#39;] |

{style="table-layout:auto"}

### 階層 — 對應 {#map}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | 此函式以物件陣列和索引鍵作為輸入，並傳回索引鍵欄位的對應，其中值為索引鍵，而陣列元素為值。 | <ul><li>INPUT： **必要**&#x200B;您要尋找的第一個非null物件的物件陣列。</li><li>索引鍵： **必要**&#x200B;索引鍵必須是物件陣列中的欄位名稱，而且物件必須是值。</li></ul> | array_to_map（OBJECT[]輸入，索引鍵） | 如需程式碼範例，請閱讀[附錄](#object_to_map)。 |
| object_to_map | 此函式將物件當作引數，並傳回機碼值組的對應。 | <ul><li>INPUT： **必要**&#x200B;您要尋找的第一個非null物件的物件陣列。</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address)，其中輸入為&quot; + &quot;address： {line1 ： \&quot;345 park ave\&quot;，line2： \&quot;bldg 2\&quot;，City ： \&quot;san jose\&quot;，State ： \&quot;CA\&quot;，type： \&quot;office\&quot;}&quot; | 傳回具有給定欄位名稱和值配對的對應，如果輸入為null，則傳回null。 例如︰`"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | 此函式接受索引鍵值配對清單並傳回索引鍵值配對的對應。 | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;， \&quot;John\&quot;， \&quot;lastName\&quot;， \&quot;Doe\&quot;)&quot; | 傳回具有給定欄位名稱和值配對的對應，如果輸入為null，則傳回null。 例如︰`"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### 邏輯運運算元 {#logical-operators}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 解碼 | 指定將索引鍵和索引鍵值配對清單平面化為陣列時，若找到索引鍵，此函式會傳回值，若陣列中存在索引鍵，則會傳回預設值。 | <ul><li>索引鍵： **必要**&#x200B;要比對的索引鍵。</li><li>OPTIONS： **必要**&#x200B;索引鍵/值配對的平面化陣列。 您可以選擇將預設值放在結尾。</li></ul> | decode(KEY， OPTIONS) | decode(stateCode， &quot;ca&quot;， &quot;California&quot;， &quot;pa&quot;， &quot;Pennsylvania&quot;， &quot;N/A&quot;) | 如果指定的stateCode為&quot;ca&quot;、&quot;California&quot;。<br>如果指定的stateCode為「pa」，「Pennsylvania」。<br>如果stateCode不符合下列專案：「不適用」。 |
| iif | 評估給定的布林運算式，並根據結果傳回指定的值。 | <ul><li>運算式： **必要**&#x200B;正在評估的布林運算式。</li><li>TRUE_VALUE： **必要**&#x200B;如果運算式評估為true，則傳回的值。</li><li>FALSE_VALUE： **必要**&#x200B;運算式評估為false時所傳回的值。</li></ul> | iif（運算式， TRUE_VALUE， FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### 彙總 {#aggregation}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 傳回給定引數的最小值。 使用自然排序。 | <ul><li>OPTIONS： **必要**&#x200B;可以相互比較的一或多個物件。</li></ul> | min(OPTIONS) | min(3， 1， 4) | 1 |
| max | 傳回給定引數的最大值。 使用自然排序。 | <ul><li>OPTIONS： **必要**&#x200B;可以相互比較的一或多個物件。</li></ul> | 最大(OPTIONS) | max(3， 1， 4) | 4 |

{style="table-layout:auto"}

### 型別轉換 {#type-conversions}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 將字串轉換為BigInteger。 | <ul><li>字串： **必要**&#x200B;要轉換為BigInteger的字串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 將字串轉換為雙精度浮點數。 | <ul><li>字串： **必要**&#x200B;要轉換為Double的字串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 將字串轉換為浮點數。 | <ul><li>字串： **必要**&#x200B;要轉換為浮點數的字串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 將字串轉換為整數。 | <ul><li>字串： **必要**&#x200B;要轉換為整數的字串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON函式 {#json}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 從給定的字串將JSON內容還原序列化。 | <ul><li>字串： **必要**&#x200B;要還原序列化的JSON字串。</li></ul> | json_to_object&#x200B;(STRING) | &#x200B; json_to_object({&quot;info&quot;：{&quot;firstName&quot;：&quot;John&quot;，&quot;lastName&quot;： &quot;Doe&quot;}}) | 代表JSON的物件。 |

{style="table-layout:auto"}

### 特殊操作 {#special-operations}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 產生偽隨機識別碼。 | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | 此函式接受FPID字串並將其轉換為ECID，以便用於Adobe Experience Platform和Adobe Experience Cloud應用程式。 | <ul><li>字串： **必要**&#x200B;要轉換為ECID的FPID字串。</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### 使用者代理程式功能 {#user-agent}

下表包含的任何使用者代理程式函式都可以傳回下列任一值：

* 電話 — 具有小熒幕（通常&lt; 7英吋）的行動裝置
* 行動 — 尚未識別的行動裝置。 此行動裝置可以是電子閱讀器、平板電腦、手機、手錶等。

如需裝置欄位值的詳細資訊，請閱讀本檔案附錄中的裝置欄位值[清單](#device-field-values)。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 從使用者代理字串中擷取作業系統名稱。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 從使用者代理程式字串中擷取作業系統的主要版本。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 從使用者代理程式字串中擷取作業系統的版本。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 從使用者代理字串中擷取作業系統的名稱和版本。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 從使用者代理字串中擷取代理程式版本。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 從使用者代理字串中擷取代理名稱和主要版本。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 從使用者代理字串中擷取代理名稱。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 從使用者代理程式字串中擷取裝置類別。 | <ul><li>USER_AGENT： **必要**&#x200B;使用者代理字串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 電話 |

{style="table-layout:auto"}

### Analytics函式 {#analytics}

>[!NOTE]
>
>您只能對WebSDK和Adobe Analytics流程使用下列分析函式。

| 函數 | 說明 | 參數 | 語法 | 運算式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | 從Analytics事件字串中擷取事件ID。 | <ul><li>EVENT_STRING： **必要**&#x200B;逗號分隔的Analytics事件字串。</li><li>EVENT_NAME： **必要**&#x200B;要擷取的事件名稱和ID。</li></ul> | aa_get_event_id(EVENT_STRING， EVENT_NAME) | aa_get_event_id(&quot;event101=5：123456，scOpen&quot;， &quot;event101&quot;) | 123456 |
| aa_get_event_value | 從Analytics事件字串中擷取事件值。 如果未指定事件值，則會傳回1。 | <ul><li>EVENT_STRING： **必要**&#x200B;逗號分隔的Analytics事件字串。</li><li>EVENT_NAME： **必要**&#x200B;要從中擷取值的事件名稱。</li></ul> | aa_get_event_value(EVENT_STRING， EVENT_NAME) | aa_get_event_value(&quot;event101=5：123456，scOpen&quot;， &quot;event101&quot;) | 5 |
| aa_get_product_categories | 從Analytics產品字串中擷取產品類別。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories（&quot;；範例產品1；1；3.50，範例類別2；範例產品2；1；5.99&quot;） | [null，&quot;Example category 2&quot;] |
| aa_get_product_names | 從Analytics產品字串中擷取產品名稱。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names（&quot;；範例產品1；1；3.50，範例類別2；範例產品2；1；5.99&quot;） | [&quot;Example product 1&quot;，&quot;Example product 2&quot;] |
| aa_get_product_quantities | 從Analytics產品字串中擷取數量。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li></ul> | aa_get_product_quantices(PRODUCTS_STRING) | aa_get_product_quantices（&quot;；範例產品1；1；3.50，範例類別2；範例產品2&quot;） | [&quot;1&quot;，空值] |
| aa_get_product_prices | 從Analytics產品字串中擷取價格。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li></ul> | aa_get_product_prices(PRODUCTS_STRING) | aa_get_product_prices（&quot;；範例產品1；1；3.50，範例類別2；範例產品2&quot;） | [&quot;3.50&quot;，空值] |
| aa_get_product_event_values | 從產品字串中擷取已命名事件的值，做為字串陣列。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li><li>EVENT_NAME： **必要**&#x200B;要從中擷取值的事件名稱。</li></ul> | aa_get_product_event_values(PRODUCTS_STRING， EVENT_NAME) | aa_get_product_event_values（&quot;；範例產品1；1；4.20；event1=2.3\|event2=5:1，；範例產品2；1；4.20；event1=3\|event2=2:2&quot;， &quot;event1&quot;） | [&quot;2.3&quot;，&quot;3&quot;] |
| aa_get_product_evars | 從產品字串中擷取已命名事件的evar值，做為字串陣列。 | <ul><li>PRODUCTS_STRING： **必要** Analytics產品字串。</li><li>eVar_名稱： **必要**&#x200B;要擷取的eVar名稱。</li></ul> | aa_get_product_evars(PRODUCTS_STRING， EVENT_NAME) | aa_get_product_evars(&quot;；範例產品；1；6.69；；eVar1=銷售值&quot;， &quot;eVar1&quot;) | [「銷售值」] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### 物件複製 {#object-copy}

>[!TIP]
>
>當來源中的物件對應至XDM中的物件時，會自動套用物件複製功能。 使用者無需執行其他動作。

您可以使用物件複製功能自動複製物件的屬性，而不需變更對映。 例如，如果來源資料的結構為：

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

和XDM結構：

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

然後，對應會變成：

```json
address -> addr
address.line1 -> addr.addrLine1
```

在上述範例中，`city`和`state`屬性也會在執行階段自動擷取，因為`address`物件已對應至`addr`。 如果您要在XDM結構中建立`line2`屬性，而您的輸入資料也在`address`物件中包含`line2`，則它也會自動內嵌，而無需手動變更對應。

若要確保自動對應能夠運作，必須符合下列先決條件：

* 父級物件應進行對應；
* 必須在XDM結構描述中建立新屬性；
* 新屬性在來源結構描述和XDM結構描述中應該有相符的名稱。

如果不滿足任何先決條件，則必須使用資料準備手動將來源結構描述對應到XDM結構描述。

## 附錄

以下提供使用「資料準備」對應函式的其他資訊

### 特殊字元 {#special-characters}

下表概述保留字元及其對應的編碼字元清單。

| 保留字元 | 編碼字元 |
| --- | --- |
| 空格 | %20 |
| ！ | %21 |
| 」 | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| 『 | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| ， | %2C |
| / | %2F |
| ： | %3A |
| ； | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| 『 | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### 裝置欄位值 {#device-field-values}

下表概述裝置欄位值清單及其對應說明。

| 裝置 | 說明 |
| --- | --- |
| 桌面 | 桌上型電腦或筆記型電腦型別的裝置。 |
| 匿名 | 匿名裝置。 在某些情況下，這些是匿名化軟體變更的`useragents`。 |
| 未知 | 未知的裝置。 這些通常是`useragents`，不包含裝置的相關資訊。 |
| 行動 | 尚未識別的行動裝置。 此行動裝置可以是電子閱讀器、平板電腦、手機、手錶等。 |
| 平板電腦 | 具備大熒幕（通常> 7英吋）的行動裝置。 |
| 電話 | 小熒幕（通常&lt; 7英吋）的行動裝置。 |
| 觀看 | 具有小熒幕（通常小於2英吋）的行動裝置。 這些裝置通常可作為手機/平板電腦型別裝置的額外畫面。 |
| 增強現實 | 具有AR功能的行動裝置。 |
| Virtual Reality | 具備VR功能的行動裝置。 |
| 電子閱讀器 | 類似平板電腦的裝置，但通常具有[!DNL eInk]熒幕。 |
| 機上盒 | 連線裝置，允許透過電視大小的熒幕進行互動。 |
| TV | 類似機頂盒的裝置，但內建於電視中。 |
| 家用電器 | （通常為大型）家用電器，例如冰箱。 |
| 遊戲主機 | 固定式遊戲系統，例如[!DNL Playstation]或[!DNL XBox]。 |
| 手持式遊戲機 | 行動遊戲系統，例如[!DNL Nintendo Switch]。 |
| 語音 | 語音導向裝置，例如[!DNL Amazon Alexa]或[!DNL Google Home]。 |
| 汽車 | 車輛瀏覽器。 |
| 自動機制 | 造訪網站的機器人。 |
| 機器人行動裝置 | 造訪網站但表示希望被視為行動訪客的機器人。 |
| 自動機制模擬器 | 造訪網站的機器人會裝扮成類似[!DNL Google]的機器人，但實際上並非如此。 **注意**：在大多數情況下，機器人模仿者確實是機器人。 |
| 雲端 | 雲端型應用程式。 這些不是機器人或駭客，而是需要連線的應用程式。 這包含[!DNL Mastodon]部伺服器。 |
| 駭客 | 在`useragent`字串中偵測到指令碼時，會使用此裝置值。 |

{style="table-layout:auto"}

### 程式碼範例 {#code-samples}

#### map_get_values {#map-get-values}

+++選取以檢視範例

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++選取以檢視範例

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++選取以檢視範例

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**語法1**

+++選取以檢視範例

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**語法2**

+++選取以檢視範例

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**語法3**

+++選取以檢視範例

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++選取以檢視範例

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

