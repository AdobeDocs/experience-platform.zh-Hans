---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒API指南
description: Adobe Experience Platform中的沙箱提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验和进行自定义配置。
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

的 [!DNL Sandbox] API提供了多个端点，允许您以编程方式管理IMS组织中可供您使用的所有沙箱。 下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅 [入门指南](./getting-started.md) 有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问 [[!DNL Sandbox] API参考](https://www.adobe.io/experience-platform-apis/references/sandbox).

## 可用沙箱

可用沙箱端点允许您查看当前用户可用的所有可用沙箱的列表，包括有关每个沙箱的名称、标题、状态、类型和区域的信息。 中的可用沙箱端点 [!DNL Sandbox] 所有用户（包括没有沙盒管理访问权限的用户）都可以访问API。 请参阅 [可用的沙箱端点指南](./available.md) 了解如何在API中查看可用沙箱。

## 沙盒管理

沙盒是Adobe Experience Platform单个实例中的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。 您可以使用 `/sandboxes` 端点。 要了解如何使用此端点，请参阅 [沙盒端点指南](./sandboxes.md).

## 沙盒类型

目前，Experience Platform上支持的沙盒类型是生产沙盒和开发沙盒。 默认的Platform许可证会授予您总共五个沙箱，您可以将其分类为生产或开发。 您可以额外授权包含10个沙箱，最多共授权75个沙箱。 请参阅 [沙盒类型端点指南](./types.md) 了解如何在API中查看支持的适用于贵组织的沙盒类型。

## 后续步骤

要开始使用 [!DNL Sandbox] API，阅读 [入门指南](./getting-started.md) 然后，选择一个端点指南以了解如何使用特定端点。
