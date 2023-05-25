---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；
solution: Experience Platform
title: 架构注册表API指南
description: 架构注册表API允许开发人员以编程方式管理Adobe Experience Platform中的所有架构和相关的Experience Data Model (XDM)资源。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 2%

---

# [!DNL Schema Registry] API指南

此 [!DNL Schema Registry] 用于访问Adobe Experience Platform中的Schema Library，提供一个用户界面和RESTful API，所有可用库资源都可从该API访问。

架构注册表API提供了多个端点，允许您以编程方式管理Platform中所有可用的架构和相关体验数据模型(XDM)资源。 这包括由Adobe定义的规则、 [!DNL Experience Platform] 合作伙伴，以及您使用其应用程序的供应商。

这些端点概述如下。 有关详细信息，请访问各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

>[!IMPORTANT]
>
>XDM使用JSON架构格式来描述和验证所摄取的客户体验数据的结构。 在使用Schema Registry API之前，强烈建议您查看 [官方JSON架构文档](https://json-schema.org/) 以更好地了解这一基础技术。

要查看所有可用的端点和CRUD操作，请访问 [架构注册表API参考](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 架构

XDM架构表示和验证引入到Platform中的数据结构和格式。 架构由一个类以及零个或多个架构字段组组成。 您可以使用创建、查看、编辑和删除架构。 `/schemas` 端点。 要了解如何使用此端点，请参阅 [架构端点指南](./schemas.md).

有关如何在Schema Registry API中手动创建完整模式（包括创建和添加字段组和数据类型）的分步指南，请参阅 [API架构创建教程](../tutorials/create-schema-api.md).

如果您正在摄取CSV数据，请参阅 [CSV到架构的转换](#csv-to-schema).

## 行为

行为定义架构描述的数据的性质。 每个XDM类都必须引用一个特定行为，使用该类的所有架构都将继承该行为。 请参阅 [行为端点指南](./behaviors.md) 以了解如何在API中查看可用行为。

## 类

类定义基于该类的所有架构都必须包含的公共属性的基本结构，并确定哪些字段组适合在这些架构中使用。 每个类都必须与现有行为关联。 请参阅 [类端点指南](./classes.md) 有关在API中使用类的详细信息。

## 字段组

字段组是可重复使用的组件，它们定义表示特定概念的一个或多个字段，例如个人、邮寄地址或Web浏览器环境。 字段组旨在作为实现兼容类的架构的一部分包含，具体取决于它们表示的数据的行为（记录或时间序列）。 请参阅 [字段组端点指南](./field-groups.md) 了解如何在API中使用字段组。

## 数据类型

数据类型在类或字段组中用作引用类型字段的方式与基本文本字段相同，主要区别在于数据类型可以定义多个子字段。 虽然与字段组类似，因为它们允许一致地使用多字段结构，但数据类型更灵活，因为它们可以包含在架构结构中的任意位置，而字段组只能在根级别添加。 请参阅 [数据类型端点指南](./data-types.md) 有关在API中使用数据类型的更多信息。

## 描述符

描述符是分配给架构中特定字段的元数据集，提供各种上下文详细信息，包括这些字段（以及架构本身）如何与其他架构相关联。 每个架构可以应用一个或多个描述符实体，并且有多个不同的描述符类型用于不同的目的。 请参阅 [描述符端点指南](./descriptors.md) 有关在API中使用描述符的更多信息，以及不同描述符类型及其用例的概述。

## 联合

虽然Platform允许您为特定用例编写架构，但它还允许您编写属于特定类的架构的“联合”。 合并架构将共享同一类的所有架构的字段聚合到单个表示中。 启用架构以用于 [Real-time Customer Profile](../../profile/home.md)，则该架构将包含在其特定类的合并中。 因此，不能直接编辑合并架构，并且只能受包含或排除配置文件中使用的架构的影响。

要了解如何在架构注册表API中查看联合，请参阅 [合并端点指南](./unions.md).

## CSV到架构的转换 {#csv-to-schema}

您可以使用CSV文件作为模板自动生成XDM架构，从而创建模板以批量导入架构字段并减少手动API或UI工作。

请参阅 [CSV到架构转换端点指南](./export.md) 了解更多信息。

>[!NOTE]
>
>您还可以将UI用于 [使用人工智能生成的推荐将CSV映射到架构](../../ingestion/tutorials/map-csv/recommendations.md) （当前为测试版）。

## 导出 {#export}

架构注册表API允许您在沙盒和组织之间传输和共享XDM资源。 对于任何架构、字段组或数据类型，可生成包含资源结构和任何依赖资源的导出有效负载。 然后，可使用此有效负载将资源导入目标沙盒和组织。

请参阅 [导出端点指南](./export.md) 有关如何为现有XDM资源创建导出有效负载的更多信息。

## 导入

如果您使用 [导出](#export) 或 [CSV到架构的转换](./import.md) 端点要创建导出有效负载，您可以将该有效负载发送到目标组织和沙盒以导入指定的资源。

请参阅 [导入端点指南](./export.md) 有关如何从导出有效负载生成XDM资源的更多信息。

## 示例数据

您可以为架构库中的任何指定架构生成示例数据。 然后，返回的响应对象可用作数据摄取的源。

请参阅 [示例数据端点指南](./sample-data.md) 有关使用此端点的更多信息。

## 审核日志

架构注册表维护在不同更新之间对资源（类、字段组、数据类型或架构）发生的所有更改的日志。 您可以通过提供特定资源的日志来检索该资源 `$id` 或 `meta:altId` 在此端点的GET请求路径中。

请参阅 [审核日志端点指南](./audit-log.md) 有关使用此端点的更多信息。

## 后续步骤

要使用Schema Registry API开始调用，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
