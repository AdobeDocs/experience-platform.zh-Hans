---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；ui指南；映射器；映射；映射字段；映射函数；
solution: Experience Platform
title: 数据准备映射函数
description: 本文档介绍了与数据准备一起使用的映射函数。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '6009'
ht-degree: 1%

---

# 数据准备映射函数

数据准备函数可用于根据在源字段中输入的内容计算和计算值。

## 字段

字段名称可以是任何合法标识符 — 由字母、美元符号(`$`)或下划线字符(`_`)开头的Unicode字母和数字构成的无限长序列。 变量名称也区分大小写。

如果字段名称不遵循此约定，则字段名称必须用`${}`括起来。 因此，例如，如果字段名称为“First Name”或“First.Name”，则名称必须分别像`${First Name}`或`${First\.Name}`一样换行。

>[!TIP]
>
>与层次结构交互时，如果子属性具有句点(`.`)，则必须使用反斜杠(`\`)对特殊字符进行转义。 有关详细信息，请阅读[转义特殊字符](home.md#escape-special-characters)的指南。

如果字段名称是以下保留关键字的&#x200B;**any**，则必须使用`${}{}`括起来：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

此外，保留的关键字还包括此页面上列出的任何映射器函数。

可使用点表示法访问子字段中的数据。 例如，如果存在`name`对象，要访问`firstName`字段，请使用`name.firstName`。

## 函数列表

下表列出了所有支持的映射函数，包括示例表达式及其生成的输出。

### 字符串函数 {#string}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 连接给定的字符串。 | <ul><li>STRING：将连接的字符串。</li></ul> | concat(STRING_1， STRING_2) | concat（“嗨，”，“那里”，“！”） | `"Hi, there!"` |
| 分解 | 根据正则表达式拆分字符串并返回部分的数组。 可以选择包含正则表达式以拆分字符串。 默认情况下，拆分解析为“，”。 以下分隔符&#x200B;**需要**&#x200B;使用`\`进行转义： `+, ?, ^, \|, ., [, (, {, ), *, $, \`如果您包含多个字符作为分隔符，则分隔符将被视为多字符分隔符。 | <ul><li>字符串： **必需**&#x200B;需要拆分的字符串。</li><li>REGEX： *可选*&#x200B;可用于拆分字符串的正则表达式。</li></ul> | explode(STRING， REGEX) | explode（“嗨，那里！”，“ ”） | `["Hi,", "there"]` |
| 实例 | 返回子字符串的位置/索引。 | <ul><li>输入： **必需**&#x200B;正在搜索的字符串。</li><li>SUBSTRING： **必需**&#x200B;在字符串中搜索的子字符串。</li><li>START_POSITION： *可选*&#x200B;字符串中开始查找的位置。</li><li>发生次数： *可选*&#x200B;要从起始位置查找的第n个发生次数。 默认情况下，该值为1。 </li></ul> | instr(INPUT， SUBSTRING， START_POSITION， OCCURRENCE) | instr(“adobe.com”，“com”) | 6 |
| 替换器 | 替换原始字符串中存在的搜索字符串。 | <ul><li>输入： **必需**&#x200B;输入字符串。</li><li>TO_FIND： **必需**&#x200B;要在输入中查找的字符串。</li><li>TO_REPLACE： **必需**&#x200B;将替换“TO_FIND”中的值的字符串。</li></ul> | replacestr(INPUT， TO_FIND， TO_REPLACE) | replacestr(&quot;This is a string re test&quot;， &quot;re&quot;， &quot;replace&quot;) | “这是一个字符串替换测试” |
| substr | 返回给定长度的子字符串。 | <ul><li>输入： **必需**&#x200B;输入字符串。</li><li>START_INDEX： **必需**&#x200B;子字符串开始处的输入字符串的索引。</li><li>长度： **必需**&#x200B;子字符串的长度。</li></ul> | substr(INPUT， START_INDEX， LENGTH) | substr（“这是一个子字符串测试”，7、8） | &quot;一个子集&quot; |
| 小写/<br>lcase | 将字符串转换为小写。 | <ul><li>输入： **必需**&#x200B;将转换为小写的字符串。</li></ul> | lower(INPUT) | lower(“HeLlO”)<br>lcase(“HeLlO”) | &quot;hello&quot; |
| upper /<br>ucase | 将字符串转换为大写。 | <ul><li>输入： **必需**&#x200B;将转换为大写的字符串。</li></ul> | upper(INPUT) | upper(“HeLlO”)<br>ucase(“HeLlO”) | “HELLO” |
| split | 在分隔符上拆分输入字符串。 以下分隔符&#x200B;**需要**&#x200B;使用`\`进行转义： `\`。 如果您包含多个分隔符，则字符串将拆分到字符串中存在的&#x200B;**any**&#x200B;个分隔符中。 **注意：**&#x200B;此函数只从字符串返回非null索引，而不管是否存在分隔符。 如果结果数组中需要所有索引（包括null），请改用“explode”函数。 | <ul><li>INPUT： **必需**&#x200B;要拆分的输入字符串。</li><li>SEPARATOR： **必需**&#x200B;用于拆分输入的字符串。</li></ul> | split（输入，分隔符） | split(“Hello world”，“ ”) | `["Hello", "world"]` |
| 加入 | 使用分隔符连接对象列表。 | <ul><li>分隔符： **必需**&#x200B;用于连接对象的字符串。</li><li>对象： **必需**&#x200B;将要联接的字符串数组。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | “Hello world” |
| lpad | 将字符串的左侧与另一个给定的字符串填充。 | <ul><li>输入： **必需**&#x200B;要填充的字符串。 此字符串可以为null。</li><li>计数： **必需**&#x200B;要填充的字符串的大小。</li><li>填充： **必需**&#x200B;用于填充输入的字符串。 如果为null或为空，则将被视为单个空格。</li></ul> | lpad（输入、计数、填充） | lpad(“bat”， 8， “yz”) | &quot;yzybat&quot; |
| rpad | 将字符串的右侧与另一个给定的字符串相贴合。 | <ul><li>输入： **必需**&#x200B;要填充的字符串。 此字符串可以为null。</li><li>计数： **必需**&#x200B;要填充的字符串的大小。</li><li>填充： **必需**&#x200B;用于填充输入的字符串。 如果为null或为空，则将被视为单个空格。</li></ul> | rpad（输入、计数、填充） | rpad(“bat”， 8， “yz”) | “batyzyzy” |
| 左侧 | 获取给定字符串的前“n”个字符。 | <ul><li>字符串： **必需**&#x200B;要获取前“n”个字符的字符串。</li><li>计数： **必需**&#x200B;要从字符串中获取的“n”个字符。</li></ul> | left(STRING， COUNT) | left(“abcde”， 2) | &quot;ab&quot; |
| 右 | 获取给定字符串的最后“n”个字符。 | <ul><li>字符串： **必需**&#x200B;要获取最后“n”个字符的字符串。</li><li>计数： **必需**&#x200B;要从字符串中获取的“n”个字符。</li></ul> | right(STRING， COUNT) | right(“abcde”， 2) | &quot;de&quot; |
| ltrim | 删除字符串开头的空格。 | <ul><li>字符串： **必需**&#x200B;要删除空白的字符串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 删除字符串末尾的空格。 | <ul><li>字符串： **必需**&#x200B;要删除空白的字符串。</li></ul> | rtrim(STRING) | rtrim(“hello ”) | &quot;hello&quot; |
| trim | 删除字符串开头和结尾的空格。 | <ul><li>字符串： **必需**&#x200B;要删除空白的字符串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 等于 | 比较两个字符串以确认它们是否相等。 此函数区分大小写。 | <ul><li>STRING1： **必需**&#x200B;要比较的第一个字符串。</li><li>STRING2： **必需**&#x200B;要比较的第二个字符串。</li></ul> | STRING1. &#x200B;equals(&#x200B;STRING2) | “string1”。&#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比较两个字符串以确认它们是否相等。 此函数为&#x200B;**而非**&#x200B;区分大小写。 | <ul><li>STRING1： **必需**&#x200B;要比较的第一个字符串。</li><li>STRING2： **必需**&#x200B;要比较的第二个字符串。</li></ul> | STRING1. &#x200B;equalsIgnoreCase&#x200B;(STRING2) | “string1”。&#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### 正则表达式函数

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根据正则表达式从输入字符串中提取组。 | <ul><li>字符串： **必需**&#x200B;从中提取组的字符串。</li><li>REGEX： **必需**&#x200B;您希望组匹配的正则表达式。</li></ul> | extract_regex(STRING， REGEX) | extract_regex&#x200B;(&quot;E259，E259B_009,1_1&quot;&#x200B;， &quot;([^，]+)，[^，]*，([^，]+)&quot;) | [&quot;E259，E259B_009,1_1&quot;，&quot;E259&quot;，&quot;1_1&quot;] |
| matches_regex | 检查字符串是否与输入的正则表达式匹配。 | <ul><li>字符串： **必需**&#x200B;要检查的字符串与正则表达式匹配。</li><li>REGEX： **必需**&#x200B;要与之进行比较的正则表达式。</li></ul> | matches_regex(STRING， REGEX) | matches_regex(&quot;E259，E259B_009,1_1&quot;， &quot;([^，]+)，[^，]*，([^，]+)&quot;) | true |

{style="table-layout:auto"}

### 哈希函数 {#hashing}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 接受输入并使用安全哈希算法1 (SHA-1)生成哈希值。 | <ul><li>输入： **必需**&#x200B;要散列的纯文本。</li><li>CHARSET： *可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1（输入，字符集） | sha1（“我的文本”，“UTF-8”） | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | 采用输入并使用安全哈希算法256 (SHA-256)生成哈希值。 | <ul><li>输入： **必需**&#x200B;要散列的纯文本。</li><li>CHARSET： *可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256（输入，字符集） | sha256（“我的文本”，“UTF-8”） | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 采用输入并使用安全哈希算法512 (SHA-512)生成哈希值。 | <ul><li>输入： **必需**&#x200B;要散列的纯文本。</li><li>CHARSET： *可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512（输入，字符集） | sha512（“我的文本”，“UTF-8”） | A.B. a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b386d4fd2ff68a |
| md5 | 接受输入并使用MD5生成哈希值。 | <ul><li>输入： **必需**&#x200B;要散列的纯文本。</li><li>CHARSET： *可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5（输入，字符集） | md5（“我的文本”，“UTF-8”） | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 取一个输入使用循环冗余校验(CRC)算法来生成32位循环代码。 | <ul><li>输入： **必需**&#x200B;要散列的纯文本。</li><li>CHARSET： *可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32（输入，字符集） | crc32（“我的文本”，“UTF-8”） | 8df92e80 |

{style="table-layout:auto"}

### URL函数 {#url}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 从给定URL返回协议。 如果输入无效，则返回空值。 | <ul><li>URL： **必需**&#x200B;需要从中提取协议的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | 返回给定URL的主机。 如果输入无效，则返回空值。 | <ul><li>URL： **必需**&#x200B;需要从中提取主机的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 返回给定URL的端口。 如果输入无效，则返回空值。 | <ul><li>URL： **必需**&#x200B;需要从中提取端口的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | 返回给定URL的路径。 默认情况下，将返回完整路径。 | <ul><li>URL： **必需**&#x200B;需要从中提取路径的URL。</li><li>FULL_PATH： *可选*&#x200B;一个布尔值，用于确定是否返回完整路径。 如果设置为false，则仅返回路径的结尾。</li></ul> | get_url_path&#x200B;(URL， FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B;employee.csv&quot; |
| get_url_query_str | 返回给定URL的查询字符串作为查询字符串名称和查询字符串值的映射。 | <ul><li>URL： **必需**&#x200B;尝试从中获取查询字符串的URL。</li><li>锚点： **必需**&#x200B;确定如何处理查询字符串中的锚点。 可以是以下三个值之一：“保留”、“移除”或“附加”。<br><br>如果该值为“保留”，则锚点将附加到返回的值。<br>如果值为“remove”，则将从返回值中删除锚点。<br>如果值为“附加”，则锚点将作为单独值返回。</li></ul> | get_url_query_str&#x200B;(URL， ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042/over&#x200B;/there？name=&#x200B;ferret#nose&quot;， &quot;retain&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042/over&#x200B; &#x200B; &#x200B; &#x200B; &#x200B;/there？name=ferret#nose&quot;， &quot;remove&quot;)<br>get_url_query_str(&quot;foo://example.com:8042/over/there？name=ferret#nose&quot;， &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | 此函数将URL作为输入，并使用ASCII字符替换或编码特殊字符。 有关特殊字符的详细信息，请阅读本文档附录中的[特殊字符列表](#special-characters)。 | <ul><li>URL： **必需**&#x200B;包含要替换或编码为ASCII字符的特殊字符的输入URL。</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>：//example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | 此函数以URL作为输入并将ASCII字符解码为特殊字符。  有关特殊字符的详细信息，请阅读本文档附录中的[特殊字符列表](#special-characters)。 | <ul><li>URL： **必需**&#x200B;包含要解码为特殊字符的ASCII字符的输入URL。</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>：//example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### 日期和时间函数 {#date-and-time}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。 有关`date`函数的更多信息，请参阅[数据格式处理指南](./data-handling.md#dates)的日期部分。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 检索当前时间。 | | now() | now() | `2021-10-26T10:10:24Z` |
| 时间戳 | 检索当前Unix时间。 | | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根据指定的格式设置输入日期的格式。 | <ul><li>日期： **必需**&#x200B;要设置格式的输入日期，即ZonedDateTime对象。</li><li>格式： **必需**&#x200B;要将日期更改为的格式。</li></ul> | format（日期，格式） | format(2019-10-23T11:24:00+00:00， &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | 根据指定的格式将时间戳转换为日期字符串。 | <ul><li>时间戳： **必需**&#x200B;要设置格式的时间戳。 这是以毫秒为单位编写的。</li><li>格式： **必需**&#x200B;您希望时间戳变为的格式。</li></ul> | dformat(TIMESTAMP， FORMAT) | dformat(1571829875000， &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需**&#x200B;表示日期的字符串。</li><li>格式： **必需**&#x200B;表示源日期格式的字符串。**注意：**&#x200B;这&#x200B;**不**&#x200B;表示要将日期字符串转换为的格式。 </li><li>DEFAULT_DATE： **必需**&#x200B;如果提供的日期为null，则返回默认日期。</li></ul> | date(DATE， FORMAT， DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH:mm&quot;， now()) | `2019-10-23T11:24:00Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需**&#x200B;表示日期的字符串。</li><li>格式： **必需**&#x200B;表示源日期格式的字符串。**注意：**&#x200B;这&#x200B;**不**&#x200B;表示要将日期字符串转换为的格式。 </li></ul> | 日期（日期，格式） | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需**&#x200B;表示日期的字符串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | “2019-10-23T11:24:00Z” |
| date_part | 检索日期的各个部分。 支持以下组件值： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;{20&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> | <ul><li>组件： **必需**&#x200B;表示日期部分的字符串。 </li><li>日期： **必需**&#x200B;标准格式的日期。</li></ul> | date_part&#x200B;(COMPONENT， DATE) | date_part(&quot;MM&quot;， date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 替换给定日期中的组件。 接受以下组件： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>组件： **必需**&#x200B;表示日期部分的字符串。 </li><li>值： **必需**&#x200B;为给定日期的组件设置的值。</li><li>日期： **必需**&#x200B;标准格式的日期。</li></ul> | set_date_part&#x200B;(COMPONENT， VALUE， DATE) | set_date_part(&quot;m&quot;， 4， date(&quot;2016-11-09T11:44:44.797&quot;) | “2016-04-09T11:44:44Z” |
| make_date_time | 从部件创建日期。 此函数也可以使用make_timestamp进行感应。 | <ul><li>YEAR： **必需**&#x200B;用四位数字表示的年份。</li><li>月份： **必需**&#x200B;月份。 允许的值为1到12。</li><li>日： **必需**&#x200B;日。 允许的值为1到31。</li><li>小时：**必需**&#x200B;小时。 允许的值为0到23。</li><li>MINUTE： **必需**&#x200B;分钟。 允许的值为0到59。</li><li>NANOSECOND： **必需**&#x200B;纳秒值。 允许的值为0到999999999。</li><li>时区： **必需**&#x200B;日期时间的时区。</li></ul> | make_date_time&#x200B;（年、月、日、小时、分钟、秒、纳秒、时区） | make_date_time&#x200B;（2019， 10， 17， 11， 55， 12， 999，“美国/洛杉矶”） | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 将任何时区的日期转换为UTC格式的日期。 | <ul><li>日期： **必需**&#x200B;尝试转换的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 将日期从一个时区转换为另一个时区。 | <ul><li>日期： **必需**&#x200B;尝试转换的日期。</li><li>区域： **必需**&#x200B;您尝试将日期转换为的时区。</li></ul> | zone_date_to_zone&#x200B;(DATE， ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### 层次结构 — 对象 {#objects}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 检查对象是否为空。 | <ul><li>输入： **必需**&#x200B;您尝试检查的对象为空。</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 创建对象列表。 | <ul><li>输入： **必需**&#x200B;键和数组对的分组。</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 根据给定的平面键/值对创建对象。 | <ul><li>输入： **必需**&#x200B;键/值对的平面列表。</li></ul> | to_object(INPUT) | to_object&#x200B;(“firstName”、“John”、“lastName”、“Doe”) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 从输入字符串创建对象。 | <ul><li>字符串： **必需**&#x200B;正在分析以创建对象的字符串。</li><li>VALUE_DELIMITER： *可选*&#x200B;用于将字段与值分开的分隔符。 默认分隔符为`:`。</li><li>FIELD_DELIMITER： *可选*&#x200B;用于分隔字段值对的分隔符。 默认分隔符为`,`。</li></ul> | str_to_object&#x200B;(STRING， VALUE_DELIMITER， FIELD_DELIMITER) **注意**：您可以使用`get()`函数以及`str_to_object()`来检索字符串中键的值。 | <ul><li>示例#1： str_to_object(&quot;firstName - John ； lastName - ； - 123 345 7890&quot;， &quot;-&quot;， &quot;；&quot;)</li><li>示例#2： str_to_object(&quot;firstName - John ； lastName - ； phone - 123 456 7890&quot;， &quot;-&quot;， &quot;；&quot;)。get(&quot;firstName&quot;)</li></ul> | <ul><li>示例#1：`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>示例#2： &quot;John&quot;</li></ul> |
| contains_key | 检查源数据中是否存在该对象。 **注意：**&#x200B;此函数替换已弃用的`is_set()`函数。 | <ul><li>输入： **必需**&#x200B;要检查的路径是否存在于源数据中。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 无效 | 将属性的值设置为`null`。 当您不想将字段复制到目标架构时，应使用此字段。 | | nullify() | nullify() | `null` |
| get_keys | 解析键/值对并返回所有键。 | <ul><li>对象： **必需**&#x200B;从中提取键的对象。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;： “Pride and Visimit”， “book2”： “1984”}) | `["book1", "book2"]` |
| get_values | 解析键/值对并根据给定的键返回字符串的值。 | <ul><li>字符串： **必需**&#x200B;要分析的字符串。</li><li>KEY： **必需**&#x200B;必须提取其值的键。</li><li>VALUE_DELIMITER： **必需**&#x200B;用于分隔字段和值的分隔符。 如果提供了`null`或空字符串，则此值为`:`。</li><li>FIELD_DELIMITER： *可选*&#x200B;用于分隔字段和值对的分隔符。 如果提供了`null`或空字符串，则此值为`,`。</li></ul> | get_values(STRING， KEY， VALUE_DELIMITER， FIELD_DELIMITER) | get_values(\&quot;firstName - John ， lastName - Cena ， phone - 555 420 8692\&quot;， \&quot;firstName\&quot;， \&quot;-\&quot;， \&quot;，\&quot;) | John |
| map_get_values | 获取映射和键输入。 如果输入是单个键，则函数返回与该键关联的值。 如果输入是字符串数组，则函数返回与提供的键对应的所有值。 如果传入的映射具有重复的键，则返回值必须删除重复的键并返回唯一值。 | <ul><li>映射： **必需**&#x200B;输入映射数据。</li><li>密钥： **必需**&#x200B;密钥可以是单个字符串或字符串数组。 如果提供了任何其他基元类型（数据/数字），则会将其视为字符串。</li></ul> | get_values(MAP， KEY) | 有关代码示例，请参阅[附录](#map_get_values)。 | |
| map_has_keys | 如果提供了一个或多个输入键，则函数返回true。 如果提供字符串数组作为输入，则函数在找到的第一个键上返回true。 | <ul><li>映射： **必需**&#x200B;输入映射数据</li><li>密钥： **必需**&#x200B;密钥可以是单个字符串或字符串数组。 如果提供了任何其他基元类型（数据/数字），则会将其视为字符串。</li></ul> | map_has_keys(MAP， KEY) | 有关代码示例，请参阅[附录](#map_has_keys)。 | |
| add_to_map | 接受至少两个输入。 可以提供任意数量的映射作为输入。 数据准备返回具有来自所有输入的所有键值对的单个映射。 如果一个或多个键重复（在同一映射中或跨映射），数据准备会删除重复的键，以便第一个键值对按它们在输入中传递的顺序持续存在。 | 映射： **必需**&#x200B;输入映射数据。 | add_to_map(MAP 1， MAP 2， MAP 3， ...) | 有关代码示例，请参阅[附录](#add_to_map)。 | |
| object_to_map（语法1） | 使用此函数可创建Map数据类型。 | <ul><li>密钥： **必需的**&#x200B;密钥必须是字符串。 如果提供了任何其他基元值（如整数或日期），则它们会自动转换为字符串并被视为字符串。</li><li>ANY_TYPE： **必需**&#x200B;引用除映射之外的任何受支持的XDM数据类型。</li></ul> | object_to_map(KEY， ANY_TYPE， KEY， ANY_TYPE， ... ) | 有关代码示例，请参阅[附录](#object_to_map)。 | |
| object_to_map（语法2） | 使用此函数可创建Map数据类型。 | <ul><li>对象： **必需**&#x200B;您可以提供传入对象或对象数组，并以键的形式指向对象内的属性。</li></ul> | object_to_map(OBJECT) | 有关代码示例，请参阅[附录](#object_to_map)。 |
| object_to_map（语法3） | 使用此函数可创建Map数据类型。 | <ul><li>对象： **必需**&#x200B;您可以提供传入对象或对象数组，并以键的形式指向对象内的属性。</li></ul> | object_to_map(OBJECT_ARRAY， ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | 有关代码示例，请参阅[附录](#object_to_map)。 |

{style="table-layout:auto"}

有关对象复制功能的信息，请参阅下面的[部分](#object-copy)。

### 层次结构 — 数组 {#arrays}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 合并 | 返回给定数组中的第一个非空对象。 | <ul><li>INPUT： **必需**&#x200B;要查找的第一个非null对象的数组。</li></ul> | coalesce（输入） | coalesce(null， null， null， first， null， second) | &quot;first&quot; |
| 第一 | 检索给定数组的第一个元素。 | <ul><li>输入： **必需**&#x200B;要查找的第一个元素的数组。</li></ul> | 第一（输入） | first(“1”、“2”、“3”) | &quot;1&quot; |
| 过去 | 检索给定数组的最后一个元素。 | <ul><li>输入： **必需**&#x200B;要查找的最后一个元素的数组。</li></ul> | last(INPUT) | last(“1”、“2”、“3”) | “3” |
| add_to_array | 将元素添加到数组的末尾。 | <ul><li>数组： **必需**&#x200B;要将元素添加到的数组。</li><li>VALUES：要附加到数组的元素。</li></ul> | add_to_array&#x200B;(ARRAY， VALUES) | add_to_array&#x200B;([&#39;a&#39;， &#39;b&#39;]， &#39;c&#39;， &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| join_array | 将数组彼此组合在一起。 | <ul><li>数组： **必需**&#x200B;要将元素添加到的数组。</li><li>值：要附加到父数组的数组。</li></ul> | join_arrays&#x200B;(ARRAY， VALUES) | join_arrays&#x200B;([&#39;a&#39;， &#39;b&#39;]， [&#39;c&#39;]， [&#39;d&#39;， &#39;e&#39;]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;] |
| to_array | 采用输入列表并将其转换为数组。 | <ul><li>INCLUDE_NULLS： **必需**&#x200B;布尔值，用于指示响应数组中是否包含null。</li><li>值： **必需**&#x200B;要转换为数组的元素。</li></ul> | to_array&#x200B;(INCLUDE_NULLS， VALUES) | to_array(false， 1， null， 2， 3) | `[1, 2, 3]` |
| 大小_of | 返回输入的大小。 | <ul><li>INPUT： **必需**&#x200B;您尝试查找大小的对象。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函数用于将整个输入数组中的所有元素附加到配置文件中数组的末尾。 此函数仅&#x200B;**适用**&#x200B;于更新期间。 如果在插入的上下文中使用，则此函数按原样返回输入。 | <ul><li>数组： **必需**&#x200B;要在配置文件中附加数组的数组。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123， 456] |
| upsert_array_replace | 此函数用于替换数组中的元素。 此函数仅&#x200B;**适用**&#x200B;于更新期间。 如果在插入的上下文中使用，则此函数按原样返回输入。 | <ul><li>数组： **必需**&#x200B;要替换配置文件中数组的数组。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123， 456] |
| [!BADGE 仅限目标]{type=Informative} array_to_string | 使用指定的分隔符连接数组中元素的字符串表示形式。 如果数组是多维数组，则在连接前将其扁平化。 **注意**：此函数用于目标。 有关详细信息，请阅读[文档](../destinations/ui/export-arrays-maps-objects.md)。 | <ul><li>SEPARATOR： **必需**&#x200B;用于连接数组中元素的分隔符。</li><li>数组： **必需**&#x200B;要连接的数组（拼合后）。</li></ul> | array_to_string(SEPARATOR， ARRAY) | `array_to_string(";", ["Hello", "world"])` | “Hello；world” |
| [!BADGE 仅目标]{type=Informative} filterArray* | 基于谓词筛选给定数组。 **注意**：此函数用于目标。 有关详细信息，请阅读[文档](../destinations/ui/export-arrays-maps-objects.md)。 | <ul><li>数组： **必需**&#x200B;要过滤的数组</li><li>谓词： **必需**&#x200B;要应用于给定数组的每个元素的谓词。 | filterArray(ARRAY， PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5， 7] |
| [!BADGE 仅目标]{type=Informative} transformArray* | 基于谓词转换给定的数组。 **注意**：此函数用于目标。 有关详细信息，请阅读[文档](../destinations/ui/export-arrays-maps-objects.md)。 | <ul><li>数组： **必需**&#x200B;要转换的数组。</li><li>谓词： **必需**&#x200B;要应用于给定数组的每个元素的谓词。 | transformArray(ARRAY， PREDICATE) | ` transformArray([5, 6, 7], x -> x + 1)` | [6， 7， 8] |
| [!BADGE 仅目标]{type=Informative} flattenArray* | 将给定的（多维）数组平面化为一维数组。 **注意**：此函数用于目标。 有关详细信息，请阅读[文档](../destinations/ui/export-arrays-maps-objects.md)。 | <ul><li>数组： **必需**&#x200B;要平面化的数组。</li></ul> | flattenArray(ARRAY) | flattenArray([[[&#39;a&#39;， &#39;b&#39;]， [&#39;c&#39;， &#39;d&#39;]]， [[&#39;e&#39;]， [&#39;f&#39;]]]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;、&#39;f&#39;] |

{style="table-layout:auto"}

### 层次结构 — 映射 {#map}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | 此函数将对象数组和键作为输入，并返回键字段的映射，其中值为键，数组元素为值。 | <ul><li>INPUT： **必需**&#x200B;要查找的第一个非null对象的对象数组。</li><li>KEY： **必需**&#x200B;键必须是对象数组中的字段名称，并且对象必须是值。</li></ul> | array_to_map（对象[]输入，键） | 请阅读[附录](#object_to_map)中的代码示例。 |
| object_to_map | 此函数将对象作为参数并返回键值对的映射。 | <ul><li>INPUT： **必需**&#x200B;要查找的第一个非null对象的对象数组。</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address)，输入为&quot; + &quot;address： {line1 ： \&quot;345 park ave\&quot;，line2： \&quot;bldg 2\&quot;，City ： \&quot;san jose\&quot;，State ： \&quot;CA\&quot;，type： \&quot;office\&quot;}&quot; | 返回具有给定字段名称和值对的映射，如果输入为null，则返回null。 例如：`"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | 此函数接受键值对列表并返回键值对的映射。 | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;， \&quot;John\&quot;， \&quot;lastName\&quot;， \&quot;Doe\&quot;)&quot; | 返回具有给定字段名称和值对的映射，如果输入为null，则返回null。 例如：`"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### 逻辑运算符 {#logical-operators}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 解码 | 给定键值以及作为数组扁平化的键值对列表，如果找到键，此函数将返回值，如果数组中存在，则返回默认值。 | <ul><li>密钥： **必需**&#x200B;要匹配的密钥。</li><li>OPTIONS： **必需**&#x200B;键/值对的平面化数组。 或者，也可以在末尾放置默认值。</li></ul> | decode(KEY， OPTIONS) | decode(stateCode， &quot;ca&quot;， &quot;California&quot;， &quot;pa&quot;， &quot;Pennsylvania&quot;， &quot;N/A&quot;) | 如果给定的stateCode为“ca”，则为“California”。<br>如果提供的stateCode为“pa”，则为“Pennsylvania”。<br>如果stateCode与以下内容不匹配，“不适用”。 |
| iif | 计算给定的布尔表达式并根据结果返回指定的值。 | <ul><li>表达式： **必需**&#x200B;正在计算的布尔表达式。</li><li>TRUE_VALUE： **必需**&#x200B;如果表达式的计算结果为true，则返回的值。</li><li>FALSE_VALUE： **必需**&#x200B;表达式计算结果为false时返回的值。</li></ul> | iif（表达式， TRUE_VALUE， FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### 聚合 {#aggregation}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 返回给定参数的最小值。 使用自然排序。 | <ul><li>OPTIONS： **必需**&#x200B;一个或多个可以相互比较的对象。</li></ul> | min(OPTIONS) | min(3， 1， 4) | 1 |
| max | 返回给定参数的最大值。 使用自然排序。 | <ul><li>OPTIONS： **必需**&#x200B;一个或多个可以相互比较的对象。</li></ul> | max(OPTIONS) | max(3， 1， 4) | 4 |

{style="table-layout:auto"}

### 类型转换 {#type-conversions}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 将字符串转换为大整数。 | <ul><li>字符串： **必需**&#x200B;要转换为BigInteger的字符串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 将字符串转换为双精度类型。 | <ul><li>字符串： **必需**&#x200B;要转换为双精度类型的字符串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 将字符串转换为浮点数。 | <ul><li>字符串： **必需**&#x200B;要转换为浮点数的字符串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 将字符串转换为整数。 | <ul><li>字符串： **必需**&#x200B;要转换为整数的字符串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON函数 {#json}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 将给定字符串中的JSON内容反序列化。 | <ul><li>字符串： **必需**&#x200B;要反序列化的JSON字符串。</li></ul> | json_to_object&#x200B;(STRING) | `json_to_object&#x200B;({"info":{"firstName":"John","lastName": "Doe"}})` | 表示JSON的对象。 |

{style="table-layout:auto"}

### 特别操作 {#special-operations}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 生成伪随机ID。 | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | 此函数接受FPID字符串并将其转换为ECID，以便在Adobe Experience Platform和Adobe Experience Cloud应用程序中使用。 | <ul><li>字符串： **必需**&#x200B;要转换为ECID的FPID字符串。</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### 用户代理功能 {#user-agent}

下表中包含的任何用户代理函数都可以返回以下任一值：

* 电话 — 屏幕较小的移动设备（通常小于7英寸）
* 移动设备 — 尚未识别的移动设备。 此移动设备可以是电子阅读器、平板电脑、手机、手表等。

有关设备字段值的详细信息，请阅读本文档附录中的[设备字段值列表](#device-field-values)。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 从用户代理字符串中提取操作系统名称。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 从用户代理字符串中提取操作系统的主要版本。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 从用户代理字符串中提取操作系统的版本。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 从用户代理字符串中提取操作系统的名称和版本。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 从用户代理字符串中提取代理版本。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 从用户代理字符串中提取代理名称和主要版本。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 从用户代理字符串中提取代理名称。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 从用户代理字符串中提取设备类。 | <ul><li>USER_AGENT： **必需**&#x200B;用户代理字符串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 电话 |

{style="table-layout:auto"}

### Analytics函数 {#analytics}

>[!NOTE]
>
>您只能对WebSDK和Adobe Analytics流使用以下分析函数。

| 函数 | 描述 | 参数 | 句法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | 从Analytics事件字符串中提取事件ID。 | <ul><li>EVENT_STRING： **必需**&#x200B;逗号分隔的Analytics事件字符串。</li><li>EVENT_NAME： **必需**&#x200B;要从中提取的事件名称和ID。</li></ul> | aa_get_event_id(EVENT_STRING， EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456，scOpen&quot;， &quot;event101&quot;) | 123456 |
| aa_get_event_value | 从Analytics事件字符串中提取事件值。 如果未指定事件值，则返回1。 | <ul><li>EVENT_STRING： **必需**&#x200B;逗号分隔的Analytics事件字符串。</li><li>EVENT_NAME： **必需**&#x200B;要从中提取值的事件名称。</li></ul> | aa_get_event_value(EVENT_STRING， EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456，scOpen&quot;， &quot;event101&quot;) | 5 |
| aa_get_product_categories | 从Analytics产品字符串中提取产品类别。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;；Example product 1；1；3.50，Example category 2；Example product 2；1；5.99&quot;) | [null，“示例类别2”] |
| aa_get_product_names | 从Analytics产品字符串中提取产品名称。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;；Example product 1；1；3.50，Example category 2；Example product 2；1；5.99&quot;) | [“示例产品1”，“示例产品2”] |
| aa_get_product_quantities | 从Analytics产品字符串中提取数量。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li></ul> | aa_get_product_quantities(PRODUCTS_STRING) | aa_get_product_quantities（&quot;；示例产品1；1；3.50，示例类别2；示例产品2&quot;） | [&quot;1&quot;，空] |
| aa_get_product_prices | 从Analytics产品字符串中提取价格。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li></ul> | aa_get_product_prices(PRODUCTS_STRING) | aa_get_product_prices（&quot;；示例产品1；1；3.50，示例类别2；示例产品2&quot;） | [&quot;3.50&quot;，空] |
| aa_get_product_event_values | 从products字符串中提取命名事件的值作为字符串数组。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li><li>EVENT_NAME： **必需**&#x200B;要从中提取值的事件名称。</li></ul> | aa_get_product_event_values(PRODUCTS_STRING， EVENT_NAME) | aa_get_product_event_values（&quot;；示例产品1；1；4.20；event1=2.3\|event2=5:1，；示例产品2；1；4.20；event1=3\|event2=2:2&quot;， &quot;event1&quot;） | [&quot;2.3&quot;，&quot;3&quot;] |
| aa_get_product_evars | 从products字符串中抽取命名事件的evar值作为字符串数组。 | <ul><li>PRODUCTS_STRING： **必需** Analytics产品字符串。</li><li>eVar_NAME： **必需**&#x200B;要提取的eVar名称。</li></ul> | aa_get_product_evars(PRODUCTS_STRING， EVENT_NAME) | aa_get_product_evars(&quot;；示例产品；1；6.69；；eVar1=Merchandising value&quot;， &quot;eVar1&quot;) | [“促销值”] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### 对象复制 {#object-copy}

>[!TIP]
>
>当源中的对象映射到XDM中的对象时，会自动应用对象复制功能。 无需用户执行其他操作。

您可以使用对象复制功能自动复制对象的属性，而无需更改映射。 例如，如果源数据的结构为：

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

XDM结构：

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

然后，映射将变为：

```json
address -> addr
address.line1 -> addr.addrLine1
```

在上述示例中，`city`和`state`属性在运行时也会自动摄取，因为`address`对象已映射到`addr`。 如果您要在XDM结构中创建`line2`属性，并且您的输入数据在`line2`对象中还包含`address`，则它也将自动摄取，而无需手动更改映射。

要确保自动映射正常工作，必须满足以下先决条件：

* 父级对象应进行映射；
* 必须在XDM架构中创建新属性；
* 新属性在源架构和XDM架构中应有匹配的名称。

如果不满足任何先决条件，则必须使用数据准备手动将源架构映射到XDM架构。

## 附录

下面提供了有关使用数据准备映射函数的其他信息

### 特殊字符 {#special-characters}

下表概述了保留字符及其相应的编码字符。

| 保留字符 | 编码字符 |
| --- | --- |
| 空间 | %20 |
| ！ | %21 |
| ” | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| 和 | %26 |
| ’ | %27 |
| ( | %28 |
| ） | %29 |
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
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### 设备字段值 {#device-field-values}

下表概述了设备字段值及其相应说明。

| 设备 | 描述 |
| --- | --- |
| 桌面 | 台式机或笔记本电脑类型的设备。 |
| 匿名 | 匿名设备。 在某些情况下，这些是匿名化软件更改的`useragents`。 |
| 未知 | 未知设备。 这些通常是`useragents`，不包含有关设备的信息。 |
| 移动设备 | 尚未识别的移动设备。 此移动设备可以是电子阅读器、平板电脑、手机、手表等。 |
| 平板电脑 | 大屏幕（通常大于7英寸）的移动设备。 |
| 电话 | 小屏幕的移动设备（通常小于7英寸）。 |
| 观看 | 带有小屏幕（通常小于2英寸）的移动设备。 这些设备通常用作手机/平板电脑类型的设备的附加屏幕。 |
| 增强现实 | 具有AR功能的移动设备。 |
| 虚拟现实 | 一种具有VR功能的移动设备。 |
| 电子阅读器 | 类似于平板电脑的设备，但通常具有[!DNL eInk]屏幕。 |
| 机顶盒 | 允许通过电视大小的屏幕进行交互的连接设备。 |
| TV | 与机顶盒类似的设备，但内置在电视机中。 |
| 家用电器 | （通常是大型）家用电器，如冰箱。 |
| 游戏控制台 | 固定游戏系统，如[!DNL Playstation]或[!DNL XBox]。 |
| 手持游戏机 | 移动游戏系统，如[!DNL Nintendo Switch]。 |
| 语音 | 语音驱动设备，如[!DNL Amazon Alexa]或[!DNL Google Home]。 |
| 汽车 | 基于车辆的浏览器。 |
| 机器人 | 访问网站的机器人。 |
| 机器人移动设备 | 访问网站但表示希望被视为移动设备访客的机器人。 |
| 机器人模拟器 | 访问网站的机器人假装是类似[!DNL Google]的机器人，但实际上不是。 **注意**：在大多数情况下，机器人模仿者实际上是机器人。 |
| 云 | 基于云的应用程序。 它们既不是机器人，也不是黑客，而是需要连接的应用程序。 这包括[!DNL Mastodon]个服务器。 |
| 黑客 | 在`useragent`字符串中检测到脚本时使用此设备值。 |

{style="table-layout:auto"}

### 代码示例 {#code-samples}

#### map_get_values {#map-get-values}

+++选择以查看示例

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

+++选择以查看示例

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

+++选择以查看示例

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

**语法1**

+++选择以查看示例

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**语法2**

+++选择以查看示例

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**语法3**

+++选择以查看示例

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

+++选择以查看示例

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

