---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark SQL函数
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a23ee02a9e801531a38b5ff70ef07497aa21b174

---


# Spark SQL函数

Spark SQL帮助程序提供内置的Spark SQL函数以扩展SQL功能。

参考： [Spark SQL函数文档](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE] 并非外部文档中的所有功能都受支持。

## 类别

- [数学和统计运算符及函数](#math-and-statistical-operators-and-functions)
- [逻辑运算符](#logical-operators)
- [日期／时间函数](#date/time-functions)
- [聚合函数](#aggregate-functions)
- [阵列](#arrays)
- [数据类型转换函数](#datatype-casting-functions)
- [转换和格式化功能](#conversion-and-formatting-functions)
- [数据评估](#data-evaluation)
- [当前信息](#current-information)

### 数学和统计运算符及函数

#### 取模

`expr1 % expr2`:在／后返回剩余 `expr1`部分`expr2`。

示例：

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### 乘

`expr1 * expr2`: 返回结果 `expr1`*`expr2`.

示例：

```
> SELECT 2 * 3;
 6
```

#### Add

`expr1 + expr2`: 返回结果 `expr1`+`expr2`.

示例：

```
> SELECT 1 + 2;
 3
```

#### 相减

`expr1 - expr2`: 返回结果 `expr1`-`expr2`.

示例：

```
> SELECT 2 - 1;
 1
```

#### 除法

`expr1 / expr2`: 返回结果 `expr1`/`expr2`. 它总是执行浮点除法。

示例：

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`:返回数值的绝对值。

示例：

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`:返回的反余弦（也称为反余弦） `expr`，如同由计算 `java.lang.Math.acos`。

示例：

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentile

`approx_percentile(col, percentage [, accuracy])`:返回给定百分比数值列的 `col` 近似百分点值。 百分比值必须介于0.0和1.0之间。参 `accuracy` 数(默认：10000)是一个正数字文本，它以内存的代价控制近似精度。 数值越大， `accuracy` 精度越高， `1.0/accuracy` 是近似的相对误差。 当 `percentage` 是数组时，百分比数组的每个值必须介于0.0和1.0之间。在这种情况下，将返回给定百分比数组 `col` 处的列的近似百分点数组。

示例：

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`:返回反正弦值（也称为反正弦值），即的反正弦值， `expr`如同通过计算 `java.lang.Math.asin`。

示例：

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`:返回的逆切（也称为逆切） `expr`，如同 `java.lang.Math.atan`

示例：

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`:返回平面的正x轴与坐标(`exprX`, `exprY`)给定的点之间的弧度角，如同由计算 `java.lang.Math.atan2`。

参数：

`exprY`:Y轴上的坐标`exprX`:X轴上的坐标

示例：

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`:返回根据组值计算的平均值。

#### 基数

`cardinality(expr)`:返回数组或映射的大小。 如果函数的输入为null且设置为true(默 `spark.sql.legacy.sizeOfNull` 认)，则该函数返回-1。 如果 `spark.sql.legacy.sizeOfNull` 设置为false，则函数对于null输入返回null。

示例：

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`:返回的多维数据集根 `expr`。

示例：

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`:返回不小于的最小整数 `expr`。

示例：

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### 天花板

`ceiling(expr)`:返回不小于的最小整数 `expr`。

示例：

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`:从 `num` 转换 `from_base` 为 `to_base`

示例：

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### cor

`corr(expr1, expr2)`:返回一组数字对之间的相关的皮尔逊系数。

#### cos

`cos(expr)`:返回的余弦 `expr`值，如同由计算 `java.lang.Math.cos`。

示例：

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`:返回双曲余弦 `expr`值，就像由计算 `java.lang.Math.cosh`。

参数：
- `expr`:双曲角

示例：

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`:返回的余切 `expr`值，就像由计算 `1/java.lang.Math.cot`一样。

参数：
- `expr`:以弧度为单位的角度

示例：

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`:计算一组值中值的排名。 结果是一个加上先前分配的排名值。 与函数不 `rank`同， `dense_rank` 在排序序列中不产生间隙。

#### e

`e()`:返回Euler的数e。

示例：

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`:将e返回至 `expr`。

示例：

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`:返回exp(`expr`)- 1。

示例：

```
> SELECT expm1(0);
 0.0
```

#### 因子

`factorial(expr)`:返回factorial `expr`。 `expr` 是 [0..20]。 否则，为null。

示例：

```
> SELECT factorial(5);
 120
```

#### 地板

`floor(expr)`:返回不大于的最大整数 `expr`。

示例：

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### 最伟大的

`greatest(expr, ...)`:返回所有参数的最大值，跳过null值。

示例：

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### 缺位

`hypot(expr1, expr2)`:返回sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>)。

示例：

```
> SELECT hypot(3, 4);
 5.0
```

#### 峭度

`kurtosis(expr)`:返回根据组值计算的峰度值。


#### 至少

`least(expr, ...)`:返回所有参数的最小值，跳过null值。

示例：

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`:返回两个给定字符串之间的Levenshtein距离。

示例：

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`:返回的自然对数（以e为底） `expr`。

示例：

```
> SELECT ln(1);
 0.0
```

#### 日志

`log(base, expr)`:返回与的对 `expr` 数 `base`。

示例：

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`:返回以10为 `expr` 底的对数。

示例：

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: 返回结果 `log(1 + expr)`.

示例：

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`:返回以2为 `expr` 底的对数。

示例：

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`:返回最大值 `expr`。

#### mean

`mean(expr)`:返回根据组值计算的平均值。

#### min

`min(expr)`:返回最小值 `expr`。

#### monotically_increanging_id

`monotonically_increasing_id()`:返回单调递增的64位整数。 所生成的ID被保证是单调增加且唯一的，但不是连续的。 当前实现将分区ID放在上部31位中，而下部33位表示每个分区内的记录数。 假定数据帧的分区数少于10亿，每个分区的记录数少于80亿。 该函数是非确定性的，因为其结果取决于分区ID。

#### 负

`negative(expr)`:返回的否定值 `expr`。

示例：

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`:计算一组值中某个值的百分比排名。

#### 百分点

`percentile(col, percentage [, frequency])`:返回给定百分比数字列的 `col` 精确百分位值。 值必须 `percentage` 介于0.0和1.0之间。值应 `frequency` 为正积分。

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`:返回给定百分比数字列的精确百 `col` 分点值数组。 百分比数组的每个值必须介于0.0和1.0之间。值应 `frequency` 为正积分。

#### percentile_approx

`percentile_approx(col, percentage [, accuracy])`:返回给定百分比数值列的 `col` 近似百分点值。 值必须 `percentage` 介于0.0和1.0之间。参 `accuracy` 数(默认：10000)是一个正数字文本，它以内存的代价控制近似精度。 数值越大， `accuracy` 精度越高， `1.0/accuracy` 是近似的相对误差。 当 `percentage` 是数组时，百分比数组的每个值必须介于0.0和1.0之间。在这种情况下，返回给定百分比数组的列的 `col` 近似百分点数组。

示例：

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`:返回pi。

示例：

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`:返回mod的正 `expr1` 值 `expr2`。

示例：

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### 正

`positive(expr)`:返回正值 `expr`

#### pow

`pow(expr1, expr2)`:提 `expr1` 升了力量 `expr2`。

示例：

```
> SELECT pow(2, 3);
 8.0
```

#### 功率

`power(expr1, expr2)`:提 `expr1` 升了力量 `expr2`。

示例：

```
> SELECT power(2, 3);
 8.0
```

#### 弧度

`radians(expr)`:将度数转换为弧度。

参数：

- `expr`:角度（以度为单位）

示例：

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`:返回一个随机值，该随机值具有独立且分布相同(i.i.d.)的均匀分布值(在(0, 1)中)。

示例：

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE] 在一般情况下，此函数是非确定性的。

#### randn

`randn([seed])`:返回一个随机值，该值具有从标准正态分布中提取的独立且分布相同(i.i.d.)的值。

示例：

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE] 在一般情况下，此函数是非确定性的。

#### rint

`rint(expr)`:返回值最接近参数的多次值，它等于一个数学整数。

示例：

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`:使用 `expr` HALF_UP `d` 舍入模式返回舍入到小数位。

示例：

```
> SELECT round(2.5, 0);
 3.0
```

#### 签名

`sign(expr)`:返回-1.0、0.0或1.0, `expr` 为负、0或正。

示例：

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`:返回-1.0、0.0或1.0, `expr` 作为负、0或正。

示例：

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`:返回的正弦 `expr`值，如同由计算 `java.lang.Math.sin`。

参数：

- `expr`:以弧度为单位的角度

示例：

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`:返回双曲正弦 `expr`值，就像由计算 `java.lang.Math.sinh`的。

参数：

- `expr`:双曲角

示例：

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`:返回的平方根 `expr`。

示例：

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`:返回根据组值计算的样本标准偏差。

#### stddev_pop

`sttdev_pop(expr)`:返回根据组值计算的人口标准差。

#### stddev_samp

`stddev_samp(expr)`:返回根据组值计算的样本标准偏差。

#### sum

`sum(expr)`:返回根据组值计算的总和。

#### 陈

`tan(expr)`:返回的正 `expr`切，如同由计算 `java.lang.Math.tan`。

参数：

- `expr`:以弧度为单位的角度

示例：

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`:返回的双曲正 `expr`切，就像通过计算 `java.lang.Math.tanh`。

参数：

- `expr`:双曲角

示例：

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`:返回根据组值计算的人口差异。

#### Var_samp

`var_samp(expr)`:返回根据组值计算的样本差异。

#### 方差

`variance(expr)`:返回根据组值计算的样本差异。

### 逻辑运算符

#### 逻辑不

`! expr`:不合逻辑。

#### 小于

`expr1 < expr2`:如果小于， `expr1` 则返回true `expr2`。

参数：

- `expr1, expr2`:两个表达式必须是同一类型，或者可以转换为通用类型，并且必须是可排序的类型。 例如，映射类型不可排序，因此不支持它。 对于数组／结构等复杂类型，字段的数据类型必须可排序。

示例：

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### 小于或等于

`expr1 <= expr2`:如果小于 `expr1` 或等于，则返回true `expr2`。

参数：

- `expr1, expr2`:两个表达式必须是同一类型或可以转换为通用类型，并且必须是可排序的类型。 例如，映射类型不可排序，因此不支持它。 对于复杂类型（如数组／结构），字段的数据类型必须可排序。

示例：

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### 等于

`expr1 = expr2`:如果等于，则返 `expr1` 回true `expr2`，否则返回false。

参数：

- `expr1, expr2`:两个表达式必须是同一类型，或者可以转换为通用类型，并且必须是可用于等式比较的类型。 不支持映射类型。 对于数组／结构等复杂类型，字段的数据类型必须可排序。

示例：

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### 大于

`expr1 > expr2`:如果大于， `expr1` 则返回true `expr2`。

参数：

- `expr1, expr2`:两个表达式必须是同一类型，或者可以转换为通用类型，并且必须是可排序的类型。 例如，映射类型不可排序，因此不支持它。 对于数组／结构等复杂类型，字段的数据类型必须可排序。

示例：

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### 大于或等于

`expr1 >= expr2`:如果大于 `expr1` 或等于，则返回true `expr2`。

参数：

- `expr1, expr2`:两个表达式必须是同一类型，或者可以转换为通用类型，并且必须是可排序的类型。 例如，映射类型不可排序，因此不支持它。 对于数组／结构等复杂类型，字段的数据类型必须可排序。

示例：

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### 按位排它或

`expr1 ^ expr2`:返回和的按位排它的OR的 `expr1` 结果 `expr2`。

示例：

```
> SELECT 3 ^ 5;
 2
```

#### 和

`expr1 and expr2`:逻辑和。

#### arrays_overlap

`arrays_overlap(a1, a2)`:如果a1至少包含a2中也存在的非空元素，则返回true。 如果数组没有公共元素，且它们都是非空的，并且其中任何一个都包含空元素，则返回null。 否则，返回false。

示例：

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

自：2.4.0

#### assert_true

`assert_true(expr)`:如果不为true，则 `expr` 引发异常。

示例：

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`:如果 `expr1` 计算结果为true，则返回 `expr2`;否则返回 `expr3`。

示例：

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`:如果 `expr2` 为 `expr1` null，则返回，否则 `expr1` 返回。

示例：

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`:如果等于任何 `expr` valN，则返回true。

参数：
- `expr1, expr2, expr3, ...`:参数的类型必须相同。

示例：

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`:如果为NaN，则返 `expr` 回true，否则返回false。

示例：

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`:如果不为null, `expr` 则返回true，否则返回false。

示例：

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`:如果为null，则 `expr` 返回true，否则返回false。

示例：

```
> SELECT isnull(1);
 false
```

#### 纳米

`nanvl(expr1, expr2)`:如果 `expr1` 它不是NaN，则返回，否则 `expr2` 返回。

示例：

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`:不合逻辑。

#### 或

`expr1 or expr2`:逻辑或。

#### xpath_boolean

`xpath_boolean(xml, xpath)`:如果XPath表达式的计算结果为true，或者如果找到匹配的节点，则返回true。

示例：

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### 日期／时间函数

#### add_months

`add_months(start_date, num_months)`:返回后面的日 `num_months` 期 `start_date`。

示例：

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

自：1.5.0

#### date_add

`date_add(start_date, num_days)`:返回后面的日 `num_days` 期 `start_date`。

示例：

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

自：1.5.0

#### date_format

`date_format(timestamp, fmt)`:转换 `timestamp` 为日期格式指定格式的字符串值 `fmt`。

示例：

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

自：1.5.0

#### date_sub

`date_sub(start_date, num_days)`:返回之前的 `num_days` 日期 `start_date`。

示例：

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

自：1.5.0

#### date_trunc

`date_trunc(fmt, ts)`:返回截断为格式模型指定单位的时间戳 `fmt`。 `fmt` 应为 [“年”、“YYY”、“YY”、“MON”、“月”、“MM”、“日”、“DD”、“小时”、“分钟”、“秒”、“周”、“季度”之一]

示例：

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

自：2.3.0

#### datediff

`datediff(endDate, startDate)`:返回从到的天 `startDate` 数 `endDate`。

示例：

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

自：1.5.0

#### 天

`day(date)`:返回日期／时间戳的月份日期。

示例：

```
> SELECT day('2009-07-30');
 30
```

自：1.5.0

#### dayofmonth

`dayofmonth(date)`:返回日期／时间戳的月份日期。

示例：

```
> SELECT dayofmonth('2009-07-30');
 30
```

自：1.5.0

#### dayofweek

`dayofweek(date)`:返回日期／时间戳（1 =星期日，2 =星期一，..., 7 =星期六）的星期几。

示例：

```
> SELECT dayofweek('2009-07-30');
 5
```

自：2.3.0

#### 年

`dayofyear(date)`:返回日期／时间戳的年份日期。

示例：

```
> SELECT dayofyear('2016-04-09');
 100
```

自：1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`:在指 `unix_time` 定值中返回 `format`。

示例：

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

自：1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`:将“2017-07-14 02:40:00.0”等时间戳解释为UTC时间，并将该时间渲染为给定时区的时间戳。 例如，“GMT+1”将生成“2017-07-14 03:40:00.0”。

示例：

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

自：1.5.0

#### 小时

`hour(timestamp)`:返回字符串／时间戳的小时组件。

示例：

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

自：1.5.0

#### last_day

`last_day(date):` 返回日期所属月份的最后一天。

示例：

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

自：1.5.0

#### 分钟

`minute(timestamp)`:返回字符串／时间戳的分钟组件。

示例：

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

自：1.5.0

#### 月

`month(date)` 返回日期／时间戳的月份组件。

示例：

```
> SELECT month('2016-07-30');
 7
```

自：1.5.0

#### months_between

`months_between(timestamp1, timestamp2[, roundOff])`:如果 `timestamp1` 晚于， `timestamp2`则结果为正。 如果 `timestamp1` 和 `timestamp2` 在月的同一天，或两者都是月的最后一天，则将忽略某天的时间。 否则，差额将根据每月31天计算，并舍入至8位数，除非如此 `roundOff=false`。

示例：

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

自：1.5.0

#### next_day

`next_day(start_date, day_of_week)`:返回第一个日期，该日期晚于并 `start_date` 按指示命名。

示例：

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

自：1.5.0

#### 季度

`quarter(date)`:返回日期在一年中的季度，范围为1到4。

示例：

```
> SELECT quarter('2016-08-31');
 3
```

自：1.5.0

#### 秒

`second(timestamp)`:返回字符串／时间戳的第二个组件。

示例：

```
> SELECT second('2009-07-30 12:58:59');
 59
```

自：1.5.0

#### to_date

`to_date(date_str[, fmt])`:将表达式 `date_str` 与表达式解析 `fmt` 到某个日期。 输入无效时返回null。 默认情况下，如果忽略该属性，它将遵循转换规 `fmt` 则到日期。

示例：

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

自：1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`:将带有 `timestamp` 表达式的表达式解析 `fmt` 为时间戳。 输入无效时返回null。 默认情况下，如果忽略该属性，它将遵循转换规则到 `fmt` 时间戳。

示例：

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

自：2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`:返回给定时间的UNIX时间戳。

示例：

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

自：1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`:将“2017-07-14 02:40:00.0”等时间戳解释为给定时区中的时间，并将该时间以UTC表示为时间戳。 例如，“GMT+1”将生成“2017-07-14 01:40:00.0”。

示例：

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

自：1.5.0

#### trunc

`trunc(date, fmt)`:返回日期，其中日期的时间部分被截断为格式模型指定的单位 `fmt`。 `fmt` 是&quot;year&quot;、 [&quot;yyyy&quot;、&quot;yy&quot;、&quot;mon&quot;、&quot;month&quot;、&quot;mm&quot;之一]

示例：

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

自：1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`:返回当前或指定时间的UNIX时间戳。

示例：

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

自：1.5.0

#### 工作日

`weekday(date)`:返回日期／时间戳的星期几（0 =星期一，1 =星期二，..., 6 =星期日）。

示例：

```
> SELECT weekday('2009-07-30');
 3
```

自：2.4.0

#### week_of_year

`weekofyear(date)`:返回给定日期的一年中的某周。 周被视为星期一的开始，周1是第一周，超过3天。

示例：

```
> SELECT weekofyear('2008-02-20');
 8
```

自：1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`:当 `expr1` 为true时，返回 `expr2`;else when `expr3` = true, returns `expr4`;else返回 `expr5`。

参数：

- `expr1`, `expr3`:分支条件表达式应全部为布尔类型。
- `expr2`, `expr4`, `expr5`:分支值表达式和else值表达式应全部为相同类型或可强制为公共类型。

示例：

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### 年

`year(date)`:返回日期／时间戳的年份组件。

示例：

```
> SELECT year('2016-07-30');
 2016
```

自：1.5.0

### 聚合函数

#### approx_count_distinct

`approx_count_distinct(expr[, relativeSD])`:返回HyperLogLog++的估计基数。 `relativeSD` 定义允许的最大估计错误。

### 阵列

#### 阵列

`array(expr, ...)`:返回一个包含给定元素的数组。

示例：

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`:如果数组包含值，则返回true。

示例：

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinct

`array_distinct(array)`:从数组中删除重复值。

示例：

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

自：2.4.0

#### array_except

`array_except(array1, array2)`:在中但不在中返回一组元 `array1` 素，而 `array2`不包含重复。

示例：

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

自：2.4.0

#### array_intersect

`array_intersect(array1, array2)`:返回与(不带重复)交叉处 `array1` 的元 `array2`素数组。

示例：

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

自：2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`:使用分隔符和可选字符串连接给定数组的元素以替换空值。 如果未设置任何值， `nullReplacement`则过滤任何空值。

示例：

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

自：2.4.0

#### array_max

`array_max(array)`:返回数组中的最大值。 跳过空元素。

示例：

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

自：2.4.0

#### array_min

`array_min(array)`:返回数组中的最小值。 跳过空元素。

示例：

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

自：2.4.0

#### array_position

`array_position(array, element)`:返回数组第一个元素（基于1）的索引，长度如此之长。

示例：

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

自：2.4.0

#### array_remove

`array_remove(array, element)`:从数组中删除与元素相等的所有元素。

示例：

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

自：2.4.0

#### array_repeat

`array_repeat(element, count)`:返回包含元素计数时间的数组。

示例：

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

自：2.4.0

#### array_sort

`array_sort(array)`:按升序对输入数组排序。 输入数组的元素必须可以排序。 空元素位于返回的数组的末尾。

示例：

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

自：2.4.0

#### array_合并

`array_union(array1, array2)`:返回和合并中的元素数组， `array1` 不 `array2`带重复。

示例：

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

自：2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`:返回结构的合并数组，其中第N个结构包含输入数组的所有第N个值。

示例：

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

自：2.4.0

#### element_at

`element_at(array, index)`:返回给定（基于1）索引处的数组元素。 如 `index < 0`果是，则访问从最后一个到第一个的元素。 如果索引超过数组的长度，则返回NULL。

`element_at(map, key)`:返回给定键的值；如果键不包含在映射中，则返回NULL

示例：

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

自：2.4.0

#### 爆炸

`explode(expr)`:将数组元素分 `expr` 成多行，或将映射元素分成多 `expr` 行和多列。

示例：

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`:将数组元素分 `expr` 成多行，或将映射元素分成多 `expr` 行和多列。

示例：

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`:以逗号分隔的列表()返回给定字符串(`str`)的索引(基于1的索引`str_array`)。 如果未找到该字符串或给定的字符串(`str`)包含逗号，则返回0。

示例：

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### 拼合

`flatten(arrayOfArrays)`:将数组转换为单个数组。

示例：

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

自：2.4.0

#### 内嵌

`inline(expr)`:将一组结构分解为一个表。

示例：

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inilne_outer

`inline_outer(expr)`:将一组结构分解为一个表。

示例：

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplode

`posexplode(expr)`:将数组的元素分 `expr` 成多行，多行，多行，多行，多 `expr` 列，多行，多列，多位。

示例：

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`:将数组的元素分 `expr` 成多行，多行，多行，多行，多 `expr` 列，多行，多列，多位。

示例：

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### 逆

`reverse(array)`:返回一个反向的字符串或元素顺序相反的数组。

示例：

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

自：1.5.0
>[!NOTE] 阵列的rse逻辑自2.4.0起可用。

#### 随机

`shuffle(array)`:返回给定数组的随机排列。

示例：

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

自：2.4.0
>[!NOTE] 函数是非确定性的。

#### 切片

`slice(x, start, length)`:从索引开始开始(如果开始为负，则从结束开始)的子集数组x具有指定的长度。

示例：

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

自：2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`:根据阵列元素的自然顺序，按升序或降序对输入数组进行排序。 空元素按升序放置在返回数组的开头或按降序放置在返回数组的结尾。

示例：

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`:使用函数将两个给定的数组（按元素）合并为一个数组。 如果一个数组较短，则在应用函数之前，会在末尾附加空值以匹配较长数组的长度。

示例：

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

自：2.4.0

### 数据类型转换函数

#### bigint

`bigint(expr)`:将值转换 `expr` 为目标数据类型 `bigint`。

#### 二进制

`binary(expr)`:将值转换 `expr` 为目标数据类型 `binary`。

#### 布尔

`boolean(expr)`:将值转换 `expr` 为目标数据类型 `boolean`。

#### cast

`cast(expr AS type)`:将值转换 `expr` 为目标数据类型 `type`。

示例：

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`:将值转换 `expr` 为目标数据类型 `date`。

#### 小数点

`decimal(expr)`:将值转换 `expr` 为目标数据类型 `decimal`。

#### 多次

`double(expr)`:将值转换 `expr` 为目标数据类型 `double`。

#### 浮动

`float(expr)`:将值转换 `expr` 为目标数据类型 `float`。

#### int

`int(expr)`:将值转换 `expr` 为目标数据类型 `int`。

#### 地图

`map(key0, value0, key1, value1, ...)`:创建具有给定键／值对的映射。

示例：

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)`:将值转换 `expr` 为目标数据类型 `smallint`。

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`:在使用分隔符将文本拆分为键／值对之后创建映射。 默认分隔符为&#39;,&#39;表示， `pairDelim` &#39;:&#39;表示 `keyValueDelim`。

示例：

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### 字符串

`string(expr)`:将值转换 `expr` 为目标数据类型 `string`。

#### struct

`struct(col1, col2, col3, ...)`:创建具有给定字段值的结构。

#### tinyint

`tinyint(expr)`:将值转换 `expr` 为目标数据类型 `tinyint`。

### 转换和格式化功能

#### ascii

`ascii(str)`:返回的第一个字符的数字值 `str`。

示例：

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`:将参数从二进制转 `bin` 换为基64字符串。

示例：

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### 宾

`bin(expr)`:返回以二进制表示的长值的字 `expr` 符串表示形式。

示例：

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`:返回字符串数据的位长度或二进制数据的位数。

示例：

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`:返回二进制等效于的ASCII字符 `expr`。 如果n大于256，则结果等效于 `chr(n % 256)`。

示例：

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`:返回字符串数据的字符长度或二进制数据的字节数。 字符串数据的长度包括尾部空格。 二进制数据的长度包括二进制零。

示例：

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`:返回字符串数据的字符长度或二进制数据的字节数。 字符串数据的长度包括尾部空格。 二进制数据的长度包括二进制零。

示例：

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`:返回具有与expr等效的二进制的ASCII字符。 如果n大于256，则结果等同于 `chr(n % 256)`

示例：

```
> SELECT chr(65);
 A
```

#### 度

`degrees(expr)`:将弧度转换为度。

参数：
- `expr`:以弧度为单位的角度

示例：

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`:设置数字 `expr1` 的格式，如“#、###、###”。##&#39;，四舍五入至小 `expr2` 数位。 如果 `expr2` 为0，则结果没有小数点或小数部分。 `expr2` 也接受用户指定的格式。 它的功能与MySQL类似 `FORMAT`。

示例：

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`:返回一个包含给定和的结 `jsonStr` 构值 `schema`。

示例：

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

自：2.2.0

#### 哈希

`hash(expr1, expr2, ...)`:返回参数的哈希值。

示例：

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### 十六进制

`hex(expr)`:转换 `expr` 为十六进制。

示例：

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`:返回 `str` 时，每个单词的第一个字母都以大写形式显示。 所有其他字母均以小写形式显示。 单词以空格分隔。

示例：

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`:返回 `str` 时，所有字符都更改为小写。

示例：

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`:返回 `str` 时，所有字符都更改为小写。

示例：

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`:退 `str`回，左边填充 `pad` 一段长度 `len`。 如果 `str` 长度大于 `len`此值，则返回值将缩短为字 `len` 符。

示例：

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### 地图

`map(key0, value0, key1, value1, ...)`:创建具有给定键／值对的映射。

示例：

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`:使用一对给定键／值数组创建映射。 键中的元素不能为null。

示例：

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

自：2.4.0

#### map_from_entries

`map_from_entries(arrayOfEntries)`:返回从给定条目数组创建的映射。

示例：

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

自：2.4.0

#### md5

`md5(expr)`:将MD5 128位校验和作为十六进制字符串返回 `expr`。

示例：

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`:返 `str`回，右边填充 `pad` 一段长度 `len`。 如果 `str` 长度大于 `len`此值，则返回值将缩短为字 `len` 符。

示例：

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`:从中删除尾随空格字符 `str`。

`rtrim(trimStr, str)`:删除尾随字符串，该字符串包含从中的修剪字符串中的字符 `str`。

参数：
- `str`:字符串表达式
- `trimStr`:要修剪的修剪字符串字符。 默认值是单个空格

示例：

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`:返回 `sha1` 哈希值作为的十六进制字符串 `expr`。

示例：

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`:返回 `sha1` 哈希值作为的十六进制字符串 `expr`。

示例：

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`:将SHA-2系列的校验和作为十六进制字符串返回 `expr`。 支持SHA-224、SHA-256、SHA-384和SHA-512。 位长度为0等于256。

示例：

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`:返回字符串的Soundex代码。

示例：

```
> SELECT soundex('Miller');
 M460
```

#### 堆栈

`stack(n, expr1, ..., exprk)`:分 `expr1`成几行…… `exprk` .. `n` 行。

示例：

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`:返回该开始的 `str` 子字符串 `pos` ，其长度为，或者该开始的字节数组的片段，该片段的长 `len`度为和 `pos``len`。

示例：

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### 子字符串

`substring(str, pos[, len])`:返回该开始的 `str` 子字符串 `pos` ，其长度为，或者该开始的字节数组的片段，该片段的长 `len`度为和 `pos``len`。

示例：

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`:返回具有给定结构值的JSON字符串。

示例：

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

自：2.2.0

#### 翻译

`translate(input, from, to)`:将字符串 `input` 中存在的字符替换为字符串中 `from` 的相应字符，从而转换字符串 `to` 。

示例：

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`:从中删除前导和尾部空格字符 `str`。

`trim(BOTH trimStr FROM str)`:从中删除前导和尾 `trimStr` 部字符 `str`。

`trim(LEADING trimStr FROM str)`:从中删除前 `trimStr` 导字符 `str`。

`trim(TRAILING trimStr FROM str)`:从中删除尾 `trimStr` 随字符 `str`。

参数：
- `str`:字符串表达式
- `trimStr`:要裁切的裁切字符串字符，默认值是单个空格
- `BOTH`, `FROM`:这些关键字用于指定字符串两端的修剪字符串字符
- `LEADING`, `FROM`:这些关键字用于从字符串的左端指定修剪字符串字符
- `TRAILING`, `FROM`:这些关键字用于从字符串的右端指定修剪字符串字符

示例：

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### 酶

`ucase(str)`:返回 `str` 时，所有字符都更改为大写。

示例：

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`:将参数从基64字符串转换 `str` 为二进制。

示例：

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`:将十六进制转 `expr` 换为二进制。

示例：

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`:返回 `str` 时，所有字符都更改为大写。

示例：

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`:返回通用唯一标识符(UUID)字符串。 该值将作为规范的UUID 36字符串返回。

示例：

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE] 函数是非确定性的。

### 数据评估

#### 凝聚

`coalesce(expr1, expr2, ...)`:返回第一个非null参数（如果存在）。 否则，为null。

示例：

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_列表

`collect_list(expr)`:收集并返回一列表非唯一元素。

#### collect_set

`collect_set(expr)`:收集并返回一组唯一元素。

#### concat

`concat(col1, col2, ..., colN)`:返回col1、col2、...、colN的串联。

示例：

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE] 阵 `concat` 列逻辑自2.4.0起可用。

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`:返回以分隔的字符串的串联 `sep`。

示例：

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`:返回已检索行的总数，包括包含null的行。

`count(expr[, expr...])`:返回所提供表达式均为非null的行数。

`count(DISTINCT expr[, expr...])`:返回所提供表达式为唯一且非null的行数。

#### crc32

`crc32(expr)`:返回作为大整数的循环 `expr` 冗余校验值。

示例：

```
> SELECT crc32('Spark');
 1557323817
```

#### 解码

`decode(bin, charset)`:使用第二个参数字符集解码第一个参数。

示例：

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### 跪

`elt(n, input1, input2, ...)`:返回 `n`第三个输入，例如，当 `input2` 为 `n` 2时。

示例：

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### 编码

`encode(str, charset)`:使用第二个参数字符集对第一个参数进行编码。

示例：

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`:返回一组行 `expr` 的第一个值。 如果 `isIgnoreNull` 为true，则仅返回非null值。

#### first_value

`first_value(expr[, isIgnoreNull])`:返回一组行 `expr` 的第一个值。 如果 `isIgnoreNull` 为true，则仅返回非null值。

#### get_json_object

`get_json_object(json_txt, path)`:从中提取json对象 `path`。

示例：

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### 分组

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`:返回第一个出现的（基于1的）索引 `substr` , `str`in

示例：

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`:返回一个元组（如函数）, `get_json_object`但它采用多个名称。 所有输入参数和输出列类型都是字符串。

示例：

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### 滞后

`lag(input[, offset[, default]])`:返回窗口 `input` 中当 `offset`前行前第一行的值。 默认值 `offset` 为1，默认值为 `default` null。 如果第行 `input` 的值 `offset`为null，则返回null。 如果没有此类偏移行（例如，当偏移为1时，窗口的第一行没有任何以前的行），并将返 `default` 回该行。

#### last

`last(expr[, isIgnoreNull])`:返回一组行 `expr` 的最后一个值。 如果 `isIgnoreNull` 为true，则仅返回非null值。

#### last_value

`last_value(expr[, isIgnoreNull])`:返回一组行 `expr` 的最后一个值。 如果 `isIgnoreNull` 为true，则仅返回非null值。

#### 铅

`lead(input[, offset[, default]])`:返回窗口 `input` 中当 `offset`前行后第一行的值。 默认值 `offset` 为1，默认值为 `default` null。 如果第行 `input` 的值 `offset`为null，则返回null。 如果没有这样的偏移行（例如，当偏移为1时，窗口的最后一行没有任何后续行），则返回 `default` 该行。


#### 左

`left(str, len)`:返回字符串 `len` 中最左`len` 侧的字符（可以是字符串类型） `str`。 如 `len` 果小于或等于0，则结果为空字符串。

示例：

> SELECT left(&#39;Spark SQL&#39;, 3);Spa


#### length

`length(expr)`:返回字符串数据的字符长度或二进制数据的字节数。 字符串数据的长度包括尾部空格。 二进制数据的长度包括二进制零。

示例：

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### 定位

`locate(substr, str[, pos])`:返回第一个出现在后面位置 `substr` 的 `str` 位置 `pos`。 给定 `pos` 值和返回值基于1。

示例：

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`:返回所有给定映射的合并。

示例：

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

自：2.4.0

#### map_keys

`map_keys(map)`:返回包含映射键的无序数组。

示例：

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`:返回包含映射值的无序数组。

示例：

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`:将每个窗口分区的行分 `n` 为范围从1到最多的时段 `n`。

#### 无效

`nullif(expr1, expr2)`:如果等于或 `expr1` 其他值， `expr2`则返回 `expr1` null。

示例：

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`:如果 `expr2` 为 `expr1` null，则返回，否则 `expr1` 返回。

示例：

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`:如果 `expr2` 不 `expr1` 为null，则返回，否则 `expr3` 返回。

示例：

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`:从URL提取部件。

示例：

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`:返回第一个出现在后面位置 `substr` 的 `str` 位置 `pos`。 给定 `pos` 值和返回值基于1。

示例：

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### 秩

`rank()`:计算一组值中值的排名。 结果是，在分区的排序中，前面或等于当前行的行数加1。 这些值在序列中产生间隙。

#### regexp_extract

`regexp_extract(str, regexp[, idx])`:提取匹配的组 `regexp`。

示例：

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`:替换与匹配的 `str` 所有子 `regexp` 字符串 `rep`。

示例：

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### 重复

`repeat(str, n)`:返回重复给定字符串值n次的字符串。

示例：

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`:将所有出现的 `search` 项替换为 `replace`。

参数：
- `str`:字符串表达式
- `search`:字符串表达式。 如果 `search` 在中未找到， `str`则 `str` 返回不变。
- `replace`:字符串表达式。 如果 `replace` 未指定或为空字符串，则不替换从中删除的字符串 `str`。

示例：

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### 汇总

<!-- was blank -->

#### row_number

`row_number()`:根据窗口分区内各行的顺序，为每个行分配一个唯一的顺序编号，从一个开始。

#### 模式_of_json

`schema_of_json(json[, options])`:返回JSON字符串DDL格式的模式。

示例：

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

自：2.4.0

#### 句子

`sentences(str[, lang, country])`:拆 `str` 分为一组单词。

示例：

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### 序列

`sequence(start, stop, step)`:生成从开始到停止（包括）的元素数组，逐步递增。 返回元素的类型与参数表达式的类型相同。

支持的类型有：byte, short, integer, long, date, timestamp.

和 `start` 表达式 `stop` 必须解析为同一类型。 如果 `start` 和 `stop` 表达式解析为“日期”或“时间戳”类型，则 `step` 表达式必须解析为“间隔”类型；否则，它解析为与和表达式相同 `start` 的类 `stop` 型。

参数：
- `start`:表达式。 范围的开始。
- `stop`:表达式。 范围（包括）的结束。
- `step`:可选表达式。 范围的步骤。 默认情 `step` 况下，如 `start` 果小于或等于，则为1，否 `stop`则为-1。 对于时序，分别为1天和-1天。 如 `start` 果大于 `stop`，则 `step` 为负，反之亦然。

示例：

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

自：2.4.0

#### shiftleft

`shiftleft(base, expr)`:按位左移。

示例：

```
> SELECT shiftleft(2, 1);
 4
```

#### shiftright

`shiftright(base, expr)`:按位（已签名）右移。

示例：

```
> SELECT shiftright(4, 1);
 2
```

#### shittrightunged

`shiftrightunsigned(base, expr)`:按位无符号右移。

示例：

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### 大小

`size(expr)`:返回数组或映射的大小。 如果函数的输入为null且设置为true，则该函 `spark.sql.legacy.sizeOfNull` 数返回-1。 如果 `spark.sql.legacy.sizeOfNull` 设置为false，则函数对于null输入返回null。 默认情况下， `spark.sql.legacy.sizeOfNull` 该参数设置为true。

示例：

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### 空间

`space(n)`:返回一个包含空格的 `n` 字符串。

示例：

```
> SELECT concat(space(2), '1');
   1
```

#### 拆分

`split(str, regex)`:在匹配 `str` 的实例周围拆分 `regex`。

示例：

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`:返回分隔符出现 `str` 前的 `count` 子字符串 `delim`。 如 `count` 果为正，则返回最终分隔符左侧的所有内容（从左侧计数）。 如 `count` 果为负，则返回最终分隔符右侧的所有内容（从右侧计数）。 函数在 `substring_index` 搜索时执行区分大小写的匹配 `delim`。

示例：

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### 窗口

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`:返回xml节点中与XPath表达式匹配的值的字符串数组。

示例：

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_多次

`xpath_double(xml, xpath)`:返回多次值；如果未找到匹配项，则返回值零；如果找到匹配项，但该值为非数字值，则返回NaN。

示例：

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`:返回浮点值；如果未找到匹配项，则返回值零；如果找到匹配项，但该值为非数字值，则返回NaN。

示例：

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`:返回整数值；如果未找到匹配项，则返回值零；如果找到匹配项，但该值为非数字值。

示例：

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`:返回一个长整数值；如果未找到匹配项，则返回值零；如果找到匹配项，但该值为非数字值。

示例：

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`:返回多次值；如果未找到匹配项，则返回值零；如果找到匹配项，但该值为非数字值，则返回NaN。

示例：

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`:返回一个短整数值，或者如果找不到匹配项，或者找到匹配项但该值为非数字值，则返回值零。

示例：

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`:返回与XPath表达式匹配的第一个xml节点的文本内容。

示例：

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### 当前信息

#### current_database

`current_database()`:返回当前数据库。

示例：

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`:返回查询评估开始的当前日期。

自：1.5.0

#### current_timestamp

`current_timestamp()`:返回查询评估开始的当前时间戳。

自：1.5.0

#### now

`now()`:返回查询评估开始的当前时间戳。

自：1.5.0
