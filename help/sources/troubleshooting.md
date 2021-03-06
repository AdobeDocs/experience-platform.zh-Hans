---
keywords: Experience Platform；主页；热门主题；源；摄取；故障诊断；源故障诊断；源常见问题解答；源连接器；源连接器；源连接器；常见问题解答；源连接器故障诊断；
solution: Experience Platform
title: 源疑难解答
topic-legacy: troubleshooting
description: 本文档提供有关Adobe Experience Platform源的常见问题解答。
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: b55097b6e7cd49166f68d0c86b788cd36ebdebab
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 源疑难解答指南

本文档提供有关Adobe Experience Platform源的常见问题解答。 有关与其他 [!DNL Platform] 服务，包括在所有 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

## 常见问题

以下是有关来源的常见问题解答的列表。

### 我是否必须更改网络安全设置才能启用源？

您可能需要允许列表某些IP地址才能启用源。 有关更多信息，请阅读有关特定源连接器的文档。

### 源支持哪些身份验证类型？

源可以使用连接字符串、用户名和密码或访问令牌和密钥进行身份验证。 有关支持的身份验证类型的特定详细信息，请参阅指定源连接器的文档。

### 为什么我最近的流量都会失败？

如果您注意到所有最近的流运行都失败，则您的凭据可能已更改或过期。 要解决此问题，请尝试使用最新凭据更新连接。

### 支持哪些文件类型？

目前，支持的文件类型为分隔文件、JSON和Parquet。

### 对文件名和大小的限制是什么？

以下是源中必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点，如 `\uE000`，但在NTFS文件名中有效，是无效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中控制Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点(.)字符和两个点(.)字符。
- 每批文件的最大数量为1500，最大批量为100 GB。
- 每行的属性或字段的最大数为10,000。
- 每用户每分钟可发送的批次数上限为138个。

### 支持哪些数据类型？

支持的数据类型包括整数、字符串、布尔值、日期时间对象、数组和对象。

### 支持哪些日期和时间格式？

源在摄取数据时支持多种日期时间格式。 有关支持的日期时间格式的详细信息，请参阅 [数据格式处理指南](../data-prep/data-handling.md#dates) （在数据准备文档中）。

### 如何在CSV、JSON和Parquet文件中设置数组格式？

JSON和Parquet文件本身支持数组。 对于平面结构（如CSV），不支持数组。 但是，可以使用数据准备函数（如分解和连接）将具有多个值的字符串划分为数组。 有关这些数据准备函数的更多信息，请参阅 [数据准备功能指南](../data-prep/functions.md#string)

### 哪些源支持部分摄取？

所有批量摄取源都支持部分摄取。 但是，流摄取源不支持部分摄取。

### 何时应使用部分摄取？

如果需要，则应使用部分摄取 **not** 具有限制，例如将整个文件摄取到平台中。 或者，如果您不介意摄取数据中可能包含错误，则应使用部分摄取。

### 典型的部分摄取错误阈值是什么？

部分摄取没有“典型错误阈值”。 此值因用例而异。 默认情况下，错误阈值设置为5%。

### 创建新数据流后，流运行状态需要多长时间才能更新？

流量运行不会即时生成，在指定后可能需要大约两到三分钟才能进行更新 `startTime`. 创建新数据流后立即检查流运行的状态不会返回有关流运行的信息 `lastRunDetails` 因为它尚未发生。 建议在检查流运行状态之前，允许在几分钟内生成数据流。