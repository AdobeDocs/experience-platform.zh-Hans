---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;date;date functions;dates;
solution: Experience Platform
title: 日期函数
topic: overview
description: 本文档介绍了数据准备中使用的日期功能。
translation-type: tm+mt
source-git-commit: 1f9833c06a3423c334edb8aa7e441adfd74be0f2
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 17%

---


# 日期函数

数据准备支持日期函数，既作为字符串，也作为日期时间对象。

## 日期函数转换

当使用体验数据模型(XDM)将传入数据的字符串字段映射到模式中的日期字段时，应明确提及日期格式。 如果未明确提及，数据准备将尝试将输入数据与以下格式进行匹配，从而转换该数据。 找到匹配格式后，将停止评估任何后续格式。

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
> 数据准备将尝试尽可能将字符串转换为最佳日期。 但是，这些转换可能会产生不良结果。 例如，字符串值“12112020”与模式“MMdyyyy”匹配，但用户可能希望使用模式“ddMMyyyy”读取日期。 因此，用户应明确提及字符串的日期格式。

## 日期／时间格式字符串

下表显示了为格式字符串定义的模式字母。 请注意，这些字母区分大小写。

| 符号 | 意义 | 演示文稿 | 示例 |
| ------ | ------- | ------------ | ------- |
| G | 时代 | 文本 | 广告；安诺·多米尼；A |
| Y | 年，基于ISO周 | 数值 | 1996; 96 |
| y | 年 | 数值 | 2004; 04 |
| M/L | 年月 | 数字／文本 | 7;07;7月；7月；J |
| w | 一年中的一周 | 数值 | 27 |
| W | 月中的周 | 数值 | 3 |
| D | 一年中的某天 | 数值 | 189 |
| d | 当月日 | 数值 | 10 |
| F | 一个月中的一周中的某天 | 数值 | 2 |
| E | 星期的名称 | 文本 | 星期二；周二 |
| u | 星期几，作为数字。 1代表星期一， ..., 7代表星期日 | 数值 | 1 |
| a | 上午／下午标记 | 文本 | PM |
| H | 一天中的小时数(0-23) | 数值 | 0 |
| k | 一天中的小时数(1-24) | 数值 | 24 |
| K | 上午／下午小时(0-11) | 数值 | 0 |
| h | 上午／下午的小时(1-12) | 数值 | 12 |
| m | 每小时的分钟数 | 数值 | 38 |
| s | 分秒 | 数值 | 44 |
| S | 毫秒 | 数值 | 245 |
| z | 时区 | 一般时区 | 太平洋标准时间；太平洋标准时间；GMT-08:00 |
| Z | 时区 | RFC 822时区 | -0800 |
| X | 时区 | ISO 8601时区 | -08; -0800; -08:00 |
| V | 时区ID | 文本 | 美国／洛杉矶 |
| O | 时区偏移 | 文本 | GMT+8 |
| Q/q | 一年中的季度 | 数字／文本 | 3;03;第三季度；第三季度 |

**示例**

表达式 `date(orderDate, 'yyyy-MM-dd')` 会将值 `orderDate` “2020年12月31日”转换为日期时间值“2020-12-31”。