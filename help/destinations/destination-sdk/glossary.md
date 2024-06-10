---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK术语表
description: 了解使用Experience PlatformDestination SDK创作目标时的重要术语。
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---


# Adobe Experience Platform Destination SDK术语表

有关Destination SDK中使用的术语的定义，请参阅此术语表。 有关其他Adobe Experience Platform术语，请参阅 [Experience Platform术语表](/help/landing/glossary.md).

## A

**聚合策略**：在配置应如何将数据导出到实时流目标时，您可以定义在将数据发送到目标平台之前如何聚合配置文件数据。 这有助于通过根据特定标准对数据记录进行分组、降低API调用的频率并提高整体效率来优化数据交付。 可以配置不同的策略以满足各种目标要求，从而确保以最有效的方式打包和交付数据。 [了解详情](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md)。

**受众元数据配置**：受众元数据配置是指在Adobe Experience Platform中定义的结构化设置和参数，这些设置和参数支持以编程方式创建、更新和删除指定目标中的受众区段。 此配置利用受众元数据模板，以符合目标平台的营销API的规范。 详细了解 [受众元数据配置](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) 和 [可用的宏](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**目标配置端点**：Adobe Experience Platform中的目标配置端点，特别是 `/authoring/destinations` API端点用于创建、检索、更新和删除目标的配置。 这些配置定义如何将来自Adobe Experience Platform的数据传递到各种外部系统或目标，如营销平台、云存储服务或其他数据处理端点。 详细了解 [可用的配置选项](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) 并查看 [参考文档](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**目标实例**：Adobe Experience Platform中目标配置的特定设置，通过Experience PlatformUI创建和管理。 它包括用于连接数据并将数据发送到目标的所有必要参数和凭据。 建立与目标的连接后，您可以在以下情况下获取目标实例ID： [浏览与目标的连接](/help/destinations/ui/destination-details-page.md).

![用户界面图像如何获取目标实例ID](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]模板**：A [!DNL Pebble] 模板用于将从Adobe Experience Platform导出的数据转换为目标平台所需的格式。 它采用 [!DNL Pebble] 模板化语言，允许通过如下函数进行动态数据转换 `filter`， `for`， `if`、和 `set`. Adobe Experience Platform包含其他自定义函数，如 `addedSegments` 和 `removedSegments`. 这些模板有助于设置数据元素（如时间戳和受众成员资格）的格式，以满足目标的规范。 了解详情 [此处](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) 和 [此处](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**专用目标**：各个Adobe Experience Platform客户创建的自定义集成。 这些应用程序专为满足特定的业务需求而定制，并且只能在客户的组织内访问，在数据导出配置方面提供了灵活性。 私有目标仅适用于Real-Time CDP Ultimate客户。 [了解详情](/help/destinations/destination-sdk/overview.md#productized-custom-integrations)。

**公共目标**：Adobe Experience Platform目录中的公开可用集成。 这些目标实现了标准化、品牌化，并通过提供预配置的参数简化了客户设置。 所有使用Adobe Experience Platform的客户都可以访问它们。 [了解详情](/help/destinations/destination-sdk/overview.md#productized-custom-integrations)。

## S

**自助服务文档模板**：自助文档模板提供了一种结构化格式，可用于记录您的目标。 其中包括概述、用例、先决条件、支持的身份、受众、导出类型和频率的部分，以及连接到目标、激活受众和映射属性的步骤。 使用此模板可确保提供全面一致的文档，从而使客户能够快速开始使用您的目标并了解提供的用例。 详细了解 [如何记录您的目标](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md)， [下载最新的自助服务文档模板](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip)、和 [查看其呈现方式](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**模板规范和模板化策略**：模板规范是用于设置从Adobe Experience Platform发送到目标的HTTP请求的格式的配置。 它们将XDM架构中的配置文件属性字段转换为目标平台支持的格式。 使用类似于的模板化语言 [!DNL Jinja]，这些规范允许根据特定规则和输入数据进行动态数据转换。 [了解详情](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md)。

**测试API**：使用测试API，您可以在提交发布请求之前验证目标配置。 它提供了用于生成样本配置文件和测试数据流的工具，确保配置符合目标的要求。 该API支持流目标和基于文件的（批量）目标，提供了一种方法来模拟数据并解决设置过程中的潜在问题。 详细了解的测试API [流式](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) 和 [基于文件的目标](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**转换模板**：转换模板可将数据格式从AdobeXDM架构自定义为目标的预期格式。 [了解详情](/help/destinations/destination-sdk/functionality/destination-server/message-format.md)。