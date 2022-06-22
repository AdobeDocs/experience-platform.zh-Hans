---
keywords: Experience Platform；查询服务；查询服务；嵌套数据结构；嵌套数据；扁平化；扁平化嵌套数据；
title: 扁平化嵌套数据结构以与BI工具一起使用
description: 本文档介绍在查询服务中使用第三方BI工具时，如何在会话期间扁平化所有表和视图的XDM模式。
source-git-commit: 3c9a1f552760b34bfb2c4246382fcb2d66e563d0
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# 扁平化嵌套数据结构以与第三方BI工具一起使用

Adobe Experience Platform查询服务支持 `FLATTEN` 通过第三方BI工具连接到数据库时进行设置。 此功能可拼合第三方BI工具中的嵌套数据结构，以提高其可用性，并减少检索、分析、转换和报告数据所需的工作量。

许多BI工具，如 [!DNL Tableau] 和 [!DNL Power BI] 本身不支持嵌套的数据结构。 的 `FLATTEN` 设置消除了在数据上创建SQL视图以提供平面版本或使用查询服务的需要 `CTAS` 或 `INSERT INTO` 使用临时模式时，将数据集复制到平面版本的作业。

的 `FLATTEN` 设置会将每个叶字段的结构提取到表的根中，并将字段命名为原始命名空间之后的字段。 这允许您使用点表示法将字段与其体验数据模型(XDM)路径匹配，同时保留字段的上下文。

## 先决条件

使用 `FLATTEN` 设置需要对Adobe Experience Platform的以下组件有一定的了解：

* [XDM系统](../../xdm/home.md):XDM及其在Experience Platform中实施的高级概述。

   * [创建临时架构](../../xdm/tutorials/ad-hoc.md):XDM架构（其字段名称仅由单个数据集使用）称为临时架构。 Ad hoc架构用于各种数据摄取工作流，用于Experience Platform和创建特定类型的源连接。

* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

* [嵌套的数据结构](./nested-data-structures.md):本文档提供了有关如何创建、处理或转换具有复杂数据类型（包括嵌套数据结构）的数据集的示例。

## 使用FLATTEN设置连接到数据库 {#connect-with-flatten}

的 `FLATTEN` 设置会将嵌套数据结构拼合到单独的列中，其中属性名称将变为保存行值的列名称。 当在不支持嵌套数据结构的BI工具中处理数据时，此设置可提高临时架构的可用性并减少必要的工作量。

使用所选的第三方客户端连接到查询服务时，请附加 `FLATTEN` 设置为数据库名称。 有关如何连接特定BI工具的信息，请参阅 [将客户端连接到查询服务概述](../clients/overview.md). 连接字符串应包含：

* 沙盒名称。
* 冒号后跟 `all` 或特定数据集ID、视图ID或数据库名称。
* 问号(?) 后跟 `FLATTEN` 关键词。

输入应采用以下格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

连接字符串示例如下所示：

```terminal
prod:all?FLATTEN
```

## 示例 {#example}

本指南中使用的示例架构采用标准字段组 [!UICONTROL 商务详细信息]，利用 `commerce` 对象结构和 `productListItems` 数组。 有关 [有关 [!UICONTROL 商务详细信息] 字段组](../../xdm/field-groups/event/commerce-details.md). 架构结构的表示形式可在下图中查看。

![商务详细信息字段组的架构图，包括 `commerce` 和 `productListItems` 结构。](../images/best-practices/final-subscription-schema.png)

如果BI工具不支持嵌套数据结构，则当嵌套字段包含序列化值(例如 `commerce` 和 `productListItems` （在示例架构中）。 这些值可能显示为单个编码的一部分 `commerce` 字符串字段，不会实际无法使用。

以下值表示 `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180)和 `commerce.purchases.value`(1.0)。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

通过使用 `FLATTEN` 设置后，您可以使用点表示法及其原始路径名访问架构或嵌套数据结构整个部分中的单独字段。 此格式的示例使用 `commerce` 字段组如下所示。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

的 `FLATTEN` 设置在处理其他数据结构时存在一些限制。 有关详细信息，请参阅 [限制部分](#limitations).

### 在查询中对字段使用引号 {#quotation-marks}

扁平化根字段现在使用点表示法来匹配其XDM路径。 在查询中使用时，需要将字段用引号(&quot; &quot;)括起来。

以下SQL示例显示嵌套查询的原始状态：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用扁平化数据字段时，查询使用点表示法编写，并用引号括起来，如下所示：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

的 `FLATTEN` 设置当前不会扁平化以下数据结构：

| 数据结构 | 限制 |
|---|---|
| 数组 | 使用显式数组索引或 `EXPLODE` 函数访问数组。 |
| 地图 | 使用字符串键访问映射下的值以访问映射。 |

要同时解决映射和数组限制，您需要使用BI工具原始SQL编辑，如Power BI中的Advanced Options -> SQL语句。

要解决映射和数组限制，必须使用诸如原始SQL编辑之类的BI工具。 请参阅指南以了解操作方法 [使用Power BI高级选项输入自定义SQL查询](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) 在SQL语句部分中。

## 后续步骤

本文档介绍了如何扁平化嵌套数据结构以与第三方BI工具一起使用。 如果您尚未连接客户端，请参阅 [客户端连接概述](../clients/overview.md) ，以获取受支持的第三方客户的列表。
