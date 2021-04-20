---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 计算属性的PQL表达式示例
topic: guide
type: Documentation
description: 计算属性是用于将事件级数据聚合为用户档案级属性的函数。 这些函数需要使用有效的用户档案查询语言(PQL)表达式。 本指南概述了计算属性中一些最常用的PQL表达式。
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# (Alpha)计算属性的PQL表达式示例

>[!IMPORTANT]
>
>计算属性功能当前位于Alpha中，并且不适用于所有用户。 文档和功能可能会发生变化。

在Adobe Experience Platform中，计算属性是用于将事件级数据聚合为用户档案级属性的函数。 这些函数会自动计算，以便能够跨细分、激活和个性化使用。 每个计算属性都用基本信息来定义，如名称和描述、模式类和值所在字段的路径，以及表达式，其计算值是要存储在计算属性中的值。

在计算属性中使用的表达式是使用[!DNL Profile Query Language](PQL)创建的，PQL是一种符合Experience Data Model(XDM)规范的查询语言，旨在支持实时客户用户档案数据的查询的定义和执行。

计算属性当前支持以下函数：sum、count、min、max和boolean。 本指南概述了在为组织定义自己的计算属性时可以使用的一些最常用的PQL表达式。 有关PQL的详细信息以及指向其他格式指南和受支持查询示例的链接，请访问[PQL概述](../../segmentation/pql/overview.md)。

## 流表达式

下表提供了流模式中支持的常用查询表达式的详细信息。

| 描述 | PQL表达式 | 输入类型：<br/>用户档案或体验事件(EE[]) | 结果类型 |
|---|---|---|---|
| 过去7天内图像下载的计数。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;,contentType = &quot;image&quot;].count() | 用户档案和EE[] | 整数 |
| 过去7天内客户在体育用品上的支出总和。 | xEvent[（timestamp发生在&lt; 7天前），eventType=&quot;transaction&quot;和类别 = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | 用户档案和EE[] | 整数或多次 |
| 过去7天中，客户在体育用品上的平均支出。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1:** xEvent[(timestamp occurs  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(timestamp  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;><br/><br/>**** occurs.count()ca3: ca1 / ca2]] | 用户档案和EE[] | 双精度 |
| 客户过去7天在体育用品上花费了100多美元吗？<br/><br/>**注意：** 需要创建两个计算属性。 | **ca1:** xEvent[(timestamp occurs  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | 用户档案和EE[] | 布尔值 |
| 客户在最近7天内购买了吗？ | chain(xEvent， timestamp， [A:WHAT(eventType = &quot;transaction&quot;)WHEN（&lt; 7天前）]) | 用户档案和EE[] | 布尔值 |
| 过去7天里，用户在体育用品上的支出最低。 | xEvent[（timestamp发生在&lt; 7天前），eventType=&quot;transaction&quot;和类别 = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | 用户档案和EE[] | 整数或多次 |
| 过去7天里，用户在体育用品上的支出最高。 | xEvent[（timestamp发生在&lt; 7天前），eventType=&quot;transaction&quot;和类别 = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | 用户档案和EE[] | 整数或多次 |
| 最近7天内按产品编制索引的每个下载产品的下载次数。 | xEvent[（时间戳在&lt; 7天前发生）和eventType=&quot;download&quot;].groupBy(product)。map(((K， G)=> mapEntry(K， G.count())) | 用户档案和EE[] | Map[String， Integer] |
| 过去7天内按产品编制索引的每个下载产品的下载次数的数字属性总和。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal))) | 用户档案和EE[] | Map[String、Integer]或Map[String、多次] |
| 过去7天内按产品编制索引的每个下载产品的下载次数的平均值。<br/><br/>**注意：** 需要创建三个计算属性。 | **ca1:** xEvent[(timestamp occurs  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(timestamp occurs  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;><br/><br/>**** .groupBy(product)。map(K，G)=> map(K， count()))ca3:Ca2 / ca1]] | 用户档案和EE[] | Map[字符串，多次] |
| 在过去7天内，每个下载产品的下载次数中按产品编制索引的最小数字属性。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.min(commerce.order.priceTotal))) | 用户档案和EE[] | Map[String、Integer]或Map[String、多次] |
| 过去7天内，每个下载产品的下载次数中按产品编制索引的最大数值属性。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.max(commerce.order.priceTotal))) | 用户档案和EE[] | Map[String、Integer]或Map[String、多次] |
| 用户档案上的数字表达式，不是引用事件。 | if（person.geder = &quot;女性&quot;, 60, 65） | 配置文件 | 整数或多次 |
| 用户档案上的布尔表达式，而不是引用事件。 | person.birthYear >= 2000 | 配置文件 | 布尔值 |
| 用户档案上的字符串表达式，而不是引用事件。 | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 配置文件 | 字符串 |

## 批表达式

下表提供了仅在批处理模式下可用的查询表达式的详细信息，这意味着它们当前在流中不可用。

| 描述 | PQL表达式 | 输入类型：<br/>用户档案或体验事件(EE[]) | 结果类型 |
|---|---|---|---|
| 过去7天内产品下载的数字表达式总和是否超过100（按产品编制索引）。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.sum(commerce.order.priceTotal)> 100)) | 用户档案和EE[] | Map[String， Boolean] |
| 过去7天内产品下载的数字表达式平均数是否超过100（按产品编制索引）。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， G.average(commerce.order.priceTotal)> 100)) | 用户档案和EE[] | Map[String， Boolean] |
| 在过去7天内按产品编制索引的每个下载产品的各种指标的累积。 | xEvent[（timestamp发生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map((K， G)=> mapEntry(K， {&quot;count&quot;:G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal)) | 用户档案和EE[] | 映射[字符串，对象]，其中对象是自定义XDM类型 |