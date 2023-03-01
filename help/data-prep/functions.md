---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；ui指南；映射器；映射；映射字段；映射函数；
solution: Experience Platform
title: 数据准备映射函数
description: 本文档介绍了与数据准备一起使用的映射函数。
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 2584e804674cc54f9cdd0b3a28ee6fb1600b6216
workflow-type: tm+mt
source-wordcount: '4392'
ht-degree: 3%

---

# 数据准备映射函数

数据准备函数可用于根据在源字段中输入的内容计算和计算值。

## 字段

字段名称可以是任何合法标识符 — 由Unicode字母和数字组成的无限长序列，以字母、美元符号(`$`)或下划线字符(`_`)。 变量名称也区分大小写。

如果字段名称不遵循此约定，则字段名称必须用换行 `${}`. 因此，例如，如果字段名称是“First Name”或“First.Name”，则必须像这样换行 `${First Name}` 或 `${First\.Name}` 的量度。

>[!TIP]
>
>与层次结构交互时，如果子属性具有句点(`.`)，则必须使用反斜杠(`\`)以转义特殊字符。 有关详细信息，请阅读以下指南： [转义特殊字符](home.md#escape-special-characters).

此外，如果字段名称为 **任意** 保留关键字中，必须使用 `${}`：

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

可以使用点表示法访问子字段中的数据。 例如，如果有 `name` 对象，以访问 `firstName` 字段，使用 `name.firstName`.

## 函数列表

下表列出了所有受支持的映射函数，包括示例表达式及其生成的输出。

### 字符串函数 {#string}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 连接给定的字符串。 | <ul><li>STRING：将连接的字符串。</li></ul> | concat(STRING_1， STRING_2) | concat(&quot;Hi， &quot;， &quot;there&quot;， &quot;！&quot;) | `"Hi, there!"` |
| 爆炸 | 根据正则表达式拆分字符串并返回部分数组。 可以选择包含正则表达式以拆分字符串。 默认情况下，拆分解析为“，”。 以下分隔符 **需要** 逃跑的 `\`： `+, ?, ^, \|, ., [, (, {, ), *, $, \` 如果包含多个字符作为分隔符，则分隔符将被视为多字符分隔符。 | <ul><li>字符串： **必需** 需要拆分的字符串。</li><li>正则表达式： *可选* 可用于拆分字符串的正则表达式。</li></ul> | explode(STRING， REGEX) | explode(&quot;Hi， there！&quot;， &quot;) | `["Hi,", "there"]` |
| 实例 | 返回子字符串的位置/索引。 | <ul><li>输入： **必需** 正在搜索的字符串。</li><li>子字符串： **必需** 在字符串中搜索的子字符串。</li><li>起始位置： *可选* 字符串中开始查找的位置。</li><li>发生次数： *可选* 从起始位置查找的第n个匹配项。 默认情况下，该值为1。 </li></ul> | instr(INPUT， SUBSTRING， START_POSITION， OCCURRENCE) | instr(“adobe.com”，“com”) | 6 |
| 替换器 | 替换搜索字符串（如果存在于原始字符串中）。 | <ul><li>输入： **必需** 输入字符串。</li><li>TO_FIND： **必需** 在输入中查找的字符串。</li><li>TO_REPLACE： **必需** 将替换“TO_FIND”中的值的字符串。</li></ul> | replacestr(INPUT， TO_FIND， TO_REPLACE) | replacestr(&quot;This is a string re test&quot;， &quot;re&quot;， &quot;replace&quot;) | “这是一个字符串替换测试” |
| substr | 返回给定长度的子字符串。 | <ul><li>输入： **必需** 输入字符串。</li><li>START_INDEX： **必需** 子字符串开始处的输入字符串的索引。</li><li>长度： **必需** 子字符串的长度。</li></ul> | substr(INPUT， START_INDEX， LENGTH) | substr（“这是一个子字符串测试”，7、8） | &quot;a subst&quot; |
| lower /<br>lcase | 将字符串转换为小写。 | <ul><li>输入： **必需** 将转换为小写的字符串。</li></ul> | lower(INPUT) | lower(“HeLo”)<br>lcase(“HeLlO”) | &quot;hello&quot; |
| upper /<br>ucase | 将字符串转换为大写。 | <ul><li>输入： **必需** 将转换为大写的字符串。</li></ul> | upper(INPUT) | upper(“HeLo”)<br>Ucase(“HeLlO”) | &quot;HELLO&quot; |
| split | 在分隔符上拆分输入字符串。 以下分隔符 **需要** 逃跑的 `\`： `\`. 如果您包含多个分隔符，则字符串将被拆分 **任意** 字符串中存在的分隔符的数量。 | <ul><li>输入： **必需** 将要拆分的输入字符串。</li><li>分隔符： **必需** 用于拆分输入的字符串。</li></ul> | split（输入，分隔符） | split(“Hello world”、“ ”) | `["Hello", "world"]` |
| 加入 | 使用分隔符连接对象列表。 | <ul><li>分隔符： **必需** 用于连接对象的字符串。</li><li>对象： **必需** 将连接的字符串数组。</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | “Hello world” |
| lpad | 将字符串的左侧与另一个给定的字符串填充。 | <ul><li>输入： **必需** 将要填充的字符串。 此字符串可以为null。</li><li>计数： **必需** 要填充的字符串的大小。</li><li>内边距： **必需** 用于填充输入的字符串。 如果为null或为空，则将被视为单个空格。</li></ul> | lpad（输入、计数、填充） | lpad(“bat”， 8， “yz”) | &quot;yzybat&quot; |
| rpad | 将字符串的右边与另一个给定的字符串进行填充。 | <ul><li>输入： **必需** 将要填充的字符串。 此字符串可以为null。</li><li>计数： **必需** 要填充的字符串的大小。</li><li>内边距： **必需** 用于填充输入的字符串。 如果为null或为空，则将被视为单个空格。</li></ul> | rpad（输入、计数、填充） | rpad(“bat”， 8， “yz”) | “batyzyzy” |
| left | 获取给定字符串的前“n”个字符。 | <ul><li>字符串： **必需** 要为其获取前“n”个字符的字符串。</li><li>计数： **必需**&#x200B;您希望从字符串中获取的“n”字符。</li></ul> | left(STRING， COUNT) | left(&quot;abcde&quot;， 2) | &quot;ab&quot; |
| 右 | 获取给定字符串的最后“n”个字符。 | <ul><li>字符串： **必需** 要为其获取最后“n”个字符的字符串。</li><li>计数： **必需**&#x200B;您希望从字符串中获取的“n”字符。</li></ul> | right(STRING， COUNT) | right(&quot;abcde&quot;， 2) | &quot;de&quot; |
| ltrim | 删除字符串开头的空格。 | <ul><li>字符串： **必需** 要删除空白的字符串。</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 删除字符串末尾的空格。 | <ul><li>字符串： **必需** 要删除空白的字符串。</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | 删除字符串开头和结尾的空格。 | <ul><li>字符串： **必需** 要删除空白的字符串。</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 等于 | 比较两个字符串以确认它们是否相等。 此函数区分大小写。 | <ul><li>STRING1： **必需** 要比较的第一个字符串。</li><li>字符串2： **必需** 要比较的第二个字符串。</li></ul> | STRING1. &#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;。 &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 比较两个字符串以确认它们是否相等。 此函数为 **非** 区分大小写。 | <ul><li>STRING1： **必需** 要比较的第一个字符串。</li><li>字符串2： **必需** 要比较的第二个字符串。</li></ul> | STRING1. &#x200B;equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;。 &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### 正则表达式函数

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 根据正则表达式从输入字符串中提取组。 | <ul><li>字符串： **必需** 从中提取组的字符串。</li><li>正则表达式： **必需** 您希望组匹配的正则表达式。</li></ul> | extract_regex(STRING， REGEX) | extract_regex&#x200B;(&quot;E259，E259B_009,1_1&quot;&#x200B;， &quot;([^，]+)，[^，]*，([^，]+)”) | [“E259、E259B_009、1_1”、“E259”、“1_1”] |
| matches_regex | 检查字符串是否与输入的正则表达式匹配。 | <ul><li>字符串： **必需** 正在检查的字符串与正则表达式匹配。</li><li>正则表达式： **必需** 要比较的正则表达式。</li></ul> | matches_regex(STRING， REGEX) | matches_regex(&quot;E259，E259B_009,1_1&quot;， &quot;([^，]+)，[^，]*，([^，]+)”) | true |

{style=&quot;table-layout:auto&quot;}

### 哈希函数 {#hashing}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 采用输入并使用安全哈希算法1 (SHA-1)生成哈希值。 | <ul><li>输入： **必需** 要进行哈希处理的纯文本。</li><li>字符集： *可选* 字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha1（输入，字符集） | sha1（“我的文本”，“UTF-8”） | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | 采用输入并使用安全哈希算法256 (SHA-256)生成哈希值。 | <ul><li>输入： **必需** 要进行哈希处理的纯文本。</li><li>字符集： *可选* 字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha256（输入，字符集） | sha256（“我的文本”，“UTF-8”） | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 采用输入并使用安全哈希算法512 (SHA-512)生成哈希值。 | <ul><li>输入： **必需** 要进行哈希处理的纯文本。</li><li>字符集： *可选* 字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | sha512（输入，字符集） | sha512（“我的文本”，“UTF-8”） | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b7d4fd2ff68a fd24d16 |
| md5 | 获取输入并使用MD5生成哈希值。 | <ul><li>输入： **必需** 要进行哈希处理的纯文本。</li><li>字符集： *可选* 字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。 </li></ul> | md5（输入，字符集） | md5（“我的文本”，“UTF-8”） | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 采用循环冗余校验(CRC)算法生成一个32位循环码。 | <ul><li>输入： **必需** 要进行哈希处理的纯文本。</li><li>字符集： *可选* 字符集的名称。 可能的值包括UTF-8、UTF-16、ISO-8859-1和US-ASCII。</li></ul> | crc32（输入，字符集） | crc32（“我的文本”，“UTF-8”） | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL函数 {#url}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 从给定的URL返回协议。 如果输入无效，则返回null。 | <ul><li>URL： **必需** 需要从中提取协议的URL。</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | 返回给定URL的主机。 如果输入无效，则返回null。 | <ul><li>URL： **必需** 需要从中提取主机的URL。</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 返回给定URL的端口。 如果输入无效，则返回null。 | <ul><li>URL： **必需** 需要从中提取端口的URL。</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | 返回给定URL的路径。 默认情况下，将返回完整路径。 | <ul><li>URL： **必需** 需要从中提取路径的URL。</li><li>完整路径(_P)： *可选* 一个布尔值，确定是否返回完整路径。 如果设置为false，则仅返回路径的结尾。</li></ul> | get_url_path&#x200B;(URL， FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | “//home/joe/&#x200B;employee.csv” |
| get_url_query_str | 将给定URL的查询字符串作为查询字符串名称和查询字符串值的映射返回。 | <ul><li>URL： **必需** 您尝试从中获取查询字符串的URL。</li><li>锚点： **必需** 确定对查询字符串中的锚点执行的操作。 可以是以下三个值之一：“保留”、“移除”或“附加”。<br><br>如果该值为“retain”，则锚点将附加到返回的值。<br>如果该值为“remove”，则将从返回值中删除锚点。<br>如果该值为“append”，则锚点将作为单独值返回。</li></ul> | get_url_query_str&#x200B;(URL， ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there？name=&#x200B;ferret#nose&quot;， &quot;retain&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there？name=&#x200B;ferret#nose&quot;， &quot;remove&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com&#x200B;：8042/over/there&#x200B;？name=ferret#nose&quot;， &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### 日期和时间函数 {#date-and-time}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。 欲知关于 `date` 函数中，日期部分包含了 [数据格式处理指南](./data-handling.md#dates).

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 检索当前时间。 |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | 检索当前Unix时间。 |  | timestamp() | timestamp() | 1571850624571 |
| 格式 | 根据指定的格式设置输入日期的格式。 | <ul><li>日期： **必需** 要格式化的输入日期，作为ZonedDateTime对象。</li><li>格式： **必需** 您希望将日期更改为的格式。</li></ul> | format（日期，格式） | format(2019-10-23T11:24:00+00:00， &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | 根据指定的格式将时间戳转换为日期字符串。 | <ul><li>时间戳： **必需** 要设置格式的时间戳。 这是以毫秒为单位编写的。</li><li>格式： **必需** 您希望时间戳变为的格式。</li></ul> | dformat(TIMESTAMP， FORMAT) | dformat(1571829875000， &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX”) | `2019-10-23T11:24:35.000Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字符串。</li><li>格式： **必需** 表示源日期格式的字符串。**注意：** 这可以 **非** 表示要将日期字符串转换成的格式。 </li><li>DEFAULT_DATE： **必需** 如果提供的日期为null，则返回默认日期。</li></ul> | date(DATE， FORMAT， DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;， now()) | `2019-10-23T11:24:00Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字符串。</li><li>格式： **必需** 表示源日期格式的字符串。**注意：** 这可以 **非** 表示要将日期字符串转换成的格式。 </li></ul> | 日期（日期，格式） | date(&quot;2019-10-23 11:24&quot;， &quot;yyyy-MM-dd HH：mm&quot;) | `2019-10-23T11:24:00Z` |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | <ul><li>日期： **必需** 表示日期的字符串。</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | “2019-10-23T11:24:00Z” |
| date_part | 检索日期的各个部分。 支持以下组件值： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>“dayofyear”<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>“工作日”<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>“hh24”<br>“hh12”<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>“毫秒”<br>&quot;SSS&quot; | <ul><li>组件： **必需** 表示日期部分的字符串。 </li><li>日期： **必需** 日期（标准格式）。</li></ul> | date_part&#x200B;(COMPONENT， DATE) | date_part(&quot;MM&quot;， date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | 替换给定日期中的组件。 接受以下组件： <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>组件： **必需** 表示日期部分的字符串。 </li><li>值： **必需** 为给定日期的组件设置的值。</li><li>日期： **必需** 日期（标准格式）。</li></ul> | set_date_part&#x200B;(COMPONENT， VALUE， DATE) | set_date_part(&quot;m&quot;， 4， date(&quot;2016-11-09T11:44:44.797英寸) | “2016-04-09T11:44:44Z” |
| make_date_time | 从部件创建日期。 此函数还可以使用make_timestamp来诱导。 | <ul><li>年： **必需** 年份，用四位数字写成。</li><li>月： **必需** 月。 允许的值为1到12。</li><li>日： **必需** 那天。 允许的值为1到31。</li><li>小时： **必需** 小时。 允许的值为0到23。</li><li>分钟： **必需** 分钟。 允许的值为0到59。</li><li>纳秒： **必需** 纳秒值。 允许的值为0到999999999。</li><li>时区： **必需** 日期时间的时区。</li></ul> | make_date_time&#x200B;（年、月、日、小时、分钟、秒、纳秒、时区） | make_date_time&#x200B;（2019， 10， 17， 11， 55， 12， 999，“美国/洛杉矶”） | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 将任何时区的日期转换为UTC格式的日期。 | <ul><li>日期： **必需** 您尝试转换的日期。</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 将日期从一个时区转换为另一个时区。 | <ul><li>日期： **必需** 您尝试转换的日期。</li><li>区域： **必需** 您尝试将日期转换为的时区。</li></ul> | zone_date_to_zone&#x200B;(DATE， ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}

### 层次结构 — 对象 {#objects}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 检查对象是否为空。 | <ul><li>输入： **必需** 您尝试检查的对象为空。</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 创建对象列表。 | <ul><li>输入： **必需** 键和数组对的分组。</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 根据给定的平面键/值对创建对象。 | <ul><li>输入： **必需** 键/值对的平面列表。</li></ul> | to_object(INPUT) | to_object&#x200B;(“firstName”、“John”、“lastName”、“Doe”) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 从输入字符串创建对象。 | <ul><li>字符串： **必需** 正在分析以创建对象的字符串。</li><li>VALUE_DELIMITER： *可选* 用于分隔字段和值的分隔符。 默认分隔符为 `:`.</li><li>FIELD_DELIMITER： *可选* 分隔字段值对的分隔符。 默认分隔符为 `,`.</li></ul> | str_to_object&#x200B;(STRING， VALUE_DELIMITER， FIELD_DELIMITER) **注释**：您可以使用 `get()` 函数以及 `str_to_object()` 以检索字符串中键的值。 | <ul><li>示例#1： str_to_object(&quot;firstName - John ； lastName - ； - 123 345 7890&quot;， &quot;-&quot;， &quot;；&quot;)</li><li>示例#2： str_to_object(&quot;firstName - John ； lastName - ； phone - 123 456 7890&quot;， &quot;-&quot;， &quot;；&quot;)。get(&quot;firstName&quot;)</li></ul> | <ul><li>示例#1：`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>示例#2： &quot;John&quot;</li></ul> |
| contains_key | 检查源数据中是否存在该对象。 **注意：** 此函数将替换已弃用的 `is_set()` 函数。 | <ul><li>输入： **必需** 要检查的路径（如果它存在于源数据中）。</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| Nullify | 将属性的值设置为 `null`. 当您不想将字段复制到目标架构时，应使用此字段。 |  | nullify() | nullify() | `null` |
| get_keys | 解析键/值对并返回所有键。 | <ul><li>对象： **必需** 从中提取键的对象。</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;： &quot;Pride and Impance&quot;， &quot;book2&quot;： &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 解析键/值对并根据给定的键返回字符串的值。 | <ul><li>字符串： **必需** 要分析的字符串。</li><li>密钥： **必需** 必须为其提取值的键。</li><li>VALUE_DELIMITER： **必需** 分隔字段和值的分隔符。 如果 `null` 或提供了空字符串，则此值为 `:`.</li><li>FIELD_DELIMITER： *可选* 分隔字段和值对的分隔符。 如果 `null` 或提供了空字符串，则此值为 `,`.</li></ul> | get_values(STRING， KEY， VALUE_DELIMITER， FIELD_DELIMITER) | get_values(\&quot;firstName - John ， lastName - Cena ， phone - 555 420 8692\&quot;， \&quot;firstName\&quot;， \&quot;-\&quot;， \&quot;，\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

有关对象复制功能的信息，请参阅部分 [以下](#object-copy).

### 层级 — 阵列 {#arrays}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 合并 | 返回给定数组中的第一个非空对象。 | <ul><li>输入： **必需** 要查找的第一个非null对象的数组。</li></ul> | 合并（输入） | coalesce(null， null， null， first”， null， second”) | &quot;first&quot; |
| 第一 | 检索给定数组的第一个元素。 | <ul><li>输入： **必需** 要查找的第一个元素的数组。</li></ul> | first(INPUT) | first(“1”、“2”、“3”) | &quot;1&quot; |
| 最后 | 检索给定数组的最后一个元素。 | <ul><li>输入： **必需** 要查找的最后一个元素的数组。</li></ul> | last(INPUT) | last(“1”、“2”、“3”) | &quot;3&quot; |
| add_to_array | 将元素添加到数组的末尾。 | <ul><li>阵列： **必需** 要将元素添加到的数组。</li><li>VALUES：要附加到数组的元素。</li></ul> | add_to_array&#x200B;(ARRAY， VALUES) | add_to_array&#x200B;([&#39;a&#39;、&#39;b&#39;]， &#39;c&#39;， &#39;d&#39;) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;] |
| join_arrays | 将阵列相互组合。 | <ul><li>阵列： **必需** 要将元素添加到的数组。</li><li>值：要附加到父数组的数组。</li></ul> | join_arrays&#x200B;(ARRAY， VALUES) | join_arrays&#x200B;([&#39;a&#39;、&#39;b&#39;]， [&#39;c&#39;]， [&#39;d&#39;， &#39;e&#39;]) | [&#39;a&#39;、&#39;b&#39;、&#39;c&#39;、&#39;d&#39;、&#39;e&#39;] |
| to_array | 获取输入列表并将其转换为数组。 | <ul><li>INCLUDE_NULLS： **必需** 一个布尔值，指示是否在响应数组中包含null。</li><li>值： **必需** 要转换为数组的元素。</li></ul> | to_array&#x200B;(INCLUDE_NULLS， VALUES) | to_array(false， 1， null， 2， 3) | `[1, 2, 3]` |
| size_of | 返回输入的大小。 | <ul><li>输入： **必需** 您正在尝试查找大小为“ ”的对象。</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 此函数用于将整个输入数组中的所有元素附加到配置文件中数组末尾。 此函数为 **仅限** 适用于更新期间。 如果在插入的上下文中使用，则此函数按原样返回输入。 | <ul><li>阵列： **必需** 用于在配置文件中附加数组的数组。</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | 此函数用于替换数组中的元素。 此函数为 **仅限** 适用于更新期间。 如果在插入的上下文中使用，则此函数按原样返回输入。 | <ul><li>阵列： **必需** 在配置文件中替换该数组的数组。</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |

{style=&quot;table-layout:auto&quot;}

### 逻辑运算符 {#logical-operators}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | 给定一个键和一个作为数组扁平化的键值对列表，如果找到键，此函数将返回值，如果数组中存在，则返回默认值。 | <ul><li>密钥： **必需** 要匹配的键。</li><li>OPTIONS： **必需** 键/值对的平面化数组。 或者，也可以在末尾放置默认值。</li></ul> | decode(KEY， OPTIONS) | decode(stateCode， &quot;ca&quot;， &quot;California&quot;， &quot;pa&quot;， &quot;Pennsylvania&quot;， &quot;N/A&quot;) | 如果给定的stateCode为“ca”、“California”。<br>如果给定的stateCode为“pa”，“Pennsylvania”。<br>如果stateCode与以下内容不匹配，则为“不适用”。 |
| iif | 评估给定的布尔表达式并根据结果返回指定的值。 | <ul><li>表达式： **必需** 正在评估的布尔表达式。</li><li>真值： **必需** 表达式计算结果为true时返回的值。</li><li>FALSE_VALUE： **必需** 表达式计算结果为false时返回的值。</li></ul> | iif（表达式，TRUE_VALUE，FALSE_VALUE） | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;)， &quot;True&quot;， &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### 聚合 {#aggregation}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 返回给定参数的最小值。 使用自然排序。 | <ul><li>OPTIONS： **必需** 可以相互比较的一个或多个对象。</li></ul> | min(OPTIONS) | min(3， 1， 4) | 1 |
| max | 返回给定参数的最大值。 使用自然排序。 | <ul><li>OPTIONS： **必需** 可以相互比较的一个或多个对象。</li></ul> | 最大(OPTIONS) | max(3， 1， 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### 类型转换 {#type-conversions}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 将字符串转换为BigInteger。 | <ul><li>字符串： **必需** 要转换为BigInteger的字符串。</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 将字符串转换为双精度类型。 | <ul><li>字符串： **必需** 要转换为Double的字符串。</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 将字符串转换为浮点数。 | <ul><li>字符串： **必需** 要转换为浮点的字符串。</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 将字符串转换为整数。 | <ul><li>字符串： **必需** 要转换为整数的字符串。</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON函数 {#json}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 将给定字符串中的JSON内容反序列化。 | <ul><li>字符串： **必需** 要反序列化的JSON字符串。</li></ul> | json_to_object&#x200B;(STRING) | &#x200B; json_to_object({&quot;info&quot;：{&quot;firstName&quot;：&quot;John&quot;，&quot;lastName&quot;： &quot;Doe&quot;}}) | 表示JSON的对象。 |

{style=&quot;table-layout:auto&quot;}

### 特别行动 {#special-operations}

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 生成伪随机ID。 |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### 用户代理功能 {#user-agent}

下表中包含的任何用户代理函数都可以返回以下任一值：

* 电话 — 带有小屏幕的移动设备（通常小于7英寸）
* 移动设备 — 尚未识别的移动设备。 此移动设备可以是电子阅读器、平板电脑、手机、手表等。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 函数 | 描述 | 参数 | 语法 | 表达式 | 示例输出 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 从用户代理字符串中提取操作系统名称。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46 （KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 从用户代理字符串中提取操作系统的主要版本。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1，如Mac OS X)AppleWebKit/534.46 （KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 从用户代理字符串中提取操作系统的版本。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 从用户代理字符串中提取操作系统的名称和版本。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML like Gecko)版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 从用户代理字符串中提取代理版本。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 从用户代理字符串中提取代理名称和主要版本。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0(iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46（KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 从用户代理字符串中提取代理名称。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46 （KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 从用户代理字符串中提取设备类。 | <ul><li>USER_AGENT： **必需** 用户代理字符串。</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone；CPU iPhone OS 5_1_1_1，如Mac OS X)AppleWebKit/534.46 （KHTML，如Gecko）版本/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Phone |

{style=&quot;table-layout:auto&quot;}

### 对象复制 {#object-copy}

>[!TIP]
>
>当源中的对象映射到XDM中的对象时，会自动应用对象复制功能。 无需用户执行其他操作。

可以使用对象复制功能自动复制对象的属性，而无需对映射进行更改。 例如，如果源数据的结构为：

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

和XDM结构：

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

在上例中， `city` 和 `state` 属性也会在运行时自动摄取，因为 `address` 对象已映射到 `addr`. 如果您要创建 `line2` 属性，并且您的输入数据还包含 `line2` 在 `address` 对象，则它也将自动摄取，而无需手动更改映射。

要确保自动映射正常工作，必须满足以下先决条件：

* 父级对象应进行映射；
* 必须在XDM架构中创建新属性；
* 新属性在源架构和XDM架构中应有匹配的名称。

如果不满足任何先决条件，则必须使用数据准备手动将源架构映射到XDM架构。
