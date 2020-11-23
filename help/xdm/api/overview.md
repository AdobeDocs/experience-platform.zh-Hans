---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: 模式注册表API开发人员指南
description: '模式注册表API允许您以编程方式管理Experience Platform中可用的所有模式和相关XDM资源。 '
topic: developer guide
translation-type: tm+mt
source-git-commit: d0e5865fddcf2592e9b6d8d4b2747bdceee6bda7
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# [!DNL Schema Registry] API开发人员指南

该 [!DNL Schema Registry] 库用于访问Adobe Experience Platform的模式库，提供可访问所有可用库资源的用户界面和RESTful API。

模式注册表API提供多个端点，允许您以编程方式管理平台内可用的所有模式和相关的体验数据模型(XDM)资源。 这包括由Adobe、合作伙伴和您使 [!DNL Experience Platform] 用其应用程序的供应商定义的应用程序。

这些端点概述如下。 请访问各个端点指南获取详细信息，并参 [阅入门指南](./getting-started.md) ，获取有关所需标头、读取示例API调用等的重要信息。

>[!IMPORTANT]
>
>XDM使用JSON模式格式描述和验证所摄取的客户体验数据的结构。 在使用模式注册表API之前，强烈建议您查看官方的JSON [模式文档](https://json-schema.org/) ，以更好地了解此基础技术。

要视图所有可用端点和CRUD操作，请访问 [模式注册表API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 模式

XDM模式表示并验证引入平台的数据的结构和格式。 模式由类和零个或多个混音组成。 您可以使用端点创建、视图、编辑和删除 `/schemas` 模式。 要了解如何使用此端点，请参阅 [模式端点指南](./schemas.md)。

有关如何在模式注册表API中创建完整模式（包括创建和添加混音和数据类型）的分步指南，请参阅API [模式创建教程](../tutorials/create-schema-api.md)。

## 类

类定义模式将包含的数据的行为方面（记录或时间序列）。 此外，类确定基于该类的所有模式必须包含的公用属性的基结构。 模式的类决定哪些混音符合在该模式中使用的条件。 有关在 [API中使用类](./classes.md) ，请参阅类端点指南。

## Mixins

Mixin是可重用的组件，它们定义一个或多个表示特定概念的字段，如个人、邮寄地址或Web浏览器环境。 混音将被作为实现兼容类的模式的一部分包含在内，具体取决于它们所代表的数据的行为（记录或时间序列）。 请参阅 [mixins端点指南](./mixins.md) ，了解如何在API中使用mix。

## 数据类型

数据类型在类或混合中用作引用类型字段的方式与基本文本字段相同，关键区别在于数据类型可以定义多个子字段。 虽然与混音类似，它们允许多字段结构的一致使用，但数据类型更灵活，因为它们可以包含在模式结构中的任何位置，而混音只能添加在根级别。 有关在 [API中使用数据类型](./data-types.md) ，请参阅数据类型端点指南。

## 描述符

描述符是指在模式中分配特定字段的元数据集，提供各种上下文详细信息，包括这些字段(和模式本身)如何与其他模式相关。 每个模式可以应用一个或多个描述符实体，并且有几种不同的描述符类型用于不同的用途。 有关在 [API中使用描述符](./descriptors.md) 的更多信息，请参阅描述符端点指南，以及不同描述符类型及其用例的概述。

## 合并

平台允许您为特定用例创建模式，也允许您构建属于特定类的模式的“合并”。 合并模式将共享同一类的所有模式的字段聚合为单一表示形式。 通过启用模式以与实 [时客户用户档案一起使用](../../profile/home.md)，该模式将包含在其特定类的合并中。 因此，合并模式不能直接进行编辑，并且只能受包含或排除用于用户档案的模式的影响。

要了解如何在视图注册表API中模式合并，请参阅 [合并端点指南](./unions.md)。

## 导出／导入

模式注册表API允许您在沙箱和IMS组织之间传输和共享XDM资源。 对于任何模式、混音或数据类型，您可以生成包含资源结构和任何从属资源的导出有效负荷。 然后，此有效负荷可用于将资源导入目标沙箱和IMS组织。

有关此 [端点的使用](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，请参阅模式注册表API参考。

## 样本数据

您可以为模式库中的任何指定模式生成示例数据。 返回的响应对象随后可用作数据获取源。

有关此 [端点的使用](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，请参阅模式注册表API参考。

## 审核日志

模式注册表会维护一个日志，其中列出了在不同更新之间对资源(类、混合、数据类型或模式)所做的所有更改。 您可以通过提供特定资源的日志或在GET请求 `$id` 到此 `meta:altId` 端点的路径中检索其日志。

有关此 [端点的使用](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) ，请参阅模式注册表API参考。

## 后续步骤

要开始使用模式注册表API进行调用，请阅读 [入门指南](./getting-started.md) ，然后选择一个端点指南来了解如何使用特定端点。