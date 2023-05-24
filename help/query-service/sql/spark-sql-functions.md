---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；spark sql；Spark sql；spark；spark sql函式；函式；
solution: Experience Platform
title: 查詢服務中的Spark SQL函式
description: 本檔案包含擴充SQL功能的Spark SQL函式的資訊。
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 0%

---

# [!DNL Spark] SQL函式

Adobe Experience Platform Query Service提供數種內建的Spark SQL函式，以擴充SQL功能。 本檔案列出Query Service支援的Spark SQL函式。

如需函式的詳細資訊，包括其語法、使用方式和範例，請參閱 [Spark SQL函式檔案](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>並非外部檔案中的所有函式都受支援。

## 數學和統計運運算元和函式 {#math}

| 運運算元/函式 | 描述 |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | 傳回兩個數字的餘數 |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | 將兩個數字相乘 |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | 將兩個數字相加 |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 減去兩個數字 |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 將兩個數字相除 |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | 傳回輸入的絕對值 |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | 傳回反餘弦值 |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | 傳回HyperLogLog的估計基數++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | 傳回給定百分比的近似百分位數值 |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | 傳回反正弦值 |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | 傳回反正切值 |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | 傳回x軸正平面與座標所指定點之間的角度 |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | 傳回平均值 |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | 傳回立方根 |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) 或 [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | 傳回不大於輸入值的最小整數 |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | 從一個基底轉換到另一個基底 |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | 傳回數字之間的皮爾遜係數 |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | 傳回餘弦值 |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | 傳回雙曲餘弦值 |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | 傳回餘切值 |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | 傳回值在值群組中的排名 |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | 傳回Euler數字 |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | 將e傳回值的冪 |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | 傳回e為值減去1的冪 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | 傳回值的階乘 |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | 傳回不小於值的最大整數 |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | 傳回所有引數的最大值 |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | 傳回給定兩個值的次冪 |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | 傳回群組的峭度值 |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | 傳回所有引數的最小值 |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | 傳回值的自然對數 |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | 傳回值的對數 |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | 傳回值的對數（以10為單位） |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | 傳回值加1的對數 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | 傳回以2為底的對數值 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | 傳回運算式的最大值 |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | 傳回從值計算出的平均值 |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | 傳回運算式的最小值 |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | 傳回單調遞增的ID |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | 傳回否定值 |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | 傳回值的百分比排名 |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | 傳回指定百分比的確切百分位數 |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | 傳回給定百分比的近似百分位數 |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | 傳回pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | 傳回兩個值之間的正模數 |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | 傳回正值 |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | 將第一個值傳回至第二個值的冪 |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | 將值轉換為弧度 |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | 傳回0到1之間的隨機數字 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | 傳回隨機值 |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | 傳回最接近的雙精度值 |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | 傳回最接近的舍入值 |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | 傳回數字的符號 |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | 傳回值的正弦 |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | 傳回值的雙曲正弦 |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | 傳回值的平方根 |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | 傳回值的標準差 |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | 傳回值的母體標準差 |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | 傳回值的範例標準差 |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | 傳回值的總和 |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | 傳回值的正切 |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | 傳回值的雙曲正切 |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | 傳回計算的母體變異數 |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | 傳回計算的樣本變異數 |

### 邏輯運運算元和函式 {#logical-operators}

| 運運算元/函式 | 描述 |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) 或 [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | 邏輯非 |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 小于 |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | 小于或等于 |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | 等于 |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | 大于 |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | 大于或等于 |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | 位元排除或 |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | 位元或 |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | 位元非 |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | 傳回常見元素 |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | 判斷運算式是否為true |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | 如果運算式的計算結果為true，則傳回第二個運算式。 否則，傳回第三個運算式。 |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | 如果運算式為null，則會傳回第二個運算式。 否則，會傳回第一個運算式。 |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | 如果第一個運算式位於任何後續運算式中，則傳回true。 |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | 如果值不是數字，則傳回true |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | 如果值不是null，則傳回true |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | 如果值為null，則傳回true |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | 若不是數字，則傳回第一個運算式，否則傳回第二個運算式 |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | 邏輯或 |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | 何時可用來建立分支條件以進行比較 |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | 如果XPath運算式的評估結果為true或找到相符的節點，則傳回true |

### 日期/時間函式 {#datetime-functions}

| 函数 | 描述 |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | 按日期新增月份 |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | 新增日期至日期 |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | 修改日期格式 |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | 從日期減去天數 |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | 傳回截斷為指定單位的日期 |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | 傳回日期之間的差異（以天為單位） |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | 傳回該月的第幾天 |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | 傳回星期幾(1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | 傳回一年中的第幾天 |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | 以Unix時間傳回日期 |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | 以UTC時間傳回日期 |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | 傳回輸入的小時 |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | 傳回日期所屬月份的最後一天 |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | 傳回輸入的分鐘數 |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | 傳回輸入的月份 |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | 月數介於 |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | 傳回比輸入晚的第一天 |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | 傳回輸入的季度 |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | 傳回字串的秒數 |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | 將字串轉換為日期。 **注意：** 字串 **必須** 採用格式 `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | 將字串轉換為時間戳記。 **注意：** 字串 **必須** 採用格式 `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | 將字串轉換為Unix時間戳記 |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | 將字串轉換為UTC時間戳記 |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | 截斷日期 |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | 傳回Unix時間戳記 |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | 星期(0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | 傳回指定日期在一年中的第幾週 |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | 傳回字串的年份 |

### 数组 {#arrays}

| 函数 | 描述 |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | 使用指定的元素建立陣列 |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | 檢查陣列是否包含值 |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | 從陣列中移除重複值 |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | 傳回第一個陣列中的元素陣列，但不傳回第二個陣列 |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | 傳回兩個陣列的交集 |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | 將兩個陣列連線在一起 |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | 傳回陣列的最大值 |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | 傳回陣列的最小值 |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | 傳回元素以1為底的位置 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | 移除等於元素的所有元素 |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | 建立包含已計算次數的值的陣列 |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | 排序陣列 |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | 將陣列聯結在一起，沒有任何重複專案 |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | 結合指定陣列的值與指定索引處的原始集合值 |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | 傳回陣列的大小 |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | 傳回位置上的元素 |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | 將陣列元素分隔成多列，不包括null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | 將陣列元素分隔成多列，包括null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | 傳回陣列以1為基底的位置 |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | 平面化陣列陣列 |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | 將結構陣列分隔到表格中，不包括null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | 將結構陣列分隔到表格中，包括null |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | 將陣列元素分隔成含有位置的多個列，不包括null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | 反轉陣列元素 |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | 傳回陣列的隨機排列 |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | 將陣列設為子集 |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | 依順序排序陣列 |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | 在套用函式之前，將兩個陣列合併為單一陣列 |

### 資料型別轉換函式 {#datatype-casting}

| 函数 | 描述 |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | 將資料型別變更為bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | 將資料型別變更為二進位 |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | 將資料型別變更為布林值 |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | 將資料型別變更為指定的型別 |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | 將資料型別變更為日期 |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | 將資料型別變更為小數 |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | 將資料型別變更為兩次 |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | 將資料型別變更為浮點數 |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | 將資料型別變更為int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | 將資料型別變更為smallint |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | 從字串建立對應 |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | 將資料型別變更為字串 |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | 建立結構 |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | 將資料型別變更為tinyint |

### 轉換和格式化函式 {#conversion}

| 函数 | 描述 |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | 傳回數值(ASCII)值 |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | 將引數變更為base64字串 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | 將引數變更為二進位值 |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | 傳回位元長度 |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | 傳回ASCII字元 |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | 傳回字串長度 |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | 傳回循環冗餘檢查值 |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | 將弧度轉換為度 |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | 變更號碼的格式 |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | 從JSON取得資料 |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | 傳回雜湊值 |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | 將引數轉換為十六進位值 |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | 將字串變更為標題大小寫 |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | 將字串變更為全部小寫 |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | 貼上字串的左側 |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | 建立地圖 |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | 從陣列建立對應 |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | 從結構陣列建立對應 |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | 傳回md5值 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | 貼上字串的右側 |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | 移除結尾空格 |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | 傳回SHA1值 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | 傳回SHA2值 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | 傳回soundex程式碼 |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | 將值分隔成列 |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | 傳回子字串 |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | 傳回JSON字串 |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | 取代字串中的值 |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | 移除前置字元和結尾字元 |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | 將字串變更為全部大寫 |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | 將base64字串轉換為二進位 |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | 將十六進位轉換為二進位 |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | 傳回UUID |

### 資料評估 {#data-evaluation}

| 函数 | 描述 |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | 傳回第一個非null引數 |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | 傳回非唯一元素清單 |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | 傳回一組不重複元素 |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | 串連 |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | 使用分隔符號串連 |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | 傳回列的總計數 |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | 使用字元集解碼 |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | 傳回 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)輸入 |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | 使用字元集編碼 |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | 傳回第一個值 |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | 指示欄是否分組 |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | 傳回群組層級 |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | 傳回以1為基礎的字元出現索引 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | 從JSON輸入傳回Tuple |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | 傳回位移前的值 |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | 傳回最後一個值 |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | 傳回第一個 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 個字元 |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | 傳回字串的長度 |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | 傳回字串之間的Levenshtein距離 |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | 傳回子字串第一次出現的位置 |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | 串連地圖 |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | 傳回對應的索引鍵 |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | 傳回對應的值 |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | 將資料列分割成分割區 |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | 如果為true，則傳回null |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | 如果為null，則傳回值 |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | 如果不為空，則傳回值 |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | 擷取部分URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | 計算值的排名 |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | 擷取和規則運算式相符的內容 |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | 取代符合regex的內容 |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | 傳回重複的字串 |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | 取代字串的所有例項 |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | 建立多維度統計 |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | 指派唯一的列號 |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | 傳回JSON的結構描述 |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | 將字串分割為字元陣列 |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | 產生元素陣列 |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | 帶正負號的位元左移 |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | 帶正負號位元右移 |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | 無正負號位元右移 |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | 傳回陣列的大小 |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | 傳回字串，其中 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 空間 |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | 分割字串 |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | 傳回子字串的索引 |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | 視窗 |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | 剖析XML節點 |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | 剖析XML節點以取得雙精度浮點數 |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | 剖析浮點數的XML節點 |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | 剖析整數的XML節點 |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | 長時間剖析XML節點 |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | 剖析短整數的XML節點 |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | 剖析字串的XML節點 |

### 目前資訊 {#current-information}

| 函数 | 描述 |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | 傳回目前的資料庫 |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | 傳回目前日期 |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | 傳回目前的時間戳記 |

### 高階函式 {#higher-order}

| 函数 | 描述 |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | 轉換陣列中的元素 |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | 檢查元素是否存在 |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | 篩選輸入陣列 |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | 將二進位運運算元套用至所有元素 |
