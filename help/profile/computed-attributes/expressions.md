---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 计算属性的PQL表达式示例
type: Documentation
description: 计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数需要使用有效的配置文件查询语言(PQL)表达式。 本指南概述了计算属性的一些最常用的PQL表达式。
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha)计算属性的PQL表达式示例

>[!IMPORTANT]
>
>计算属性功能当前位于Alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

在Adobe Experience Platform中，计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数会自动计算，以便在分段、激活和个性化期间使用。 每个计算属性都由基本信息来定义，如名称和描述、用于保存值的字段的架构类和路径，以及要存储在计算属性中的值的表达式。

在计算属性中使用的表达式是使用 [!DNL Profile Query Language] (PQL)，一种符合Experience Data Model(XDM)规范的查询语言，旨在支持实时客户资料数据查询的定义和执行。

计算属性当前支持以下函数：sum、count、min、max和boolean。 本指南概述了在为组织定义自己的计算属性时可以使用的一些最常用的PQL表达式。 有关PQL的更多信息以及指向其他格式准则和支持查询示例的链接，请访问 [PQL概述](../../segmentation/pql/overview.md).

## 流表达式

下表提供了在流模式下支持的常用查询表达式的详细信息。

| 描述 | PQL表达式 | 输入类型：<br/>用户档案或体验事件(EE)[]) | 结果类型 |
|---|---|---|---|
| 过去7天内图像下载次数。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;和contentType = &quot;image&quot;].count() | 配置文件和EE[] | 整数 |
| 过去7天内客户在体育用品上花费的总和。 | xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天内顾客平均花在体育用品上。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1:** xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | 配置文件和EE[] | 双精度 |
| 客户过去7天在体育用品上花了100美元以上吗？<br/><br/>**注意：** 需要创建两个计算属性。 | **ca1:** xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | 配置文件和EE[] | 布尔型 |
| 客户在过去7天内购买过吗？ | chain(xEvent， timestamp， [答：WHAT(eventType = &quot;transaction&quot;)WHEN（&lt; 7天前）]) | 配置文件和EE[] | 布尔型 |
| 过去7天中，用户在体育用品上花费的最低。 | xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天中，用户在体育用品上花费的最高。 | xEvent[（时间戳发生时间早于7天），eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | 配置文件和EE[] | 整数或双精度 |
| 过去7天内按产品编入索引的每个下载产品的下载次数计数。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.count())) | 配置文件和EE[] | 地图[字符串，整数] |
| 过去7天内每个下载产品下载次数中按产品编入索引的数值属性总和。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal))) | 配置文件和EE[] | 地图[字符串，整数] 或地图[字符串，双精度类型] |
| 过去7天内每个下载产品下载次数中按产品编入索引的平均值。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1:** xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.count()))<br/><br/>**ca3:** ca2 / ca1 | 配置文件和EE[] | 地图[字符串，双精度类型] |
| 过去7天内每个下载产品下载次数中按产品编入索引的最小数值属性数。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.min(commerce.order.priceTotal))) | 配置文件和EE[] | 地图[字符串，整数] 或地图[字符串，双精度类型] |
| 过去7天内每个下载产品下载次数中按产品编入索引的最大数值属性数。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.max(commerce.order.priceTotal))) | 配置文件和EE[] | 地图[字符串，整数] 或地图[字符串，双精度类型] |
| 配置文件上的数字表达式，不引用事件。 | if(person.gender = &quot;female&quot;, 60, 65) | 配置文件 | 整数或双精度 |
| 配置文件上的布尔表达式，不引用事件。 | person.birthYear >= 2000 | 配置文件 | 布尔型 |
| 配置文件中的字符串表达式，不是引用事件。 | if(homeAddress.countryCode in [&quot;US&quot;、&quot;MX&quot;、&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 配置文件 | 字符串 |

## 批处理表达式

下表提供了仅在批处理模式下可用的查询表达式的详细信息，这意味着它们当前在流模式下不可用。

| 描述 | PQL表达式 | 输入类型：<br/>用户档案或体验事件(EE)[]) | 结果类型 |
|---|---|---|---|
| 过去7天内产品下载次数中数字表达式的总和是否超过100（按产品编入索引）。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal)> 100) | 配置文件和EE[] | 地图[字符串，布尔值] |
| 过去7天内产品下载次数中数字表达式的平均值是否超过100（按产品编入索引）。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.average(commerce.order.priceTotal)> 100) | 配置文件和EE[] | 地图[字符串，布尔值] |
| 过去7天内每个下载产品的各种量度的累积，已按产品建立索引。 | xEvent[（时间戳发生时间早于7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， {&quot;count&quot;:G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal)}) | 配置文件和EE[] | 地图[字符串，对象] 其中，对象是自定义XDM类型 |
