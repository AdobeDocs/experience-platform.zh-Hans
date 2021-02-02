---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；spark sql;Spark sql;spark sql函数；函数；
solution: Experience Platform
title: Spark SQL函数
topic: spark sql functions
description: 本文档包含有关扩展SQL功能的Spark SQL函数的信息。
translation-type: tm+mt
source-git-commit: 019de34c5e4ac53d38887752e893733f843dd22f
workflow-type: tm+mt
source-wordcount: '3890'
ht-degree: 1%

---


# [!DNL Spark] SQL函数

Adobe Experience Platform查询服务提供多个内置的Spark SQL函数来扩展SQL功能。 此文档列表查询服务支持的Spark SQL函数。

有关这些函数的详细信息，包括它们的语法、用法和示例，请阅读[Spark SQL函数文档](https://spark.apache.org/docs/latest/api/sql/index.html)。

>[!NOTE]
>
>并非外部文档中的所有功能都受支持。

## 类别

- [数学和统计运算符及函数](#math)
- [逻辑运算符](#logical-operators)
- [日期／时间函数](#datetime-functions)
- [阵列](#arrays)
- [数据类型转换函数](#datatype-casting)
- [转换和格式化功能](#conversion)
- [数据评估](#data-evaluation)
- [当前信息](#current-information)
- [高阶函数](#higher-order)

## 数学和统计运算符及函数{#math}

| 运算符／函数 | 描述 |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | 返回两个数字的余数 |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | 将两个数字相乘 |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | 将两个数字相加 |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | 减去两个数字 |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 将两个数字除以 |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | 返回输入的绝对值 |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | 返回反余弦值 |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | 返回HyperLogLog++的估计基数 |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | 返回给定百分比的近似百分点值 |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | 返回反正弦值 |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | 返回反切值 |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | 返回正x轴平面与坐标所给点之间的角度 |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | 返回平均值 |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | 返回多维数据集根 |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) 或 [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | 返回不大于输入值的最小整数 |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | 从一个基础转换为另一个基础 |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | 返回数字之间的皮尔逊系数 |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | 返回余弦值 |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | 返回双曲余弦值 |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | 返回余切值 |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | 返回值组中值的排名 |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | 返回Euler数 |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | 返回e值的幂 |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | 返回值减1的幂 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | 返回值的阶乘 |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | 返回不小于该值的最大整数 |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | 返回所有参数的最大值 |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | 返回给定的两个值的斜边 |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | 返回组的峭度值 |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | 返回所有参数的最小值 |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | 返回值的自然对数 |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | 返回值的对数 |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | 返回值以10为底的对数 |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | 返回值加1的对数 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | 返回值以2为底的对数 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | 返回表达式的最大值 |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | 返回从值计算的平均值 |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | 返回表达式的最小值 |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | 返回单调递增的ID |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | 返回否定值 |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | 返回值的百分比排名 |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | 返回给定百分比的精确百分点 |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | 返回给定百分比的近似百分点 |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | 返回pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | 返回两个值之间的正模 |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | 返回正数 |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow),  [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | 将第一个值返回第二个值的幂 |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | 将值转换为弧度 |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | 返回0到1之间的随机数 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | 返回随机值 |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | 返回最接近的多次值 |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | 返回最接近的舍入值 |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | 返回数字的符号 |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | 返回值的正弦值 |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | 返回值的双曲正弦 |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | 返回值的平方根 |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | 返回值的标准偏差 |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | 返回值的人口标准偏差 |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | 返回值的示例标准偏差 |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | 返回值的和 |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | 返回值的正切 |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | 返回值的双曲正切 |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | 返回计算的人口差异 |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | 返回计算的样本差异 |

### 逻辑运算符和函数{#logical-operators}

| 运算符／函数 | 描述 |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) 或 [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | 逻辑不 |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 小于 |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 小于或等于 |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | 等于 |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | 大于 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | 大于或等于 |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | 按位排它或 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | 大于或等于 |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | 按位或 |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | 不按位 |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | 返回公用元素 |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | 声明表达式是否为真 |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | 如果表达式的计算结果为true，则返回第二个表达式。 否则，返回第三个表达式。 |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | 如果表达式为null，则返回第二个表达式。 否则，返回第一个表达式。 |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | 如果第一个表达式位于任何后续表达式中，则返回true。 |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | 如果值不是数字，则返回true |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | 如果值不为null，则返回true |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | 如果值为null，则返回true |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | 如果不是数字，则返回第一个表达式，否则返回第二个表达式 |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | 逻辑或 |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | 何时可用于创建分支条件进行比较 |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | 如果XPath表达式的计算结果为true或找到匹配节点，则返回true |

### 日期／时间函数{#datetime-functions}

| 函数 | 描述 |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | 将月份添加到日期 |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | 添加截止日期 |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | 修改日期格式 |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | 从日期减去天数 |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | 返回截断到指定单位的日期 |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | 返回日期之间的差异（以天为单位） |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | 返回月中的某天 |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | 返回星期(1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | 返回年份中的某天 |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Unix时间中的返回日期 |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | 返回日期（以UTC时间为单位） |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | 返回输入小时数 |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | 返回日期所属月份的最后一天 |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | 返回输入的分钟数 |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | 返回输入月份 |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | 月数 |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | 返回比输入日期晚的第一天 |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | 返回输入的四分之一 |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | 返回字符串的第二个 |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | 将字符串转换为日期 |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | 将字符串转换为时间戳 |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | 将字符串转换为Unix时间戳 |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | 将字符串转换为UTC时间戳 |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | 截断日期 |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | 返回Unix时间戳 |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | 星期(0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | 返回给定日期的一年中的一周 |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | 返回字符串的年份 |

### 阵列{#arrays}

| 函数 | 描述 |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | 使用给定元素创建数组 |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | 检查数组是否包含值 |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | 从数组删除重复值 |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | 返回第一个数组中元素的数组，但不返回第二个数组 |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | 返回两个数组的交集 |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | 将两个阵列连接在一起 |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | 返回数组的最大值 |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | 返回数组的最小值 |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | 返回元素的基于1的位置 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | 删除与元素相等的所有元素 |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | 创建包含值计数次数的数组 |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | 对数组排序 |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | 将阵列连接在一起，无需任何重复 |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Zip |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | 返回数组大小 |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | 将元素返回位置 |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | 将数组元素分成多行，不包括null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | 将数组元素分成多行，包括null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | 返回基于1的数组位置 |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | 拼合数组 |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | 将结构数组分离到表中，不包括null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | 将结构数组分离到表中，包括null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | 将数组元素分成多行，位置不包括null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | 将数组元素分成多行，并带有位置（包括null） |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | 反向数组元素 |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | 返回数组的随机排列 |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | 对数组进行子集化 |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | 按顺序对数组排序 |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | 在应用函数之前，将两个数组合并到单个数组中 |

### 数据类型转换函数{#datatype-casting}

| 函数 | 描述 |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | 将数据类型更改为bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | 将数据类型更改为二进制 |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | 将数据类型更改为布尔值 |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | 将数据类型更改为指定类型 |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | 将数据类型更改为日期 |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | 将数据类型更改为十进制 |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | 将数据类型更改为多次 |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | 将数据类型更改为浮动 |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | 将数据类型更改为int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | 将数据类型更改为小闪烁 |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | 从字符串创建映射 |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | 将数据类型更改为字符串 |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | 创建结构 |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | 将数据类型更改为tinyint |

### 转换和格式化函数{#conversion}

| 函数 | 描述 |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | 返回数字(ASCII)值 |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | 将参数更改为base64字符串 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | 将参数更改为二进制值 |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | 返回位长度 |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | 返回ASCII字符 |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | 返回字符串长度 |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | 返回循环冗余校验值 |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | 将弧度转换为度 |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | 更改数字的格式 |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | 从JSON获取数据 |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | 返回哈希值 |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | 将参数转换为十六进制值 |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | 将字符串更改为大小写 |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | 将字符串更改为全小写 |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | 将字符串的左侧填充 |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | 创建地图 |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | 从数组创建映射 |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | 从结构数组创建映射 |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | 返回md5值 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | 将字符串的右侧 |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | 删除尾随空格 |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | 返回SHA1值 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | 返回SHA2值 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | 返回soundex代码 |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | 将值分隔为行 |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | 返回子字符串 |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | 返回JSON字符串 |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | 替换字符串中的值 |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | 删除前导和尾部字符 |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | 将字符串更改为全大写 |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | 将base64字符串转换为二进制 |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | 将十六进制转换为二进制 |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | 返回UUID |

### 数据评估{#data-evaluation}

| 函数 | 描述 |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | 返回第一个非空参数 |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | 返回一列表非唯一元素 |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | 返回一组唯一元素 |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | 级联 |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | 带分隔符的串连 |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | 返回行的总计数 |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | 使用字符集进行解码 |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | 返回[`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)输入 |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | 使用字符集进行编码 |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | 返回第一个值 |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | 指示列是否已分组 |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | 返回分组级别 |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | 返回基于1的字符出现索引 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | 从JSON输入返回元组 |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | 返回偏移前的值 |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | 返回最后一个值 |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | 返回前一个[`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)字符 |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | 返回字符串的长度 |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | 返回字符串之间的列文施泰因距离 |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | 返回子字符串第一次出现的位置 |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | 连接映射 |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | 返回地图的键 |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | 返回映射的值 |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | 将行分为多个分区 |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | 如果为True，则返回Null |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | 返回null值 |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | 如果不为null，则返回值 |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | 提取部分URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | 计算值的排名 |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | 提取与正则表达式匹配的内容 |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | 替换与正则表达式匹配的内容 |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | 返回重复的字符串 |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | 替换字符串的所有实例 |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | 创建多维汇总 |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | 指定唯一行号 |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | 返回JSON的模式 |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | 将字符串拆分为一组字 |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | 生成元素数组 |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | 带符号的向左位移 |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | 带符号的按位向右移动 |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | 无符号按位向右移位 |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | 返回数组大小 |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | 返回带有[`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)空格的字符串 |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | 拆分字符串 |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | 子字符串的返回索引 |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | 窗口 |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | 解析XML节点 |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | 解析XML节点以进行多次 |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | 解析浮点的XML节点 |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | 解析XML节点以获取整数 |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | 解析长XML节点 |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | 解析短整数的XML节点 |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | 解析字符串的XML节点 |

### 当前信息{#current-information}

| 函数 | 描述 |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | 返回当前数据库 |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | 返回当前日期 |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | 返回当前时间戳 |

### 高阶函数{#higher-order}

| 函数 | 描述 |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | 变换数组中的元素 |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | 检查元素是否存在 |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | 过滤输入数组 |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | 将二进制运算符应用于所有元素 |