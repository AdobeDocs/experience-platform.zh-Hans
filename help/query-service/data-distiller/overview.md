---
title: 数据Distiller概述
description: 与您的授权许可相关的查询服务数据的Distiller使用限制摘要。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 数据Distiller概述

Data Distiller是一款产品包，其中包含Adobe Experience Platform功能的子集。 借助Data Distiller，您可以通过在查询服务中执行批量查询，为实时客户资料或分析用例执行摄取后数据准备（例如清理、整形和操作）。 您对Data Distiller的使用取决于您当前和持续至少拥有以下一项许可证：Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer。

## 许可证使用情况 {#licence-usage}

请参阅 [数据Distiller许可证使用文档](./licence-usage.md) 查看有关贵组织查询服务许可证使用情况的重要信息。

## 范围参数 {#scoping-parameters}

范围界定参数是与根据您的许可证容量定义的建议用例范围界定相关的使用限制。 如果没有附加组件，Data Distiller的范围界定参数如下所示：

* **计算小时数**:您可以使用PSQL或查询服务API来运行在任何沙盒（已计划或其他）中执行的批处理查询，以扫描和写入数据。 它使用您在许可协议的范围界定过程中确定的每年分配的计算小时数。 所有沙盒的总计算小时数都会累计。
* **摄取的数据**:摄取到Adobe Experience Platform中且可使用Data Distiller查询的数据受当前Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer许可证中所述的限制。
* **数据湖存储**:在您当前为Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer提供的许可证中提供的数据湖存储也可以与Data Distiller一起使用。 数据湖存储是一项共享功能。
* **查询服务用户**:在您当前对Adobe Real-time Customer Data Platform、Customer Journey Analytics和/或Adobe Journey Optimizer的许可证中详细列出的查询服务用户数，也可以与Data Distiller一起使用。 查询服务用户是一项共享功能。

## 护栏

请参阅 [查询服务护栏](../guardrails.md) 有关与您的许可授权相关的查询服务数据的默认使用限制的文档。

## 静态限制

静态限制是与Adobe Experience Platform激活的功能边界相关的使用限制。 [有关Adobe Experience Platform激活的更多信息](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) 可在Adobe帮助文档中找到。 下面列出了数据Distiller静态限制的摘要，有关更完整的信息，请参阅查询服务护栏文档。

* **批量查询**:计划的批处理查询在24小时后超时。
* **查询服务**:您可以使用查询服务实现以下目的：
   * 要运行SQL查询以进行数据分析，并进行摄取数据准备（清理、整形和操作）之后。
   * 要运行SQL查询以创建汇总量度以直接显示到BI工具中，请执行以下操作：
   * 在Adobe Experience Platform中快速检查数据。
* **报表API调用**:要确保使用报表API对聚合数据运行查询，有足够的资源来高效执行。 这包括可增强现有数据模型(例如Real-time Customer Data Platform提供的数据模型)的查询。 报表API通过为每个查询分配并发插槽来跟踪资源利用率。 最多可同时使用4个报表API调用。 如果您通过BI工具访问报表API，并且需要更多并发插槽，则需要BI服务器。


