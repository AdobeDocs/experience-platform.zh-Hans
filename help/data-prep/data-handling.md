---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；ui指南；映射器；映射；数据准备；数据准备；准备数据；
solution: Experience Platform
title: 使用数据准备处理数据格式
description: 本文档概述了数据准备中处理不同数据类型的方式。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 8%

---

# 使用数据准备处理数据格式

数据准备可以稳健地处理摄取到Adobe Experience Platform中的不同格式的数据。 本文档概述了如何使用数据准备处理不同的数据格式。

## 布尔昂 {#booleans}

如果源类型是字符串，而目标类型是布尔值，则数据准备可以自动解析该值并将源值转换为布尔值。

自动将值`y`、`yes`、`Y`、`YES`、`on`、`ON`、`true`和`TRUE`解析为`true`。

自动将值`n`、`N`、`no`、`NO`、`off`、`OFF`、`false`和`FALSE`解析为`false`。

## 日期 {#dates}

数据准备支持日期函数，包括字符串和日期时间对象。

### 日期函数格式

日期函数将字符串和日期时间对象转换为ISO 8601格式的ZonedDateTime对象。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATE}` | 必需。表示日期的字符串。 |
| `{FORMAT}` | 可选。 表示源日期格式的字符串。 有关字符串格式的详细信息，请参阅[日期/时间格式字符串部分](#format)。 |
| `{DEFAULT_DATE}` | 可选。 如果提供的日期为null，则返回默认日期。 |

例如，表达式`date(orderDate, "yyyy-MM-dd")`会将`orderDate`值“December 31， 2020”转换为datetime值“2020-12-31”。

### 日期函数转换

当来自传入数据的字符串字段映射到使用Experience Data Model (XDM)的架构中的日期字段时，应明确提及日期格式。 如果未明确提及，数据准备将尝试通过将输入数据与以下格式匹配来转换输入数据。 找到匹配的格式后，将停止评估任何后续格式。

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
> 数据准备将尝试尽可能将字符串转换为日期。 但是，这些转化可能会导致不良结果。 例如，字符串值“12112020”与模式“MMddyyyy”匹配，但用户可能希望以模式“ddMMyyyy”读取日期。 因此，用户应明确提及字符串的日期格式。

### 日期/时间格式字符串 {#format}

下表显示了为格式字符串定义的样式字母。 请注意，这些字母区分大小写。

| 符号 | 含义 | 演示文稿 | 示例 |
| ------ | ------- | ------------ | ------- |
| G | 时代 | 文本 | AD； Anno Domini； A |
| Y | 年，基于ISO周 | 数值 | 1996； 96 |
| y | 年 | 数值 | 2004； 04 |
| M/L | 月份 | 数字/文本 | 7；07；7月；7月；J |
| w | 一年中的周 | 数值 | 27 |
| W | 月中周 | 数值 | 3 |
| D | 每年的某一日 | 数值 | 189 |
| d | 日期 | 数值 | 10 |
| F | 一个月中星期几 | 数值 | 2 |
| E | 一周中某天的名称 | 文本 | 星期二；星期二 |
| u | 星期几（数字）。 1表示星期一， ...， 7表示星期日 | 数值 | 1 |
| 一个 | AM/PM标记 | 文本 | 下午 |
| H | 一天中的小时(0-23) | 数值 | 0 |
| k | 一天中的小时(1-24) | 数值 | 24 |
| K | 上午/下午的小时(0-11) | 数值 | 0 |
| h | 上午/下午的小时(1-12) | 数值 | 12 |
| m | 一小时中的分钟 | 数值 | 38 |
| s | 一分钟中的秒 | 数值 | 44 |
| S | 毫秒 | 数值 | 245 |
| z | 时区 | 常规时区 | 太平洋标准时间；PST；GMT-08:00 |
| Z | 时区 | rfc 822时区 | -0800 |
| X | 时区 | ISO 8601时区 | -08； -0800； -08:00 |
| V | 时区Id | 文本 | 美国/洛杉矶 |
| O | 时区偏移 | 文本 | GMT+8 |
| Q/q | 季度 | 数字/文本 | 第三季度；03；第三季度 |

## 地图 {#maps}

[!DNL Data Prep]当前不支持映射。
