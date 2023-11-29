---
keywords: Experience Platform；查询服务；查询服务；嵌套数据结构；嵌套数据；拼合；拼合嵌套数据；
title: 拼合嵌套数据结构以用于BI工具
description: 本文档介绍在将第三方BI工具与查询服务结合使用时，如何在会话期间拼合所有表和视图的XDM架构。
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 拼合嵌套数据结构以用于第三方BI工具

Adobe Experience Platform查询服务支持 `FLATTEN` 设置。 此功能可拼合第三方BI工具中的嵌套数据结构，以提高其可用性并减少检索、分析、转换和报告数据所需的工作量。

许多BI工具如 [!DNL Tableau] 和 [!DNL Power BI] 本身不支持嵌套数据结构。 此 `FLATTEN` 设置删除了在数据上创建SQL视图以提供平面版本或使用查询服务的需要 `CTAS` 或 `INSERT INTO` 使用临时架构时将数据集复制到平面版本的作业。

此 `FLATTEN` 设置可将每个叶字段的结构提取到表的根中，并在原始命名空间之后命名该字段。 这允许您使用点表示法将字段与其体验数据模型(XDM)路径进行匹配，同时保留字段的上下文。

## 先决条件

使用 `FLATTEN` 设置要求您实际了解Adobe Experience Platform的以下组件：

* [XDM系统](../../xdm/home.md)：XDM及其在Experience Platform中实现的高级概述。

   * [创建临时架构](../../xdm/tutorials/ad-hoc.md)：XDM架构及其字段被命名为仅供单个数据集使用，称为临时架构。 临时架构用于各种数据摄取工作流中，用于Experience Platform和创建特定类型的源连接。

* [沙盒](../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

* [嵌套数据结构](./nested-data-structures.md)：本文档提供了如何使用复杂数据类型（包括嵌套数据结构）创建、处理或转换数据集的示例。

## 使用FLATTEN设置连接到数据库 {#connect-with-flatten}

此 `FLATTEN` 设置将嵌套数据结构拼合到单独的列中，其中属性名称成为保存行值的列名称。 在不支持嵌套数据结构的BI工具中处理数据时，此设置提高了临时架构的可用性并减少了必要的工作量。

使用您选择的第三方客户端连接到查询服务时，请附加 `FLATTEN` 设置为数据库名称。 有关如何连接特定BI工具的信息，请参阅 [将客户端连接到查询服务概述](../clients/overview.md). 连接字符串应包含：

* 沙盒名称。
* 冒号后跟 `all` 或特定数据集ID、视图ID或数据库名称。
* 问号(？) 后面是 `FLATTEN` 关键字。

输入内容应采用以下格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

连接字符串示例可能如下所示：

```terminal
prod:all?FLATTEN
```

## 示例 {#example}

本指南中使用的示例架构采用标准字段组 [!UICONTROL 商业详细信息]，利用 `commerce` 对象结构和 `productListItems` 数组。 请参阅XDM文档，了解 [欲知关于 [!UICONTROL 商业详细信息] 字段组](../../xdm/field-groups/event/commerce-details.md). 架构结构的表示形式可以在下图中看到。

![商务详细信息字段组的架构图，包括 `commerce` 和 `productListItems` 结构。](../images/essential-concepts/commerce-details.png)

如果BI工具不支持嵌套数据结构，则当嵌套字段包含序列化值(例如 `commerce` 和 `productListItems` （例如，在示例架构中）。 这些值可能显示为单个编码的一部分 `commerce` 字符串字段和并非实际不可用。

以下值表示 `commerce.order.priceTotal` (3018.0)， `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180)，和 `commerce.purchases.value`(1.0)在嵌套字段格式不正确。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

通过使用 `FLATTEN` 设置时，可以使用点表示法及其原始路径名访问架构内的单独字段或嵌套数据结构的整个部分。 此格式的示例，使用 `commerce` 字段组如下所示。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

此 `FLATTEN` 设置在处理其他数据结构时有一定的限制。 欲知详情，请参见 [限制部分](#limitations).

### 为查询中的字段使用引号 {#quotation-marks}

扁平化的根字段现在使用点表示法来匹配其XDM路径。 在查询中使用时，字段需要用引号(“ ”)括起来。

下面的SQL示例显示了嵌套查询的原始状态：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用拼合数据字段时，使用点表示法编写查询并将其括在引号中，如下所示：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

此 `FLATTEN` 设置当前不会拼合以下数据结构：

| 数据结构 | 限制 |
|---|---|
| 数组 | 使用显式数组索引或 `EXPLODE` 函数以访问数组。 |
| 地图 | 使用字符串键访问映射下的值以访问映射。 |

要解决Map和Array的限制，您需要使用BI工具原始SQL编辑，如Power BI中的“高级选项” — > SQL语句。

需要使用BI工具（如原始SQL编辑）来解决映射和数组限制。 请参阅有关如何执行操作的指南 [使用Power BI高级选项输入自定义SQL查询](../clients/power-bi.md#import-tables-using-custom-sql) 在SQL语句部分中。

## 后续步骤

本文档介绍了如何拼合嵌套数据结构以用于第三方BI工具。 如果您尚未连接客户端，请参阅 [客户端连接概述](../clients/overview.md) 以获取支持的第三方客户端列表。
