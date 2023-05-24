---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應到xdm；將csv對應到xdm；ui指南；對應程式；對應；對應欄位；對應函式；
solution: Experience Platform
title: 資料準備對應函式
description: 本檔案將介紹「資料準備」使用的對應函式。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: a89faf5f1d1befdc057cd872fcd190703c620c2d
workflow-type: tm+mt
source-wordcount: '4916'
ht-degree: 3%

---

# 資料準備對應函式

「資料準備」函式可用於根據來源欄位中輸入的內容運算和計算值。

## 字段

欄位名稱可以是任何合法識別碼 — 由字母和美元符號(`$`)或底線字元(`_`)。 變數名稱也區分大小寫。

如果欄位名稱不遵循此慣例，則欄位名稱必須換行 `${}`. 因此，舉例來說，如果欄位名稱為「First Name」或「First.Name」，則名稱必須封裝為 `${First Name}` 或 `${First\.Name}` （分別）。

>[!TIP]
>
>與階層互動時，如果子屬性有句點(`.`)，則必須使用反斜線(`\`)以逸出特殊字元。 如需詳細資訊，請閱讀以下指南： [逸出特殊字元](home.md#escape-special-characters).

此外，如果欄位名稱為 **任何** 保留關鍵字中，必須以 `${}`：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

可以使用點標籤法存取子欄位內的資料。 例如，如果有 `name` 物件，以存取 `firstName` 欄位，使用 `name.firstName`.

## 函数列表

下表列出所有支援的對映函式，包括範例運算式及其產生的輸出。

### 字符串函数 {#string}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 串連指定的字串。 | <ul><li>STRING：要串連的字串。</li></ul> | concat(STRING_1， STRING_2) | concat(&quot;Hi， &quot;， &quot;there&quot;， &quot;！&quot;) | `"Hi, there!"` |
| 爆炸 | 根據regex分割字串並傳回部分陣列。 可選擇加入規則運算式以分割字串。 依預設，分割會解析為「，」。 下列分隔字元 **需要** 將逸出 `\`： `+, ?, ^, \|, ., [, (, {, ), *, $, \` 如果您包含多個字元做為分隔字元，則會將分隔字元視為多字元分隔字元。 | <ul><li>字串： **必填** 需要分割的字串。</li><li>規則運算式： *可選* 可用來分割字串的規則運算式。</li></ul> | explode(STRING， REGEX) | explode(&quot;Hi， there！&quot;， &quot;) | `["Hi,", "there"]` |
| 安裝 | 傳回子字串的位置/索引。 | <ul><li>輸入： **必填** 正在搜尋的字串。</li><li>子字串： **必填** 正在字串中搜尋的子字串。</li><li>START_POSITION： *可選* 在字串中開始檢視的位置。</li><li>發生次數： *可選* 從起始位置開始尋找的第n個事件。 預設為1。 </li></ul> | instr(INPUT， SUBSTRING， START_POSITION， OCCURRENCE) | instr(&quot;adobe.com&quot;， &quot;com&quot;) | 6 |
| 取代者 | 取代原始字串中存在的搜尋字串。 | <ul><li>輸入： **必填** 輸入字串。</li><li>TO_FIND： **必填** 要在輸入中查詢的字串。</li><li>TO_REPLACE： **必填** 取代&quot;TO_FIND&quot;中值的字串。</li></ul> | 取代器(INPUT， TO_FIND， TO_REPLACE) | replacestr(&quot;this is a string re test&quot;， &quot;re&quot;， &quot;replace&quot;) | 「這是字串取代測試」 |
| substr | 傳回指定長度的子字串。 | <ul><li>輸入： **必填** 輸入字串。</li><li>START_INDEX： **必填** 子字串開始的輸入字串索引。</li><li>長度： **必填** 子字串的長度。</li></ul> | substr(INPUT， START_INDEX， LENGTH) | substr(&quot;This is a substring test&quot;， 7， 8) | &quot;a subst&quot; |
| lower /<br>lcase | 將字串轉換為小寫。 | <ul><li>輸入： **必填** 將轉換為小寫的字串。</li></ul> | lower(INPUT) | lower(&quot;HeLo&quot;)<br>lcase(&quot;HeLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | 將字串轉換為大寫。 | <ul><li>輸入： **必填** 將轉換為大寫的字串。</li></ul> | upper(INPUT) | upper(&quot;HeLor&quot;)<br>Ucase(&quot;HeLo&quot;) | &quot;HELLO&quot; |
| split | 在分隔符號上分割輸入字串。 下列分隔符號 **需求** 將逸出 `\`： `\`. 如果您包含多個分隔字元，字串將會分割為 **任何** 字串中存在的分隔字元數目。 | <ul><li>輸入： **必填** 即將分割的輸入字串。</li><li>分隔符號： **必填** 用來分割輸入的字串。</li></ul> | split(INPUT， SEPARATOR) | split(&quot;Hello world&quot;， &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符號聯結物件清單。 | <ul><li>分隔符號： **必填** 用來聯結物件的字串。</li><li>物件： **必填** 要聯結的字串陣列。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | 「Hello world」 |
| lpad | 將字串的左側與其他指定字串貼齊。 | <ul><li>輸入： **必填** 即將填補的字串。 此字串可以是Null。</li><li>計數： **必填** 要填補的字串大小。</li><li>內距： **必填** 用來填補輸入的字串。 如果為Null或空白，則會視為單一空格。</li></ul> | lpad(INPUT， COUNT， PADDING) | lpad(&quot;bat&quot;， 8， &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | 將字串的右側與其他指定字串貼齊。 | <ul><li>輸入： **必填** 即將填補的字串。 此字串可以是Null。</li><li>計數： **必填** 要填補的字串大小。</li><li>內距： **必填** 用來填補輸入的字串。 如果為Null或空白，則會視為單一空格。</li></ul> | rpad(INPUT， COUNT， PADDING) | rpad(&quot;bat&quot;， 8， &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | 取得指定字串的前「n」個字元。 | <ul><li>字串： **必填** 您要取得前「n」個字元的字串。</li><li>計數： **必填**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | left(STRING， COUNT) | left(&quot;abcde&quot;， 2) | &quot;ab&quot; |
| 右側 | 取得指定字串的最後「n」個字元。 | <ul><li>字串： **必填** 您要取得最後「n」個字元的字串。</li><li>計數： **必填**&#x200B;您要從字串取得的&quot;n&quot;字元。</li></ul> | right(STRING， COUNT) | right(&quot;abcde&quot;， 2) | &quot;de&quot; |
| ltrim | 移除字串開頭的空格。 | <ul><li>字串： **必填** 您要移除空白字元的字串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 移除字串結尾的空格。 | <ul><li>字串： **必填** 您要移除空白字元的字串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | 移除字串開頭和結尾的空格。 | <ul><li>字串： **必填** 您要移除空白字元的字串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 等于 | 比較兩個字串以確認是否相等。 此函式區分大小寫。 | <ul><li>STRING1： **必填** 您要比較的第一個字串。</li><li>STRING2： **必填** 您要比較的第二個字串。</li></ul> | STRING1. &#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;。 &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比較兩個字串以確認是否相等。 此函式為 **not** 區分大小寫。 | <ul><li>STRING1： **必填** 您要比較的第一個字串。</li><li>STRING2： **必填** 您要比較的第二個字串。</li></ul> | STRING1. &#x200B;equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;。 &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### 規則運算式函式

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根據規則運算式，從輸入字串中擷取群組。 | <ul><li>字串： **必填** 您從中擷取群組的字串。</li><li>規則運算式： **必填** 您希望群組比對的規則運算式。</li></ul> | extract_regex(STRING， REGEX) | extract_regex&#x200B;(&quot;E259，E259B_009,1_1&quot;&#x200B;， &quot;([^，]+)，[^，]*，([^，]+)」) | [「E259、E259B_009、1_1」、「E259」、「1_1」] |
| matches_regex | 檢查字串是否符合輸入的規則運算式。 | <ul><li>字串： **必填** 您正在檢查的字串符合規則運算式。</li><li>規則運算式： **必填** 要比較的規則運算式。</li></ul> | matches_regex(STRING， REGEX) | matches_regex(&quot;E259，E259B_009,1_1&quot;， &quot;([^，]+)，[^，]*，([^，]+)」) | true |

{style="table-layout:auto"}

### 雜湊函式 {#hashing}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 取得輸入並使用安全雜湊演演算法1 (SHA-1)產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT， CHARSET) | sha1（「我的文字」、「UTF-8」） | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | 取得輸入並使用安全雜湊演演算法256 (SHA-256)產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256（輸入，字元集） | sha256（「我的文字」、「UTF-8」） | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 取得輸入並使用安全雜湊演演算法512 (SHA-512)產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512(INPUT， CHARSET) | sha512（「我的文字」、「UTF-8」） | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b7d4fd2ff68a fd24d16 |
| md5 | 取得輸入並使用MD5產生雜湊值。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5(INPUT， CHARSET) | md5（「我的文字」，「UTF-8」） | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 取得輸入使用循環冗餘檢查(CRC)演演算法來產生32位元循環代碼。 | <ul><li>輸入： **必填** 要雜湊的純文字。</li><li>字元集： *可選* 字元集的名稱。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT， CHARSET) | crc32（「我的文字」，「UTF-8」） | 8df92e80 |

{style="table-layout:auto"}

### URL函式 {#url}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 從指定的URL傳回通訊協定。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必填** 需要從中擷取通訊協定的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | 傳回指定URL的主機。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必填** 需要從中擷取主機的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 傳回指定URL的連線埠。 如果輸入無效，則會傳回null。 | <ul><li>URL： **必填** 需要從中擷取連線埠的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | 傳回指定URL的路徑。 依預設，會傳回完整路徑。 | <ul><li>URL： **必填** 需要從中擷取路徑的URL。</li><li>完整路徑(_P)： *可選* 布林值，決定是否傳回完整路徑。 若設為false，則只會傳迴路徑的結尾。</li></ul> | get_url_path&#x200B;(URL， FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B;employee.csv&quot; |
| get_url_query_str | 傳回指定URL的查詢字串，作為查詢字串名稱和查詢字串值的對應。 | <ul><li>URL： **必填** 您嘗試從中取得查詢字串的URL。</li><li>錨點： **必填** 決定要對查詢字串中的錨點做什麼。 可以是下列三個值之一：「保留」、「移除」或「附加」。<br><br>如果值為「retain」，則錨點會附加至傳回的值。<br>如果值為「remove」，則會從傳回的值中移除錨點。<br>如果值為「append」，則錨點會以個別值的形式傳回。</li></ul> | get_url_query_str&#x200B;(URL， ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there？name=&#x200B;ferret#nose&quot;， &quot;retain&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there？name=&#x200B;ferret#nose&quot;， &quot;remove&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com&#x200B;：8042/over/there&#x200B;？name=ferret#nose&quot;， &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | 此函式以URL作為輸入，並使用ASCII字元取代或編碼特殊字元。 如需特殊字元的詳細資訊，請閱讀 [特殊字元清單](#special-characters) 在本檔案附錄中。 | <ul><li>URL： **必填** 含有特殊字元的輸入URL，您要取代該輸入URL或將其編碼為ASCII字元。</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>：//example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | 此函式以URL作為輸入，並將ASCII字元解碼為特殊字元。  如需特殊字元的詳細資訊，請閱讀 [特殊字元清單](#special-characters) 在本檔案附錄中。 | <ul><li>URL： **必填** 含有ASCII字元的輸入URL，您要將其解碼成特殊字元。</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>：//example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### 日期和時間函式 {#date-and-time}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。 更多關於「 」的資訊 `date` 函式可在 [資料格式處理指南](./data-handling.md#dates).

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 擷取目前時間。 |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | 擷取目前的Unix時間。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根據指定的格式來格式化輸入日期。 | <ul><li>日期： **必填** 您要格式化的輸入日期（ZonedDateTime物件）。</li><li>格式： **必填** 您希望日期變更成的格式。</li></ul> | format（日期，格式） | 格式(2019-10-23T11:24:00+00:00， &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | 根據指定的格式將時間戳記轉換為日期字串。 | <ul><li>時間戳記： **必填** 您要格式化的時間戳記。 這會以毫秒為單位寫入。</li><li>格式： **必填** 您希望時間戳記變為的格式。</li></ul> | dformat(TIMESTAMP， FORMAT) | dformat(1571829875000， &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li><li>格式： **必填** 代表來源日期格式的字串。**注意：** 這可以 **not** 代表您要將日期字串轉換為的格式。 </li><li>DEFAULT_DATE： **必填** 如果提供的日期為Null，則傳回預設日期。</li></ul> | date(DATE， FORMAT， DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;， now()) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li><li>格式： **必填** 代表來源日期格式的字串。**注意：** 這可以 **not** 代表您要將日期字串轉換為的格式。 </li></ul> | date(DATE， FORMAT) | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 將日期字串轉換為ZonedDateTime物件（ISO 8601格式）。 | <ul><li>日期： **必填** 代表日期的字串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | 「2019-10-23T11:24:00Z英吋 |
| date_part | 擷取日期部分。 支援下列元件值： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;毫秒&quot;<br>&quot;SSS&quot; | <ul><li>元件： **必填** 代表日期組成部分的字串。 </li><li>日期： **必填** 日期（標準格式）。</li></ul> | date_part&#x200B;(COMPONENT， DATE) | date_part(&quot;MM&quot;， date(&quot;2019-10-17 11:55:12英吋)) | 10 |
| set_date_part | 取代指定日期中的元件。 接受下列元件： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>元件： **必填** 代表日期組成部分的字串。 </li><li>值： **必填** 為指定日期的元件設定的值。</li><li>日期： **必填** 日期（標準格式）。</li></ul> | set_date_part&#x200B;(COMPONENT， VALUE， DATE) | set_date_part(&quot;m&quot;， 4， date(&quot;2016-11-09T11:44:44.797英吋) | 「2016-04-09T11:44:44Z英吋 |
| make_date_time | 從零件建立日期。 此函式也可以使用make_timestamp引發。 | <ul><li>年： **必填** 年（以四位數表示）。</li><li>月： **必填** 月份。 允許的值為1到12。</li><li>日： **必填** 日。 允許的值為1到31。</li><li>小時： **必填** 小時。 允許的值為0到23。</li><li>分鐘： **必填** 分鐘。 允許的值為0到59。</li><li>納秒： **必填** 納秒值。 允許的值為0到999999999。</li><li>時區： **必填** 日期時間的時區。</li></ul> | make_date_time&#x200B;（年、月、日、小時、分鐘、秒、納秒、時區） | make_date_time&#x200B;（2019， 10， 17， 11， 55， 12， 999， 「美洲/洛杉磯」） | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 將任何時區的日期轉換為UTC格式的日期。 | <ul><li>日期： **必填** 您嘗試轉換的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 將日期從一個時區轉換為另一個時區。 | <ul><li>日期： **必填** 您嘗試轉換的日期。</li><li>區域： **必填** 您嘗試將日期轉換為的時區。</li></ul> | zone_date_to_zone&#x200B;(DATE， ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### 階層 — 物件 {#objects}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 檢查物件是否為空白。 | <ul><li>輸入： **必填** 您嘗試檢查的物件是空的。</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 建立物件清單。 | <ul><li>輸入： **必填** 索引鍵和陣列配對的群組。</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 根據給定的平面索引鍵/值組建立物件。 | <ul><li>輸入： **必填** 索引鍵/值配對的平面清單。</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;， &quot;John&quot;， &quot;lastName&quot;， &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 從輸入字串建立物件。 | <ul><li>字串： **必填** 正在剖析以建立物件的字串。</li><li>VALUE_DELIMITER： *可選* 分隔欄位與值的分隔字元。 預設分隔符號為 `:`.</li><li>FIELD_DELIMITER： *可選* 分隔欄位值配對的分隔字元。 預設分隔符號為 `,`.</li></ul> | str_to_object&#x200B;(STRING， VALUE_DELIMITER， FIELD_DELIMITER) **注意**：您可以使用 `get()` 函式以及 `str_to_object()` 擷取字串中索引鍵的值。 | <ul><li>範例#1： str_to_object(&quot;firstName - John ； lastName - ； - 123 345 7890&quot;， &quot;-&quot;， &quot;；&quot;)</li><li>範例#2： str_to_object(&quot;firstName - John ； lastName - ； phone - 123 456 7890&quot;， &quot;-&quot;， &quot;；&quot;)。get(&quot;firstName&quot;)</li></ul> | <ul><li>範例#1：`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>範例#2： &quot;John&quot;</li></ul> |
| contains_key | 檢查物件是否存在於來源資料中。 **注意：** 此函式取代已棄用的 `is_set()` 函式。 | <ul><li>輸入： **必填** 要檢查的路徑（如果存在於來源資料中）。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 無效 | 將屬性的值設定為 `null`. 當您不想將欄位複製到目標結構描述時，應使用此選項。 |  | nullify() | nullify() | `null` |
| get_keys | 剖析索引鍵/值配對並傳回所有索引鍵。 | <ul><li>物件： **必填** 從中擷取索引鍵的物件。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;： &quot;Pride and Impance&quot;， &quot;book2&quot;： &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 根據指定的索引鍵，剖析索引鍵/值配對並傳回字串的值。 | <ul><li>字串： **必填** 您要剖析的字串。</li><li>索引鍵： **必填** 必須為其擷取值的索引鍵。</li><li>VALUE_DELIMITER： **必填** 分隔欄位和值的分隔字元。 若以下其中一個 `null` 或提供了空字串，則此值為 `:`.</li><li>FIELD_DELIMITER： *可選* 分隔欄位和值配對的分隔字元。 若以下其中一個 `null` 或提供了空字串，則此值為 `,`.</li></ul> | get_values(STRING， KEY， VALUE_DELIMITER， FIELD_DELIMITER) | get_values(\&quot;firstName - John ， lastName - Cena ， phone - 555 420 8692\&quot;， \&quot;firstName\&quot;， \&quot;-\&quot;， \&quot;，\&quot;) | John |

{style="table-layout:auto"}

如需物件複製功能的詳細資訊，請參閱區段 [以下](#object-copy).

### 階層 — 陣列 {#arrays}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 合併 | 傳回給定陣列中的第一個非null物件。 | <ul><li>輸入： **必填** 您要尋找的第一個非null物件的陣列。</li></ul> | coalesce(INPUT) | coalesce(null， null， null， first」， null， second」) | &quot;first&quot; |
| 第一個 | 擷取給定陣列的第一個元素。 | <ul><li>輸入： **必填** 您要尋找第一個元素的陣列。</li></ul> | first(INPUT) | first(&quot;1&quot;， &quot;2&quot;， &quot;3&quot;) | &quot;1&quot; |
| 最後 | 擷取給定陣列的最後一個元素。 | <ul><li>輸入： **必填** 您要尋找的最後一個元素的陣列。</li></ul> | last(INPUT) | last(&quot;1&quot;， &quot;2&quot;， &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 將元素新增至陣列結尾。 | <ul><li>陣列： **必填** 您要新增元素的陣列。</li><li>VALUES：您要附加至陣列的元素。</li></ul> | add_to_array&#x200B;(ARRAY， VALUES) | add_to_array&#x200B;([&#39;a&#39;、&#39;b&#39;]， &#39;c&#39;， &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| join_array | 將陣列彼此結合。 | <ul><li>陣列： **必填** 您要新增元素的陣列。</li><li>VALUES：您要附加至父陣列的陣列。</li></ul> | join_arrays&#x200B;(ARRAY， VALUES) | join_arrays&#x200B;([&#39;a&#39;、&#39;b&#39;]， [&#39;c&#39;]， [&#39;d&#39;， &#39;e&#39;]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;] |
| to_array | 取得輸入清單並將其轉換為陣列。 | <ul><li>INCLUDE_NULLS： **必填** 指示是否要在回應陣列中包含null的布林值。</li><li>值： **必填** 要轉換為陣列的元素。</li></ul> | to_array&#x200B;(INCLUDE_NULLS， VALUES) | to_array(false， 1， null， 2， 3) | `[1, 2, 3]` |
| size_of | 傳回輸入的大小。 | <ul><li>輸入： **必填** 您嘗試尋找的物件大小。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函式用於將整個輸入陣列中的所有元素附加到Profile中陣列的結尾。 此函式為 **僅限** 適用於更新期間。 如果在插入內容中使用，此函式會依原樣傳回輸入。 | <ul><li>陣列： **必填** 要在設定檔中附加陣列的陣列。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | 此函式用於取代陣列中的元素。 此函式為 **僅限** 適用於更新期間。 如果在插入內容中使用，此函式會依原樣傳回輸入。 | <ul><li>陣列： **必填** 用來取代設定檔中陣列的陣列。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |

{style="table-layout:auto"}

### 邏輯運運算元 {#logical-operators}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | 指定索引鍵和以陣列形式平面化的索引鍵值配對清單，如果找到索引鍵，此函式會傳回值，如果陣列中存在索引鍵，則會傳回預設值。 | <ul><li>索引鍵： **必填** 要比對的金鑰。</li><li>OPTIONS： **必填** 索引鍵/值配對的平面化陣列。 您可以選擇將預設值放在結尾。</li></ul> | decode(KEY， OPTIONS) | decode(stateCode， &quot;ca&quot;， &quot;California&quot;， &quot;pa&quot;， &quot;Pennsylvania&quot;， &quot;N/A&quot;) | 如果指定的stateCode是&quot;ca&quot;、&quot;California&quot;。<br>如果指定的stateCode為「pa」、「Pennsylvania」。<br>如果stateCode不符合下列內容，「不適用」。 |
| iif | 評估給定的布林運算式，並根據結果傳回指定的值。 | <ul><li>運算式： **必填** 正在評估的布林運算式。</li><li>真值： **必填** 運算式評估為true時傳回的值。</li><li>FALSE_VALUE： **必填** 運算式評估為false時傳回的值。</li></ul> | iif（運算式，TRUE_VALUE，FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### 聚合 {#aggregation}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 傳回給定引數的最小值。 使用自然排序。 | <ul><li>OPTIONS： **必填** 可以相互比較的一或多個物件。</li></ul> | min(OPTIONS) | min(3， 1， 4) | 1 |
| max | 傳回給定引數的最大值。 使用自然排序。 | <ul><li>OPTIONS： **必填** 可以相互比較的一或多個物件。</li></ul> | 最大(OPTIONS) | max(3， 1， 4) | 4 |

{style="table-layout:auto"}

### 型別轉換 {#type-conversions}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 將字串轉換為BigInteger。 | <ul><li>字串： **必填** 要轉換為BigInteger的字串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 將字串轉換為雙精度型別。 | <ul><li>字串： **必填** 要轉換為Double的字串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 將字串轉換為浮點數。 | <ul><li>字串： **必填** 要轉換為浮點數的字串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 將字串轉換為整數。 | <ul><li>字串： **必填** 要轉換為整數的字串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON函式 {#json}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 從指定的字串將JSON內容還原序列化。 | <ul><li>字串： **必填** 要還原序列化的JSON字串。</li></ul> | json_to_object&#x200B;(STRING) | &#x200B; json_to_object({&quot;info&quot;：{&quot;firstName&quot;：&quot;John&quot;，&quot;lastName&quot;： &quot;Doe&quot;}}) | 代表JSON的物件。 |

{style="table-layout:auto"}

### 特殊作業 {#special-operations}

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 產生偽隨機ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | 此函式接受FPID字串並將其轉換為ECID，以便用於Adobe Experience Platform和Adobe Experience Cloud應用程式。 | <ul><li>字串： **必填** 要轉換為ECID的FPID字串。</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### 使用者代理程式功能 {#user-agent}

下表包含的任何使用者代理程式函式都可以傳回下列任一值：

* 電話 — 具有小熒幕的行動裝置（通常小於7英吋）
* 行動 — 尚未識別的行動裝置。 此行動裝置可以是電子閱讀器、平板電腦、手機、手錶等。

如需裝置欄位值的詳細資訊，請閱讀 [裝置欄位值清單](#device-field-values) 在本檔案附錄中。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 範例輸出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 從使用者代理程式字串中擷取作業系統名稱。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 從使用者代理程式字串中擷取作業系統的主要版本。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 從使用者代理程式字串中擷取作業系統的版本。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 從使用者代理字串中擷取作業系統的名稱和版本。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 從使用者代理字串中擷取代理程式版本。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 從使用者代理字串中擷取代理程式名稱和主要版本。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 從使用者代理字串中擷取代理名稱。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 從使用者代理程式字串中擷取裝置類別。 | <ul><li>USER_AGENT： **必填** 使用者代理字串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Phone |

{style="table-layout:auto"}

### 物件副本 {#object-copy}

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

在上述範例中， `city` 和 `state` 屬性也會在執行階段自動擷取，因為 `address` 物件已對應至 `addr`. 如果您要建立 `line2` XDM結構中的屬性，而您的輸入資料也包含 `line2` 在 `address` 物件，則也會自動擷取，而不需要手動變更對應。

若要確保自動對應可正常運作，必須符合下列先決條件：

* 父層級物件應該對應；
* 必須在XDM結構描述中建立新屬性；
* 新屬性在來源結構描述和XDM結構描述中應有相符的名稱。

如果不滿足任何先決條件，則必須使用資料準備手動將來源結構描述對應到XDM結構描述。

## 附录

以下提供使用「資料準備」對應函式的其他資訊

### 特殊字符 {#special-characters}

下表概述保留字元及其對應的編碼字元清單。

| 保留字元 | 已編碼的字元 |
| --- | --- |
| 空間 | %20 |
| ！ | %21 |
| ” | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ） | %29 |
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

### 裝置欄位值 {#device-field-values}

下表概述裝置欄位值清單及其對應說明。

| 设备 | 描述 |
| --- | --- |
| 台式机 | 桌上型電腦或筆記型電腦型別的裝置。 |
| 匿名 | 匿名裝置。 在某些情況下，這些是 `useragents` 已遭匿名化軟體變更的資料。 |
| 未知 | 未知的裝置。 這些通常是 `useragents` 未包含裝置相關資訊的檔案。 |
| 移动设备 | 尚未識別的行動裝置。 此行動裝置可以是電子閱讀器、平板電腦、手機、手錶等。 |
| 平板電腦 | 具有大熒幕的行動裝置（通常> 7英吋）。 |
| Phone | 小熒幕（通常&lt; 7英吋）的行動裝置。 |
| 觀看 | 具有小熒幕（通常小於2英吋）的行動裝置。 這些裝置通常可作為手機/平板電腦型別裝置的額外畫面。 |
| 增強現實 | 具有AR功能的行動裝置。 |
| Virtual Reality | 具備VR功能的行動裝置。 |
| 電子閱讀器 | 類似於平板電腦的裝置，但通常具有 [!DNL eInk] 畫面。 |
| 機上盒 | 連線裝置，允許透過電視大小的熒幕互動。 |
| TV | 類似機頂盒但內建於電視機中的裝置。 |
| 家用電器 | （通常為大型）家用電器，如冰箱。 |
| 遊戲主機 | 固定式遊戲系統，如 [!DNL Playstation] 或 [!DNL XBox]. |
| 手持式遊戲機 | 行動遊戲系統，如 [!DNL Nintendo Switch]. |
| 語音 | 語音導向裝置，例如 [!DNL Amazon Alexa] 或 [!DNL Google Home]. |
| 汽車 | 車輛瀏覽器。 |
| 自動機制 | 造訪網站的機器人。 |
| 自動機制行動 | 造訪網站但表示希望被視為行動訪客的機器人。 |
| 自動機制模擬器 | 造訪網站的機器人，假裝是機器人之類的 [!DNL Google]，但事實並非如此。 **注意**：在大多數情況下，機器人模仿者確實是機器人。 |
| Cloud | 雲端型應用程式。 這些都不是機器人或駭客，而是需要連線的應用程式。 其中包括 [!DNL Mastodon] 伺服器。 |
| 駭客 | 若在中偵測到指令碼，則會使用此裝置值 `useragent` 字串。 |

{style="table-layout:auto"}