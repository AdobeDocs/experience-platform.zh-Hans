---
keywords: Experience Platform；主页；热门主题；map csv;map csv;map csv文件；map csv文件到xdm;map csv到xdm;ui指南；mapper;mapping字段；mapping函数；
solution: Experience Platform
title: 数据准备映射函数
topic: 概述
description: 本文档介绍了与数据准备一起使用的映射功能。
translation-type: tm+mt
source-git-commit: fd2dffd5b8957833b670e9cb434517bcb0f886a3
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 3%

---


# 数据准备映射函数

数据准备函数可用于根据在源字段中输入的内容计算和计算值。

## 字段

字段名称可以是任何合法标识符 — Unicode字母和数字的无限长序列，以字母开头、美元符号(`$`)或下划线字符(`_`)。 变量名称也区分大小写。

如果字段名称未遵循此约定，则字段名称必须用`${}`包装。 因此，例如，如果字段名称为“First Name”或“First.Name”，则名称必须分别包装为`${First Name}`或`${First.Name}`。

此外，如果字段名称为以下保留关键字的&#x200B;**任何**，则必须用`${}`封装：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

子字段内的数据可使用点记号进行访问。 例如，如果有`name`对象，则要访问`firstName`字段，请使用`name.firstName`。

## 函数列表

下表列表了所有支持的映射函数，包括示例表达式及其结果输出。

### 字符串函数

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | 连接给定字符串。 | <ul><li>字符串：将连接的字符串。</li></ul> | concat(STRING_1, STRING_2) | concat（&quot;嗨，&quot;,&quot;there&quot;, &quot;!&quot;） | `"Hi, there!"` |
| 爆炸 | 根据正则表达式拆分字符串并返回一组部分。 可以选择包含正则表达式以拆分字符串。 默认情况下，拆分解析为“，”。 以下分隔符&#x200B;**需要**&#x200B;用`\`进行转义：`+, ?, ^, |, ., [, (, {, ), *, $, \` | <ul><li>字符串：**必需**&#x200B;需要拆分的字符串。</li><li>正则表达式：*可选*&#x200B;可用于拆分字符串的常规表达式。</li></ul> | explode(STRING， REGEX) | explode（&quot;你好！&quot;, &quot; &quot;） | `["Hi,", "there"]` |
| instr | 返回子字符串的位置/索引。 | <ul><li>输入：**必需**&#x200B;正在搜索的字符串。</li><li>子字符串：**必需**&#x200B;在字符串中搜索的子字符串。</li><li>开始_POSITION:*可选*&#x200B;查找字符串中要开始的位置。</li><li>具体值：*可选*&#x200B;从开始位置查找的第n个事件。 默认情况下，它为1。 </li></ul> | instr(INPUT， SUBSTRING， 开始_POSITION， OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 替换搜索字符串（如果原始字符串中存在）。 | <ul><li>输入：**必需**&#x200B;输入字符串。</li><li>TO_FIND:**必需**&#x200B;要在输入中查找的字符串。</li><li>TO_REPLACE:**必需**&#x200B;将替换“TO_FIND”中值的字符串。</li></ul> | replacestr(INPUT， TO_FIND， TO_REPLACE) | replacestr(&quot;This is a string retest&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;这是字符串替换测试&quot; |
| substr | 返回给定长度的子字符串。 | <ul><li>输入：**必需**&#x200B;输入字符串。</li><li>开始_INDEX:**必需**&#x200B;子字符串开始的输入字符串的索引。</li><li>长度：**必需**&#x200B;子字符串的长度。</li></ul> | substr(INPUT， 开始_INDEX， LENGTH) | substr（&quot;这是子字符串测试&quot;, 7, 8） | &quot; a subst&quot; |
| lower /<br>lcase | 将字符串转换为小写。 | <ul><li>输入：**必需**&#x200B;将转换为小写的字符串。</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | “你好” |
| /<br> | 将字符串转换为大写。 | <ul><li>输入：**必需**&#x200B;将转换为大写的字符串。</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | “你好” |
| split | 在分隔符上拆分输入字符串。 以下分隔符&#x200B;**需要**&#x200B;与`\`一起转义：`\`。 | <ul><li>输入：**必需**&#x200B;要拆分的输入字符串。</li><li>分隔符：**必需**&#x200B;用于拆分输入的字符串。</li></ul> | split(INPUT， SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符连接对象的列表。 | <ul><li>分隔符：**必需**&#x200B;将用于连接对象的字符串。</li><li>对象：**必需**&#x200B;将要加入的字符串数组。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | “你好世界” |
| lpad | 将字符串的左侧与另一个给定字符串进行填充。 | <ul><li>输入：**必需**&#x200B;要填充的字符串。 此字符串可以为null。</li><li>计数：**必需**&#x200B;要填充的字符串大小。</li><li>填充：**必需**&#x200B;要用来填充输入的字符串。 如果为null或为空，则它将被视为单个空格。</li></ul> | lpad(INPUT， COUNT， PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | 将字符串的右侧与另一个给定字符串相加。 | <ul><li>输入：**必需**&#x200B;要填充的字符串。 此字符串可以为null。</li><li>计数：**必需**&#x200B;要填充的字符串大小。</li><li>填充：**必需**&#x200B;要用来填充输入的字符串。 如果为null或为空，则它将被视为单个空格。</li></ul> | rpad（输入、计数、填充） | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | “batyzyzy” |
| 左 | 获取给定字符串的第一个&quot;n&quot;字符。 | <ul><li>字符串：**必需**&#x200B;您要获得的第一个&quot;n&quot;字符的字符串。</li><li>计数：**必需**&#x200B;要从字符串获取的“n”字符。</li></ul> | left（字符串，计数） | left(&quot;abcde&quot;, 2 | &quot;ab&quot; |
| 右 | 获取给定字符串的最后一个&quot;n&quot;字符。 | <ul><li>字符串：**必需**&#x200B;要获取的最后&quot;n&quot;字符的字符串。</li><li>计数：**必需**&#x200B;要从字符串获取的“n”字符。</li></ul> | right（字符串，计数） | right(&quot;abcde&quot;, 2 | &quot;de&quot; |
| ltrim | 从字符串开头删除空格。 | <ul><li>字符串：**必需**&#x200B;要从中删除空格的字符串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | “你好” |
| rtrim | 从字符串末尾删除空格。 | <ul><li>字符串：**必需**&#x200B;要从中删除空格的字符串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | “你好” |
| trim | 从字符串的开头和结尾删除空格。 | <ul><li>字符串：**必需**&#x200B;要从中删除空格的字符串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | “你好” |
| 等于 | 比较两个字符串以确认它们是否相等。 此函数区分大小写。 | <ul><li>STRING1:**必需**&#x200B;要比较的第一个字符串。</li><li>STRING2:**必需**&#x200B;要比较的第二个字符串。</li></ul> | STRING1 &#x200B;equals(&#x200B; STRING2) | &quot;string1&quot; &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比较两个字符串以确认它们是否相等。 此函数&#x200B;**不**&#x200B;区分大小写。 | <ul><li>STRING1:**必需**&#x200B;要比较的第一个字符串。</li><li>STRING2:**必需**&#x200B;要比较的第二个字符串。</li></ul> | STRING1 &#x200B;equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot; &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

&#x200B;

### 正则表达式函数

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | 基于正则表达式从输入字符串提取组。 | <ul><li>字符串：**必需**&#x200B;要从中提取组的字符串。</li><li>正则表达式：**必需**&#x200B;您希望组匹配的正则表达式。</li></ul> | extract_regex(STRING， REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;、&quot;E259&quot;、&quot;1_1&quot;] |
| matches_regex | 检查字符串是否与输入的正则表达式匹配。 | <ul><li>字符串：**必需**&#x200B;要检查的字符串与正则表达式匹配。</li><li>正则表达式：**必需**&#x200B;要比较的正则表达式。</li></ul> | matches_regex(STRING， REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

### 散列函数

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | 使用安全哈希算法1(SHA-1)获取输入并生成哈希值。 | <ul><li>输入：**必需**&#x200B;要散列的纯文本。</li><li>CHARSET:*可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT， CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B;48690840c5dfcce3c80 |
| sha256 | 使用安全哈希算法256(SHA-256)获取输入并生成哈希值。 | <ul><li>输入：**必需**&#x200B;要散列的纯文本。</li><li>CHARSET:*可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256(INPUT， CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 使用安全哈希算法512(SHA-512)获取输入并生成哈希值。 | <ul><li>输入：**必需**&#x200B;要散列的纯文本。</li><li>CHARSET:*可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512(INPUT， CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd078a89 &#x200B;a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | 使用MD5进行输入并生成哈希值。 | <ul><li>输入：**必需**&#x200B;要散列的纯文本。</li><li>CHARSET:*可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5(INPUT， CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B;e9bd0198d03ba6852c7 |
| crc32 | 输入使用循环冗余校验(CRC)算法来生成32位循环码。 | <ul><li>输入：**必需**&#x200B;要散列的纯文本。</li><li>CHARSET:*可选*&#x200B;字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT， CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL函数

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | 从给定URL返回协议。 如果输入无效，则返回null。 | <ul><li>URL:**必需**&#x200B;需要从中提取协议的URL。</li></ul> | get_url_&#x200B;protocol(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 返回给定URL的主机。 如果输入无效，则返回null。 | <ul><li>URL:**必需**&#x200B;需要从中提取主机的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 返回给定URL的端口。 如果输入无效，则返回null。 | <ul><li>URL:**必需**&#x200B;需要从中提取端口的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 返回给定URL的路径。 默认情况下，返回完整路径。 | <ul><li>URL:**必需**&#x200B;需要从中提取路径的URL。</li><li>FULL_PATH:*可选*&#x200B;一个布尔值，它确定是否返回完整路径。 如果设置为false，则只返回路径的结尾。</li></ul> | get_url_&#x200B;path(URL， FULL_PATH) | get_url_&#x200B;path(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_查询_str | 返回给定URL的查询字符串。 | <ul><li>URL:**必需**&#x200B;您尝试从中获取查询字符串的URL。</li><li>锚点：**必需**&#x200B;确定将使用查询字符串中的锚记执行哪些操作。 可以是以下三个值之一：&quot;retain&quot;、&quot;remove&quot;或&quot;append&quot;。<br><br>如果值为&quot;retain&quot;，则锚点将附加到返回的值。<br>如果值为&quot;remove&quot;，则从返回值中删除锚点。<br>如果值为&quot;append&quot;，则锚点将作为单独的值返回。</li></ul> | get_url_query_str&#x200B;(URL， ANCHOR) | get_url_query_&#x200B;str(&#x200B;&quot;foo://example.com:8042/over/there?name &#x200B;8 ferret#nose&quot;, &quot;retain&quot;)<br>get_query_str&#x200B;(&quot;foo://example.com:8042_over/there?name &#x200B;=ferret#nose&quot;, &quot;remove&quot;)<br>get_url(foo://example.com_url)#nose”、“append”) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### 日期和时间函数

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。 有关`date`函数的详细信息，请参阅[日期函数指南](./dates.md)。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | 检索当前时间。 |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 检索当前Unix时间。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根据指定的格式设置输入日期的格式。 | <ul><li>日期：**必需**&#x200B;要设置格式的输入日期（作为ZonedDateTime对象）。</li><li>格式：**必需**&#x200B;您希望日期更改为的格式。</li></ul> | format(DATE， FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | “2019-10-23 11:24:35” |
| dformat | 根据指定的格式将时间戳转换为日期字符串。 | <ul><li>时间戳：**必需**&#x200B;要设置格式的时间戳。 以毫秒为单位写入。</li><li>格式：**必需**&#x200B;您希望将时间戳更改为的格式。</li></ul> | dformat&#x200B;(TIMESTAMP， FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | 《2019年10月23日11:24》 |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期：**必需**&#x200B;表示日期的字符串。</li><li>格式：**必需**&#x200B;表示日期格式的字符串。</li><li>DEFAULT_DATE:**必需**&#x200B;如果提供的日期为null，则返回默认日期。</li></ul> | date(DATE， FORMAT， DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | “2019-10-23T11:24Z” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期：**必需**&#x200B;表示日期的字符串。</li><li>格式：**必需**&#x200B;表示日期格式的字符串。</li></ul> | date(DATE， FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | “2019-10-23T11:24Z” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期：**必需**&#x200B;表示日期的字符串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | “2019-10-23T11:24Z” |
| date_part | 检索日期的部分。 支持以下组件值：<br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;a29/>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br> | <ul><li>组件：**必需**&#x200B;表示日期部分的字符串。 </li><li>日期：**必需**&#x200B;日期，采用标准格式。</li></ul> | date_part&#x200B;(COMPONENT， DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 在给定日期替换组件。 接受以下组件：<br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hhh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>组件：**必需**&#x200B;表示日期部分的字符串。 </li><li>值：**必需**&#x200B;为给定日期的组件设置的值。</li><li>日期：**必需**&#x200B;日期，采用标准格式。</li></ul> | set_date_part(&#x200B;COMPONENT， VALUE， DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | “2016-04-09T11:44:44.797” |
| make_date_time | 从部分创建日期。 此函数也可以使用make_timestamp来引导。 | <ul><li>年：**必需**&#x200B;年份，以四位数字写入。</li><li>月：**必需**&#x200B;月。 允许的值为1到12。</li><li>日：**必需**&#x200B;天。 允许的值为1到31。</li><li>小时：**必需**&#x200B;小时。 允许的值为0到23。</li><li>分钟：**必需**&#x200B;分钟。 允许的值为0到59。</li><li>纳秒：**必需**&#x200B;纳秒值。 允许的值为0到999999999。</li><li>时区：**必需**&#x200B;日期时间的时区。</li></ul> | make_date_time(&#x200B;YEAR、MONTH、DAY、HOUR、MINUTE、SECOND、纳秒、时区) | make_date_time(&#x200B;2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 将任何时区中的日期转换为UTC中的日期。 | <ul><li>日期：**必需**&#x200B;您尝试转换的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 将日期从一个时区转换为另一个时区。 | <ul><li>日期：**必需**&#x200B;您尝试转换的日期。</li><li>区域：**必需**&#x200B;您尝试将日期转换为的时区。</li></ul> | zone_date_to_zone(&#x200B;DATE， ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### 层次结构 — 对象

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | 返回输入的大小。 | <ul><li>输入：**必需**&#x200B;您尝试查找大小的对象。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 检查对象是否为空。 | <ul><li>输入：**必需**&#x200B;您尝试检查的对象为空。</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | 假 |
| arrays_to_object | 创建对象列表。 | <ul><li>输入：**必需**&#x200B;键和数组对的分组。</li></ul> | arrays_to_object(INPUT) | 需要样本 | 需要样本 |
| to_object | 基于给定的平面键/值对创建对象。 | <ul><li>输入：**必需**&#x200B;键/值对的简单列表。</li></ul> | to_object(INPUT) | to_object(&#x200B;&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 从输入字符串创建对象。 | <ul><li>字符串：**必需**&#x200B;正在分析以创建对象的字符串。</li><li>VALUE_DELIMITER:*可选*&#x200B;分隔字段与值的分隔符。 默认分隔符为`:`。</li><li>FIELD_DELIMITER:*可选*&#x200B;分隔字段值对的分隔符。 默认分隔符为`,`。</li></ul> | str_to_object(&#x200B;STRING， VALUE_DELIMITER， FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | 电话 — 123 456 7890&quot;, &quot;-&quot;, &quot; | “) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 检查源数据中是否存在该对象。 | <ul><li>输入：**必需**&#x200B;要检查的路径（如果它存在于源数据中）。</li></ul> | is_set(INPUT) | is_set&#x200B;(&quot;evars.evar.field1&quot;) | true |
| 无效 | 将属性的值设置为`null`。 当您不想将字段复制到目标架构时，应使用此选项。 |  | nullify() | nullify() | `null` |

### 层次结构 — 数组

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| 合并 | 返回给定数组中的第一个非null对象。 | <ul><li>输入：**必需**&#x200B;要查找的第一个非null对象的数组。</li></ul> | coalesce(INPUT) | coalesce(null、null、null、null、&quot;first&quot;、null、&quot;second&quot;) | &quot;first&quot; |
| 第 | 检索给定数组的第一个元素。 | <ul><li>输入：**必需**&#x200B;要查找的第一个元素的数组。</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 最后 | 检索给定数组的最后一个元素。 | <ul><li>输入：**必需**&#x200B;要查找的最后一个元素的数组。</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | 获取输入列表并将其转换为数组。 | <ul><li>INCLUDE_NULLS:**必需**&#x200B;一个布尔值，指示是否在响应数组中包含空值。</li><li>值：**必需**&#x200B;要转换为数组的元素。</li></ul> | to_array(&#x200B;INCLUDE_NULLS， VALUES) | to_array(false， 1, null， 2, 3) | `[1, 2, 3]` |

### 逻辑运算符

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| 解码 | 如果给定一个键和作为数组拼合的键值对列表，则如果找到键，该函数将返回该值，如果数组中存在，则返回默认值。 | <ul><li>键：**必需**&#x200B;要匹配的键。</li><li>OPTIONS:**必需**&#x200B;键/值对的拼合数组。 （可选）可以将默认值放在末尾。</li></ul> | decode(KEY，OPTIONS) | decode(stateCode， &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 如果给定的stateCode为&quot;ca&quot;, &quot;California&quot;。<br>如果给定的stateCode为&quot;pa&quot;，则为&quot;Pennsylvania&quot;。<br>如果stateCode与以下代码不匹配，则为“N/A”。 |
| i | 计算给定的布尔表达式，并根据结果返回指定值。 | <ul><li>表达式：**必需**&#x200B;要计算的布尔表达式。</li><li>TRUE_VALUE:**必需**&#x200B;如果表达式的计算结果为true，则返回的值。</li><li>FALSE_VALUE:**必需**&#x200B;如果表达式的计算结果为false，则返回的值。</li></ul> | iif(EXPRESSION， TRUE_VALUE， FALSE_VALUE) | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### 聚合

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | 返回给定参数的最小值。 使用自然排序。 | <ul><li>OPTIONS:**必需**&#x200B;一个或多个可以相互比较的对象。</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 返回给定参数的最大值。 使用自然排序。 | <ul><li>OPTIONS:**必需**&#x200B;一个或多个可以相互比较的对象。</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### 类型转换

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | 将字符串转换为BigInteger。 | <ul><li>字符串：**必需**&#x200B;要转换为BigInteger的字符串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 将字符串转换为Double。 | <ul><li>字符串：**必需**&#x200B;要转换为Double的字符串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 将字符串转换为Float。 | <ul><li>字符串：**必需**&#x200B;要转换为Float的字符串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 将字符串转换为Integer。 | <ul><li>字符串：**必需**&#x200B;要转换为整数的字符串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON函数

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | 反序列化给定字符串中的JSON内容。 | <ul><li>字符串：**必需**&#x200B;要反序列化的JSON字符串。</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;:&quot;Doe&quot;}}) | 表示JSON的对象。 |

### 特别行动

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br> guid | 生成伪随机ID。 |  | uuid()<br>guid( | uuid()<br>guid( | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### 用户代理函数

>[!NOTE]
>
>请向左/向右滚动以查看表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | 从用户代理字符串提取操作系统名称。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 从用户代理字符串提取操作系统的主版本。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B;s(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 从用户代理字符串提取操作系统的版本。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 从用户代理字符串提取操作系统的名称和版本。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 从用户代理字符串提取代理版本。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 从用户代理字符串提取代理名称和主版本。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 从用户代理字符串提取代理名称。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 从用户代理字符串提取设备类。 | <ul><li>USER_AGENT:**必需**&#x200B;用户代理字符串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class(&#x200B;&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Phone |