---
keywords: Experience Platform；主页；热门主题；map csv;map csv;map csv文件；map csv文件到xdm;map csv到xdm;ui指南；mapper;mapping;data preparation;data preparation;preparing data;
solution: Experience Platform
title: 使用数据准备处理数据格式
topic-legacy: overview
description: 本文档概述了在数据准备中处理不同数据类型的方式。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 13%

---

# 使用数据准备处理数据格式

Data Prep可以强健地处理引入到Adobe Experience Platform中的不同格式数据。 本文档概述了如何使用数据准备处理不同的数据格式。

## 布尔语{#booleans}

如果源类型是字符串，而目标类型是布尔值，Data Prep可以自动分析该值并将源值转换为布尔值。

将值`y`、`yes`、`Y`、`YES`、`on`、`ON`、`true`和`TRUE`自动解析为`true`。

将值`n`、`N`、`no`、`NO`、`off`、`OFF`、`false`和`FALSE`自动解析为`false`。

## 日期{#dates}

Data Prep支持date函数，既作为字符串，也作为datetime对象。

### Date函数格式

date函数将字符串和日期时间对象转换为ISO 8601格式化的ZonedDateTime对象。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATE}` | 必需。表示日期的字符串。 |
| `{FORMAT}` | 可选。表示日期格式的字符串。 有关字符串格式的详细信息，请参阅[date/time格式字符串部分](#format)。 |
| `{DEFAULT_DATE}` | 可选。如果提供的日期为null，则返回的默认日期。 |

例如，表达式`date(orderDate, "yyyy-MM-dd")`将`orderDate`值“2020年12月31日”转换为日期时间值“2020-12-31”。

### 日期函数转换

使用体验数据模型(XDM)将传入模式的字符串字段映射到其中的日期字段时，应明确提及日期格式。 如果未明确提及，数据准备将尝试将输入数据与以下格式进行匹配以转换。 找到匹配格式后，将停止评估任何后续格式。

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> 数据准备将尝试将字符串转换为最佳日期。 但是，这些转换可能会产生不期望的结果。 例如，字符串值“12112020”与模式“MMddyyyy”匹配，但用户可能希望使用模式“ddMMyyyy”读取日期。 因此，用户应明确提及字符串的日期格式。

### 日期/时间格式字符串{#format}

下表显示了为格式字符串定义的模式字母。 请注意，这些字母区分大小写。

| 符号 | 意义 | 演示文稿 | 示例 |
| ------ | ------- | ------------ | ------- |
| G | 时代 | 文本 | AD;安诺·多米尼；A |
| Y | 年，基于ISO周 | 数值 | 1996;96 |
| y | 年 | 数值 | 2004年；04 |
| M/L | 年月 | 数字/文本 | 7;07;7月；7月；J |
| w | 一年中的一周 | 数值 | 27 |
| W | 当月 | 数值 | 3 |
| D | 年中 | 数值 | 189 |
| d | 当月 | 数值 | 10 |
| F | 一个月中的一星期 | 数值 | 2 |
| E | 星期的名称 | 文本 | 星期二；星期二 |
| u | 星期，作为数字。 1代表星期一……, 7代表星期日 | 数值 | 1 |
| a | AM/PM标记 | 文本 | PM |
| H | 一天中的小时数(0-23) | 数值 | 0 |
| k | 一天中的小时数(1-24) | 数值 | 24 |
| K | 上午/下午的小时(0-11) | 数值 | 0 |
| h | 上午/下午的小时(1-12) | 数值 | 12 |
| m | 一小时中的分钟 | 数值 | 38 |
| s | 分秒 | 数值 | 44 |
| S | 毫秒 | 数值 | 245 |
| z | 时区 | 一般时区 | 太平洋标准时间；太平洋标准时间；GMT-08:00 |
| Z | 时区 | RFC 822时区 | -0800 |
| X | 时区 | ISO 8601时区 | -08;-0800;-08:00 |
| V | 时区ID | 文本 | 美国/洛杉矶 |
| O | 时区偏移 | 文本 | GMT+8 |
| Q/q | 每年 | 数字/文本 | 3;03;第3季度；第三季度 |
