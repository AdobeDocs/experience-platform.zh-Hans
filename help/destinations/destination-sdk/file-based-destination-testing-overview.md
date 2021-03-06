---
description: 基于文件的目标测试API是端点的集合，您可以使用这些端点来验证通过Destination SDK构建的基于文件的目标的配置。
title: 基于文件的目标测试API
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# 基于文件的目标测试API

## 概述 {#overview}

基于文件的目标测试API是一组端点，您可以使用这些端点来验证通过Destination SDK构建的基于文件的目标的配置。

我们建议您先使用这些工具来验证您的配置 [提交](submit-destination.md) 您的审阅目标Adobe。

为获得最佳测试结果，我们建议根据以下流程图使用此API。

![显示推荐目标测试流程的图表](assets/file-based-testing-flow.png)

有关每个端点可以执行的操作的简要概述，请参阅以下部分。

## 生成示例用户档案 {#generate-sample-profiles}

使用 `/sample-profiles` API端点，用于根据您现有的源架构生成示例配置文件。

示例用户档案可帮助您了解用户档案的JSON结构。 此外，它们还为您提供了一个默认设置，您可以使用自己的配置文件数据进行自定义，以进一步进行目标测试。

请参阅 [专用文档](file-based-sample-profile-generation-api.md) 了解如何生成示例用户档案。

## 测试目标配置 {#test-destination-configuration}

使用 `/testing/destinationInstance` 用于测试基于文件的目标是否正确配置，以及验证数据流向您配置的目标的完整性的API端点。

无论是否添加，您都可以向测试端点发出请求 [示例用户档案](file-based-sample-profile-generation-api.md) 呼叫。 如果您未在请求中发送任何用户档案，则API会自动生成一个示例用户档案并将其添加到请求中。

请参阅 [专用文档](file-based-destination-testing-api.md) 了解如何使用示例用户档案测试目标配置。

## 查看详细的激活结果 {#view-detailed-activation-results}

使用 `/testing/destinationInstance` 用于查看基于文件的目标测试结果的完整详细信息的API端点。

此API端点会返回与使用 [流量服务API](../api/update-destination-dataflows.md) 监视数据流。

请参阅 [专用文档](file-based-destination-results-api.md) 了解如何查看详细的激活结果。

## 呈现客户数据字段 {#render-customer-data-fields}

使用 `/authoring/testing/template/render` 用于显示模板化情况的API端点 [客户数据字段](file-based-destination-configuration.md#customer-data-fields) 在目标配置中定义的内容如下所示。

API端点会为您的客户数据字段生成随机值，并在响应中返回它们。 这有助于您验证客户数据字段的语义结构，如存储段名称或文件夹路径。

请参阅 [专用文档](file-based-render-template-api.md) 了解如何为客户数据字段生成和可视化值。