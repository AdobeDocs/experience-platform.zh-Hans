---
description: 了解如何使用基于文件的目标测试API来验证通过Destination SDK构建的基于文件的目标的配置。
title: 基于文件的目标测试API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 基于文件的目标测试API概述

基于文件的目标测试API是一组端点，您可以使用它们验证通过Destination SDK构建的基于文件的目标的配置。

我们建议使用这些工具来验证您的配置，然后再 [提交](../../guides/submit-destination.md) 您要Adobe的审阅目标。

为获得最佳测试结果，我们建议根据下面的流程图使用此API。

![显示推荐的目标测试流程的图](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

请参阅以下部分，简要概述每个端点的功能。

## 生成样本配置文件 {#generate-sample-profiles}

使用 `/sample-profiles` 用于根据现有源架构生成示例配置文件的API端点。

示例配置文件可以帮助您了解配置文件的JSON结构。 此外，它们还为您提供了一个默认值，您可以使用自己的配置文件数据进行自定义，以便进一步进行目标测试。

请参阅 [专用文档](file-based-sample-profile-generation-api.md) 以了解如何生成示例用户档案。

## 测试目标配置 {#test-destination-configuration}

使用 `/testing/destinationInstance` API端点，用于测试基于文件的目标是否配置正确，并验证数据流到已配置目标的完整性。

您可以向测试端点发出请求，无论是否添加 [样本配置文件](file-based-sample-profile-generation-api.md) 到电话那边。 如果您未在请求上发送任何配置文件，则API会自动生成示例配置文件并将其添加到请求中。

请参阅 [专用文档](file-based-destination-testing-api.md) 以了解如何使用示例配置文件测试目标配置。

## 查看详细的激活结果 {#view-detailed-activation-results}

使用 `/testing/destinationInstance` API端点，用于查看基于文件的目标测试结果的完整详细信息。

此API端点返回的结果与使用时获得的结果相同 [流服务API](../../../api/update-destination-dataflows.md) 监视数据流。

请参阅 [专用文档](file-based-destination-results-api.md) 了解如何查看详细的激活结果。

## 呈现客户数据字段 {#render-customer-data-fields}

使用 `/authoring/testing/template/render` API端点，用于可视化模板化的方式 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 在目标配置中定义的内容，如下所示。

API端点会为客户数据字段生成随机值，并在响应中返回它们。 这有助于您验证客户数据字段（如存储段名称或文件夹路径）的语义结构。

请参阅 [专用文档](file-based-render-template-api.md) 以了解如何生成和可视化客户数据字段的值。
