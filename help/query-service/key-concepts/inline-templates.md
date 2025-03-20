---
title: 内联模板
description: 了解如何使用内联模板在众多查询中重用多个条件。
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: ef4c7f20710f56ca0de7c0dfdb99751ff2fe8ebe
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 内联模板

内联模板允许您在多个查询中重用多个条件。 您可以将标准保存在模板中，然后在多个查询中重复使用。 可重用的SQL模板减少了开发工作，也减少了在查询之间复制长语句所带来的错误风险。 使用内联模板，您可以在一个位置进行更改，并使这些更改反映在引用此模板的任何查询中。

本文档介绍查询编辑器中内联模板的使用和限制。

## 先决条件

UI和查询服务API都支持内联模板。 在继续本指南之前，请阅读有关如何[通过API](../api/query-templates.md#create-a-query-template)或使用[查询编辑器](../ui/user-guide.md#query-authoring)创建查询模板的文档。

## 内联模板语法 {#syntax}

保存查询后，即称为模板。 当模板引用语句中的另一个模板时，称为内联模板。 在SQL中，使用模板名称后跟哈希符号(#)表示内联模板。 此语法的示例为`#YOUR_TEMPLATE_NAME`。

## 用例 {#use-case}

以下SQL模板演示了内联模板的效用，并以一个示例说明了如何计算在2023年6月之前订购的支出超过“最大收入”的任何地区的美国客户数量。 内联模板的优点在于，您可以轻松编辑子模板（在本例中是最大收入和订单日期），而无需更改父模板。

**示例**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

在执行查询时，查询服务将从散列符号开始的模板名称替换为命名模板的SQL语句。

>[!NOTE]
>
>查询模板可以调用任意数量的其他内联模板。 对于可从单个查询调用的内联模板的数量没有限制。 模板也可以嵌套在其他内联模板中。

您可以使用模板存储一个或多个条件。 它们本身不需要是完整的查询。 如果模板包含有效的查询，则只需调用前面带有散列符号的模板名称即可执行查询。 例如，如果您将`SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;`存储为名为`JUNE_2023_LOYALTY_MEMBERS`的模板，则命令`#JUNE_2023_LOYALTY_MEMBERS;`将执行模板中包含的有效查询。

>[!NOTE]
>
>在Adobe Experience Platform UI中，仅在父级别支持参数化查询形式的内联模板。 这意味着参数化查询仅在原始模板中使用时才有效。 子模板必须是静态模板，不能具有动态参数。 有关详细信息，请参阅[参数化查询文档](../ui/parameterized-queries.md)。

## 后续步骤

阅读本文档后，您现在知道如何在查询编辑器中或通过查询服务API引用SQL中的其他模板。

此外，您应该阅读[匿名块指南](./anonymous-block.md)，该指南说明了如何通过链接按顺序执行的一个或多个SQL语句来最大限度地减少开发开销。
