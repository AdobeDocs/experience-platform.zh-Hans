---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 计算属性的PQL表达式示例
type: Documentation
description: 计算属性是用于将事件级数据聚合到配置文件级属性的函数。 这些函数需要使用有效的配置文件查询语言(PQL)表达式。 本指南概述了计算属性的一些最常用的PQL表达式。
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha)计算属性的PQL表达式示例

>[!IMPORTANT]
>
>计算属性功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。

在Adobe Experience Platform中，计算属性是用于将事件级数据聚合到配置文件级属性的函数。 这些函数是自动计算的，以便可在分段、激活和个性化之间使用。 每个计算属性都定义有基本信息，如名称和说明、架构类和保存该值的字段的路径，以及表达式，其计算值是要在计算属性中存储的值。

计算属性中使用的表达式使用以下方式创建 [!DNL Profile Query Language] (PQL)，一种与Experience Data Model (XDM)兼容的查询语言，旨在支持对实时客户档案数据的查询的定义和执行。

计算属性当前支持以下函数：sum、count、min、max和boolean。 本指南概述了在为组织定义自己的计算属性时可以使用的一些最常用的PQL表达式。 有关PQL的更多信息以及其他格式指南的链接和支持的查询示例，请访问 [PQL概述](../../segmentation/pql/overview.md).

## 流表达式

下表提供了在流模式下支持的常用查询表达式的详细信息。

| 描述 | PQL表达式 | 输入类型：<br/>配置文件或体验事件(EE)[]) | 结果类型 |
|---|---|---|---|
| 过去7天下载图像的次数。 | xEvent[（时间戳早于现在7天）和eventType=&quot;download&quot;以及contentType =&quot;image&quot;].count() | 配置文件和EE[] | 整数 |
| 过去7天客户在体育用品上的支出总和。 | xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].sum(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天客户在体育用品上的平均支出。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1：** xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2：** xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].count()<br/><br/>**ca3：** ca1 / ca2 | 配置文件和EE[] | 双精度 |
| 客户在过去7天花在体育用品上的钱是否超过100美元？<br/><br/>**注意：** 需要创建两个计算属性。 | **ca1：** xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2：** ca1 > 100 | 配置文件和EE[] | 布尔值 |
| 客户在过去7天内是否购买过商品？ | chain(xEvent、时间戳、 [答：WHAT(eventType = &quot;transaction&quot;) WHEN（&lt; 7天前）]) | 配置文件和EE[] | 布尔值 |
| 过去7天用户在体育用品上的支出最低。 | xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].min(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天内用户在体育用品上的支出最高。 | xEvent[（时间戳发生在现在之前7天）和eventType=&quot;transaction&quot;以及category=&quot;sporting goods&quot;].max(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天内每个已下载产品的下载次数（按产品索引）。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.count())) | 配置文件和EE[] | 映射[字符串，整数] |
| 过去7天内每个已下载产品下载量按产品索引的数字属性的总和。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal))) | 配置文件和EE[] | 映射[字符串，整数] 或地图[字符串，双精度] |
| 过去7天内每个已下载产品下载的平均数值属性，按产品索引。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1：** xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal)))<br/><br/>**ca2：** xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.count()))<br/><br/>**ca3：** ca2 / ca1 | 配置文件和EE[] | 映射[字符串，双精度] |
| 过去7天内每个下载产品的下载量中按产品索引的最小数值属性。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.min(commerce.order.priceTotal))) | 配置文件和EE[] | 映射[字符串，整数] 或地图[字符串，双精度] |
| 过去7天内每个已下载产品的最大下载数值属性（按产品索引）。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.max(commerce.order.priceTotal))) | 配置文件和EE[] | 映射[字符串，整数] 或地图[字符串，双精度] |
| 配置文件上的数值表达式，不引用事件。 | if(person.gender = &quot;female&quot;， 60， 65) | 配置文件 | 整数或双精度 |
| 配置文件上的布尔表达式，不引用事件。 | person.birthYear >= 2000 | 配置文件 | 布尔值 |
| 配置文件上的字符串表达式，不引用事件。 | if(homeAddress.countryCode in [&quot;US&quot;、&quot;MX&quot;、&quot;CA&quot;]，“NA”，“ROW”) | 配置文件 | 字符串 |

## 批处理表达式

下表提供了仅在批处理模式下可用的查询表达式的详细信息，这意味着这些表达式当前在流模式下不可用。

| 描述 | PQL表达式 | 输入类型：<br/>配置文件或体验事件(EE)[]) | 结果类型 |
|---|---|---|---|
| 过去7天内产品下载的数字表达式总和是否超过100（按产品索引）。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal) > 100)) | 配置文件和EE[] | 映射[字符串，布尔值] |
| 过去7天内产品下载的数值表达式的平均数是否超过100（按产品索引）。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.average(commerce.order.priceTotal) > 100)) | 配置文件和EE[] | 映射[字符串，布尔值] |
| 过去7天内每个已下载产品的各种量度累积，按产品索引。 | xEvent[（时间戳早于现在的7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， {&quot;count&quot;： G.count()， &quot;sum&quot;： G.sum(commerce.order.priceTotal)}) | 配置文件和EE[] | 映射[字符串，对象] 其中，对象是自定义XDM类型 |
