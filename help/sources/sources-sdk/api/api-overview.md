---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
title: 自助式源(Batch SDK) API指南
description: 本文档概述了创建新源的过程，包括有关如何使用Flow Service API检索、编写和提交新连接规范的步骤。
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 自助式源(Batch SDK) API指南

本文档概述了创建新源的过程，包括有关如何使用编写和提交新连接规范的步骤。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] 用于收集并集中Platform内各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，可让您轻松设置到各种数据提供商的源连接。 通过这些源连接，您可以对第三方系统进行身份验证、设置摄取运行的时间，以及管理数据摄取吞吐量。

此 [!DNL Flow Service] API提供了多个端点，允许您以编程方式管理通过自助服务源(Batch SDK)集成的新源的连接和流量规范。

## 创建新的连接规范

配置新源的第一步是创建新的连接规范。

连接规范返回源的连接器属性。 它们包括与创建基本连接和源连接相关的身份验证规范，以及分配给特定源的固定连接规范ID。 连接规范与租户和组织无关。 典型的连接规范包含有关给定源的基本信息，以及三个不同的部分： `authSpec`， `sourceSpec`、和 `exploreSpec`.

有关详细说明，请参阅 [创建新的连接规范](./create.md). 有关用于连接规范的属性和值的信息，包括有关配置身份验证、源和浏览规范的详细信息，请参阅 [配置选项文档](../config/config.md).

## 更新流程规范

成功创建连接规范后，必须附加 `RestStorageToAEP` 流规范，使您的源能够创建数据流。

流程规范包含定义流程的信息，包括它支持的源连接ID和目标连接ID、需要应用于数据的转换规范以及生成流程所需的计划参数。

有关详细说明，请参阅 [更新流程规范](./update-flow-specs.md).

## 更新您的连接规范

您可以通过向以下网站发出PUT请求来更新连接规范： [!DNL Flow Service] API。 请参阅指南，网址为 [更新连接规范](./update-connection-specs.md) 了解更多信息。

## 提交您的源

要提交源以供Experience Platform集成，您必须先完成整个 [!DNL Flow Service] 源的API工作流，可确保源成功工作。 如果源运行成功，则可以继续操作，并联系Adobe代表进行验证和提升。 请参阅指南，网址为 [测试和提交源](./submit.md) 了解更多信息

## 后续步骤

要开始使用 [!DNL Flow Service] API和通过自助源(Batch SDK)创建新源，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
