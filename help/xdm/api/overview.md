---
keywords: Experience Platform；主题；热门主题；api;API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；
solution: Experience Platform
title: 模式注册表API指南
description: 模式 Registry API允许开发人员有计划地管理Adobe Experience Platform中的所有模式和相关的Experience Data Model(XDM)资源。 请按照本指南学习如何使用API执行关键操作。
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# [!DNL Schema Registry] API指南

[!DNL Schema Registry]用于访问Adobe Experience Platform中的模式库，提供可从中访问所有可用库资源的用户界面和RESTful API。

模式 Registry API提供了多个端点，允许您通过编程方式管理平台内可用的所有模式和相关的Experience Data Model(XDM)资源。 这包括由Adobe、[!DNL Experience Platform]合作伙伴以及您使用其应用程序的供应商定义的应用程序。

以下概述了这些端点。 请访问各个端点指南以了解详细信息，并参阅[快速入门指南](./getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

>[!IMPORTANT]
>
>XDM使用JSON模式格式描述和验证所摄取的客户体验数据的结构。 在使用模式注册表API之前，强烈建议您查看[官方JSON模式文档](https://json-schema.org/)，以便更好地了解此基础技术。

要视图所有可用的端点和CRUD操作，请访问[模式注册表API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 模式 (Schema)

XDM模式表示并验证引入平台的数据的结构和格式。 模式由类和零个或多个模式字段组组成。 您可以使用`/schemas`端点创建、视图、编辑和删除模式。 要了解如何使用此端点，请参阅[模式端点指南](./schemas.md)。

有关如何在模式 Registry API中创建完整模式（包括创建和添加字段组和数据类型）的分步指南，请参阅[API模式创建教程](../tutorials/create-schema-api.md)。

## 行为

行为定义模式描述的数据的性质。 每个XDM类必须引用特定行为，使用该类的所有模式都将继承该行为。 请参阅[行为端点指南](./behaviors.md)，了解如何视图API中的可用行为。

## 类

类定义基于该类的所有模式必须包含的公用属性的基结构，并确定哪些字段组有资格在这些模式中使用。 每个类都必须与现有行为关联。 有关在API中使用类的详细信息，请参见[类终结点指南](./classes.md)。

## 字段组

字段组是可重用的组件，它们定义一个或多个表示特定概念的字段，如个人、邮寄地址或Web浏览器环境。 字段组将作为实现兼容类的模式的一部分包括，具体取决于它们所表示的数据（记录或时间序列）的行为。 请参阅[字段组端点指南](./field-groups.md)，了解如何使用API中的字段组。

## 数据类型

数据类型在类或字段组中用作引用类型字段的方式与基本文本字段相同，关键区别在于数据类型可以定义多个子字段。 虽然与字段组中允许一致使用多字段结构的字段组类似，但数据类型更灵活，因为它们可以包含在模式结构中的任意位置，而字段组只能添加在根级别。 有关在API中使用数据类型的详细信息，请参阅[数据类型终结点指南](./data-types.md)。

## 描述符

描述符是指分配给模式中特定字段的元数据集，提供各种上下文详细信息，包括这些字段(以及模式本身)如何与其他模式相关。 每个模式可以应用一个或多个描述符实体，并且存在多种不同的描述符类型以用于不同的用途。 有关在API中使用描述符的详细信息，请参阅[描述符端点指南](./descriptors.md)，以及不同描述符类型及其用例的概述。

## 合并

平台允许您为特定用例编写模式，还允许您编写属于特定类的模式的“合并”。 合并模式将共享同一类的所有模式的字段聚合为单个表示形式。 通过启用与[实时客户用户档案](../../profile/home.md)一起使用的模式，该模式将包含在其特定类的合并中。 因此，合并模式不能直接编辑，并且只能受包含或排除在用户档案中使用的模式的影响。

要了解如何在模式 Registry API中视图合并，请参阅[合并端点指南](./unions.md)。

## 导出/导入

模式注册表API允许您在沙箱和IMS组织之间传输和共享XDM资源。 对于任何模式、字段组或数据类型，您可以生成包含资源结构和任何从属资源的导出有效负荷。 然后，此有效负荷可用于将资源导入目标沙箱和IMS组织。

有关如何使用这些端点的详细信息，请参阅[导出/导入端点指南](./export-import.md)。

## 样本数据

您可以为模式库中的任何指定模式生成示例数据。 返回的响应对象随后可用作数据摄取源。

有关使用此端点的详细信息，请参见[示例数据端点指南](./sample-data.md)。

## 审核日志

模式注册表会维护一个日志，其中包含在不同更新之间对某个资源(类、字段组、数据类型或模式)所做的所有更改。 您可以通过在到此端点的GET请求路径中提供特定资源的`$id`或`meta:altId`来检索该日志。

有关使用此端点的详细信息，请参阅[审核日志端点指南](./audit-log.md)。

## 后续步骤

要开始使用模式 Registry API进行调用，请阅读[快速入门指南](./getting-started.md)，然后选择一个端点指南以了解如何使用特定端点。
