---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: 数据准备功能
topic: overview
description: 本文档介绍了与数据准备一起使用的映射功能。
translation-type: tm+mt
source-git-commit: 6deb8f5e11b87550601679f06c8445d90fd22709
workflow-type: tm+mt
source-wordcount: '3459'
ht-degree: 3%

---


# 数据准备功能

数据准备函数可用于根据在源字段中输入的内容计算和计算值。

## 字段

字段名称可以是任何合法标识符- Unicode字母和数字的无限长度序列，以字母、美元符号()`$`或下划线字符(`_`)开头。 变量名称也区分大小写。

如果字段名称不符合此约定，则字段名称必须用封面 `${}`。 因此，例如，如果字段名称为“名字”或“名字”，则名称必须分别包装为“名字” `${First Name}` 或“ `${First.Name}` 名字”。

此外，字段名 **是以** 下任何保留关键字，必须用以下方式包装 `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

子字段内的数据可以使用点记号来访问。 例如，如果有对 `name` 象，则要访问该 `firstName` 字段，请使用 `name.firstName`。

## 函数列表

下表列表了所有支持的映射函数，包括示例表达式及其结果输出。

### 字符串函数

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | 连接给定字符串。 | <ul><li>字符串：将连接的字符串。</li></ul> | concat(STRING_1, STRING_2) | concat（&quot;嗨， &quot;, &quot;there&quot;, &quot;!&quot;） | `"Hi, there!"` |
| 爆炸 | 根据正则表达式拆分字符串并返回一组部分。 可以选择包含正则表达式以拆分字符串。 默认情况下，拆分解析为“,”。 | <ul><li>字符串： **必需** 。需要拆分的字符串。</li><li>正则表达式： *可选* ：可用于拆分字符串的常规表达式。</li></ul> | explode(STRING, REGEX) | explode（&quot;嗨，那儿！&quot;, &quot; &quot;） | `["Hi,", "there"]` |
| instr | 返回子字符串的位置／索引。 | <ul><li>输入： **必需** 。正在搜索的字符串。</li><li>子字符串： **必需** 。在字符串中搜索的子字符串。</li><li>开始位置： *可选* 。开始查看字符串的位置。</li><li>具体值： *可选* ，从开始位置查找第n个匹配项。 默认情况下，它为1。 </li></ul> | instr(INPUT, SUBSTRING,开始位置，发生) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 替换搜索字符串（如果存在于原始字符串中）。 | <ul><li>输入： **必需** 。输入字符串。</li><li>TO_FIND: **必需** 。要在输入中查找的字符串。</li><li>TO_REPLACE: **必需** 。将替换“TO_FIND”中值的字符串。</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replaceestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;这是字符串替换测试&quot; |
| substr | 返回给定长度的子字符串。 | <ul><li>输入： **必需** 。输入字符串。</li><li>开始索引： **必需** ：输入字符串的索引，其中子字符串开始。</li><li>LENGTH: **Required** The length of the substring.</li></ul> | substr(INPUT,开始索引，长度) | substr（&quot;这是子字符串测试&quot;, 7, 8） | &quot; a subst&quot; |
| lower /<br>lcase | 将字符串转换为小写。 | <ul><li>输入： **必需** 。将转换为小写的字符串。</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | “hello” |
| 上/<br>下 | 将字符串转换为大写。 | <ul><li>输入： **必需** 。将转换为大写的字符串。</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | “您好” |
| 拆分 | 在分隔符上拆分输入字符串。 | <ul><li>输入： **必需** 。将要拆分的输入字符串。</li><li>分隔符： **必需** 。用于拆分输入的字符串。</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符连接对象列表。 | <ul><li>分隔符： **必需** 。将用于连接对象的字符串。</li><li>对象： **必需** 。将加入的字符串数组。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | “你好世界” |
| lpad | 将字符串的左侧与另一个给定字符串进行填充。 | <ul><li>输入： **必需** 。要填充的字符串。 此字符串可以为null。</li><li>计数： **必需** 。要填充的字符串大小。</li><li>填充： **必需** 。用于输入的字符串。 如果为null或为空，则它将被视为单个空格。</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | “yzyzybat” |
| rpad | 将字符串的右侧与另一个给定的字符串相连。 | <ul><li>输入： **必需** 。要填充的字符串。 此字符串可以为null。</li><li>计数： **必需** 。要填充的字符串大小。</li><li>填充： **必需** 。用于输入的字符串。 如果为null或为空，则它将被视为单个空格。</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | “batyzyzy” |
| 左 | 获取给定字符串的第一个“n”字符。 | <ul><li>字符串： **必需** 。您要获得的第一个“n”字符的字符串。</li><li>计数： **必**&#x200B;需要从字符串获取的“n”字符。</li></ul> | left（字符串，计数） | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| 右 | 获取给定字符串的最后一个“n”字符。 | <ul><li>字符串： **必需** 。您要获得的最后一个“n”字符的字符串。</li><li>计数： **必**&#x200B;需要从字符串获取的“n”字符。</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2 | “de” |
| ltrim | 从字符串的开头删除空格。 | <ul><li>字符串： **必需** 。要从中删除空格的字符串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | “hello” |
| 修剪 | 从字符串的末尾删除空格。 | <ul><li>字符串： **必需** 。要从中删除空格的字符串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | “hello” |
| trim | 从字符串的开头和结尾删除空格。 | <ul><li>字符串： **必需** 。要从中删除空格的字符串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | “hello” |
| 等于 | 比较两个字符串以确认它们是否相等。 此函数区分大小写。 | <ul><li>STRING1: **必需** 。要比较的第一个字符串。</li><li>STRING2: **必需** 。要比较的第二个字符串。</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;。equals(&quot;STRING1) | false |
| equalsIgnoreCase | 比较两个字符串以确认它们是否相等。 此函数不 **区分大小写** 。 | <ul><li>STRING1: **必需** 。要比较的第一个字符串。</li><li>STRING2: **必需** 。要比较的第二个字符串。</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;。equalsIgnoreCase(&quot;STRING1) | true |

### 散列函数

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | 使用安全哈希算法1(SHA-1)输入并生成哈希值。 | <ul><li>输入： **必需** 。要散列的纯文本。</li><li>字符集： *可选* 。字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1(INPUT, CHARSET) | sha1（&quot;我的文本&quot;, &quot;UTF-8&quot;） | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | 使用安全哈希算法256(SHA-256)输入并生成哈希值。 | <ul><li>输入： **必需** 。要散列的纯文本。</li><li>字符集： *可选* 。字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256(INPUT, CHARSET) | sha256（&quot;我的文本&quot;, &quot;UTF-8&quot;） | 7330d2b39ca35eaf4cb95fc846c21 &#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 使用安全哈希算法512(SHA-512)输入并生成哈希值。 | <ul><li>输入： **必需** 。要散列的纯文本。</li><li>字符集： *可选* 。字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512(INPUT, CHARSET) | sha512（&quot;我的文本&quot;, &quot;UTF-8&quot;） | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B;708bf11b4232b21d2a8704ada2cd7b367dd0788a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | 使用MD5输入并生成哈希值。 | <ul><li>输入： **必需** 。要散列的纯文本。</li><li>字符集： *可选* 。字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B;e9bd0198d03ba6852c7 |
| crc32 | 输入使用循环冗余校验(CRC)算法来生成32位循环码。 | <ul><li>输入： **必需** 。要散列的纯文本。</li><li>字符集： *可选* 。字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL函数

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | 从给定URL返回协议。 如果输入无效，则返回null。 | <ul><li>URL: **必需** 。需要从中提取协议的URL。</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | 返回给定URL的主机。 如果输入无效，则返回null。 | <ul><li>URL: **必需** 。需要从中提取主机的URL。</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 返回给定URL的端口。 如果输入无效，则返回null。 | <ul><li>URL: **必需** 。需要从中提取端口的URL。</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | 返回给定URL的路径。 默认情况下，返回完整路径。 | <ul><li>URL: **必需** 。需要从中提取路径的URL。</li><li>FULL_PATH: *可选* ：一个布尔值，它确定是否返回完整路径。 如果设置为false，则只返回路径的结尾。</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_查询_str | 返回给定URL的查询字符串。 | <ul><li>URL: **必需** 。您尝试从中获取查询字符串的URL。</li><li>锚点： **必需** ：确定将对查询字符串中的锚点执行什么操作。 可以是以下三个值之一：“retain”、“remove”或“append”。<br><br>如果值为“retain”，则锚点将附加到返回的值。<br>如果值为“remove”，则锚点将从返回的值中删除。<br>如果值为“append”，则锚点将作为单独的值返回。</li></ul> | get_url_查询_str(URL, ANCHOR) | get_url_查询_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;retain&quot;)<br>get_url_查询_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_查询_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### 日期和时间函数

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | 检索当前时间。 |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 检索当前Unix时间。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根据指定的格式设置输入日期的格式。 | <ul><li>日期： **必需** ：输入日期（作为ZonedDateTime对象），您要设置格式。</li><li>格式： **必需** 。您希望将日期更改为的格式。</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 根据指定的格式将时间戳转换为日期字符串。 | <ul><li>时间戳： **必需** 。要设置格式的时间戳。 写入时间为毫秒。</li><li>格式： **必需** 。您希望将时间戳更改为的格式。</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | “2019年10月23日11:24” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 。表示日期的字符串。</li><li>格式： **必需** 。表示日期格式的字符串。</li><li>DEFAULT_DATE: **必需** ：如果提供的日期为null，则返回默认日期。</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | “2019-10-23T11:24Z” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 。表示日期的字符串。</li><li>格式： **必需** 。表示日期格式的字符串。</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | “2019-10-23T11:24Z” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 。表示日期的字符串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | “2019-10-23T11:24Z” |
| date_part | 检索日期的部分。 支持以下组件值： <br><br><br>“年<br>”<br><br>“yy<br>”第4季度<br>“<br><br><br><br>”<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>“q”、“q”、“”、“ead”。“ 12”“mi”“n”“第二”“毫秒””。 | <ul><li>组件： **必需** A string，表示日期的一部分。 </li><li>日期： **必需** ，采用标准格式的日期。</li></ul> | date_part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 在给定日期替换组件。 接受以下组件： <br><br>&quot;年&quot;<br>&quot;<br>yy&quot;月<br><br>&quot;<br>&quot;<br>mm&quot;<br><br>&quot;<br>m&quot; dd&quot;日<br>&quot;<br><br>&quot;<br>&quot;小时&quot;<br><br><br><br><br><br><br><br>&quot;分钟&quot;&quot;mi&quot;mi&quot;n&quot;&quot;第二&quot;&quot; | <ul><li>组件： **必需** A string，表示日期的一部分。 </li><li>值： **必需** 。为组件设置的给定日期值。</li><li>日期： **必需** ，采用标准格式的日期。</li></ul> | set_date_part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | 从部分创建日期。 此函数也可以使用make_timestamp来诱导。 | <ul><li>年： **必需** ，年份，以四位数写成。</li><li>月： **月** 。 允许的值为1到12。</li><li>日： **必需** 。 允许的值为1到31。</li><li>小时： **必需** ，小时。 允许的值为0到23。</li><li>分钟： **必需** ，分钟。 允许的值为0到59。</li><li>纳秒： **必需** ，纳秒值。 允许的值为0到999999999。</li><li>时区： **必需** 。日期时间的时区。</li></ul> | make_date_time（YEAR, MONTH, DAY, HOUR, MINUTE, SECOND，纳秒， TIMEZONE） | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 将任意时区中的日期转换为UTC中的日期。 | <ul><li>日期： **必需** 。您尝试转换的日期。</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 将日期从一个时区转换为另一个时区。 | <ul><li>日期： **必需** 。您尝试转换的日期。</li><li>区域： **必需** 。您尝试将日期转换为的时区。</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### 层次——对象

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | 返回输入的大小。 | <ul><li>输入： **必需** 。您尝试查找的对象大小。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 检查对象是否为空。 | <ul><li>输入： **必需** 。您尝试检查的对象为空。</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | 创建对象列表。 | <ul><li>输入： **必需** 。键对和数组对的分组。</li></ul> | arrays_to_object(INPUT) | 需求示例 | 需求示例 |
| to_object | 根据给定的平键／值对创建对象。 | <ul><li>输入： **必需** ：键／值对的平面列表。</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 从输入字符串创建对象。 | <ul><li>字符串： **必需** 。正在分析以创建对象的字符串。</li><li>VALUE_DELIMITER: *可选* 。分隔字段与值的分隔符。 The default delimiter is `:`.</li><li>FIELD_DELIMITER: *可选* 。分隔字段值对的分隔符。 The default delimiter is `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | 电话- 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 检查源数据中是否存在该对象。 | <ul><li>输入： **必需** ：如果源数据中存在要检查的路径。</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | true |
| 取消 | 将属性的值设置为 `null`。 当您不希望将字段复制到目标模式时，应使用此字段。 |  | nullify() | nullify() | `null` |

### 层次结构——数组

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| 凝聚 | 返回给定数组中的第一个非空对象。 | <ul><li>输入： **必需** 。要查找的第一个非空对象的数组。</li></ul> | coalesce(INPUT) | coalesce(null、null、null、“first”、null、“second”) | “first” |
| 第 | 检索给定数组的第一个元素。 | <ul><li>输入： **必需** 。要查找的第一个元素的数组。</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 最后 | 检索给定数组的最后一个元素。 | <ul><li>输入： **必需** 。要查找的最后一个元素的数组。</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | 获取一列表输入并将其转换为数组。 | <ul><li>INCLUDE_NULLS: **必需** ：一个布尔值，用于指示是否在响应数组中包含空值。</li><li>值： **必需** 。要转换为数组的元素。</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### 逻辑运算符

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| 解码 | 如果将键和键值对列表拼合为数组，则函数返回值（如果找到键），或返回默认值（如果数组中存在）。 | <ul><li>密钥： **必需** 。要匹配的密钥。</li><li>OPTIONS: **必需** ：键／值对的拼合数组。 （可选）可以将默认值放在结尾。</li></ul> | decode(KEY,OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennysplania&quot;, &quot;N/A&quot;) | 如果给定的stateCode是“ca”、“California”。<br>如果给定的stateCode是“pa”、“Pennysvania”。<br>如果stateCode与以下内容不匹配，则为“N/A”。 |
| ii | 计算给定的布尔表达式，并根据结果返回指定值。 | <ul><li>BOOLEAN_表达式: **必需** ：要计算的布尔表达式。</li><li>TRUE_VALUE: **必需** ：当表达式的计算结果为true时返回的值。</li><li>FALSE_VALUE: **必需** ：当表达式的计算结果为false时返回的值。</li></ul> | iif(BOOLEAN_表达式、TRUE_VALUE、FALSE_VALUE) | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### 聚合

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | 返回给定参数的最小值。 使用自然订购。 | <ul><li>OPTIONS: **必需** ：可相互比较的一个或多个对象。</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 返回给定参数的最大值。 使用自然订购。 | <ul><li>OPTIONS: **必需** ：可相互比较的一个或多个对象。</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### 类型转换

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | 将字符串转换为BigInteger。 | <ul><li>字符串： **必需** 。要转换为BigInteger的字符串。</li></ul> | to_bigint(STRING) | to_bigint(&quot;100000.34&quot;) | 1000000.34 |
| to_decimal | 将字符串转换为多次。 | <ul><li>字符串： **必需** 要转换为多次的字符串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 将字符串转换为浮点。 | <ul><li>字符串： **必需** 要转换为浮点的字符串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 将字符串转换为整数。 | <ul><li>字符串： **必需** 。要转换为整数的字符串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON函数

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | 反序列化给定字符串中的JSON内容。 | <ul><li>字符串： **需要** ,JSON字符串需要反序列化。</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;:&quot;Doe&quot;}) | 表示JSON的对象。 |

### 特别行动

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | 生成伪随机ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### 用户代理功能

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | 从用户代理字符串中提取操作系统名称。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | iOS |
| ua_os_version_major | 从用户代理字符串中提取操作系统的主要版本。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | iOS 5 |
| ua_os_version | 从用户代理字符串提取操作系统的版本。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | 5.1.1 |
| ua_os_name_version | 从用户代理字符串提取操作系统的名称和版本。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | iOS 5.1.1 |
| ua_agent_version | 从用户代理字符串提取代理版本。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | 5.1 |
| ua_agent_version_major | 从用户代理字符串中提取代理名称和主要版本。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | Safari 5 |
| ua_agent_name | 从用户代理字符串提取代理名称。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | Safari |
| ua_device_class | 从用户代理字符串提取设备类。 | <ul><li>USER_AGENT: **必需** ：用户代理字符串。</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1（如Mac OS X）AppleWebKit/534.46（KHTML，如Gecko）Version/5.1 Mobile/9B206 Safari/7534.48.3英寸) | Phone |