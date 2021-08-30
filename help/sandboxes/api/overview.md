---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒API指南
topic-legacy: developer guide
description: Adobe Experience Platform中的沙箱提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验和进行自定义配置。
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

[!DNL Sandbox] API提供了多个端点，允许您以编程方式管理IMS组织内所有可用的沙箱。 下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅[快速入门指南](./getting-started.md) ，以了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[[!DNL Sandbox] API引用](https://www.adobe.io/experience-platform-apis/references/sandbox)。

## 可用沙箱

可用沙箱端点允许您查看当前用户可用的所有可用沙箱的列表，包括有关每个沙箱的名称、标题、状态、类型和区域的信息。 [!DNL Sandbox] API中可用的沙盒端点可由所有用户访问，包括那些没有沙盒管理访问权限的用户。 请参阅[可用沙箱端点指南](./available.md) ，了解如何在API中查看可用沙箱。

## 沙盒管理

沙盒是Adobe Experience Platform单个实例中的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。 您可以使用`/sandboxes`端点创建、查看、编辑、重置和删除生产和开发沙箱。 要了解如何使用此端点，请参阅[沙盒端点指南](./sandboxes.md)。

## 沙盒类型

目前，Experience Platform上支持的沙盒类型是生产沙盒和开发沙盒。 默认的Platform许可证会授予您总共五个沙箱，您可以将其分类为生产或开发。 您可以额外授权包含10个沙箱，最多共授权75个沙箱。 请参阅[沙盒类型端点指南](./types.md) ，了解如何在API中查看支持的组织的沙盒类型。

## 后续步骤

要开始使用[!DNL Sandbox] API进行调用，请阅读[入门指南](./getting-started.md)，然后选择其中一个端点指南，以了解如何使用特定端点。