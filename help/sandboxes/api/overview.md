---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: Sandbox API指南
description: Adobe Experience Platform中的沙盒提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验以及进行自定义配置。
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

此 [!DNL Sandbox] API提供了多个端点，允许您以编程方式管理组织中可用的所有沙箱。 这些端点概述如下。 有关详细信息，请访问各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请访问 [[!DNL Sandbox] API参考](https://www.adobe.io/experience-platform-apis/references/sandbox).

## 可用沙盒

可用沙盒端点允许您查看当前用户可用的所有沙盒的列表，包括有关每个沙盒的名称、标题、状态、类型和区域的信息。 中的可用沙盒端点 [!DNL Sandbox] 所有用户（包括没有沙盒管理访问权限的用户）都可以访问API。 请参阅 [可用沙盒端点指南](./available.md) 以了解如何在API中查看可用沙箱。

## 沙盒管理

沙盒是单个Adobe Experience Platform实例中的虚拟分区，允许与数字体验应用程序的开发过程无缝集成。 您可以使用创建、查看、编辑、重置和删除生产沙箱 `/sandboxes` 端点。 要了解如何使用此端点，请参阅 [沙盒端点指南](./sandboxes.md).

## 沙盒类型

目前，Experience Platform上支持的沙盒类型是生产和开发沙盒。 默认的Platform许可证总共授予您5个沙盒，您可以将其分类为生产或开发。 您可以额外许可包含10个沙盒的包，最多总共75个沙盒。 请参阅 [沙盒类型端点指南](./types.md) 了解如何在API中查看您组织支持的沙盒类型。

## 后续步骤

要开始使用 [!DNL Sandbox] API，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
