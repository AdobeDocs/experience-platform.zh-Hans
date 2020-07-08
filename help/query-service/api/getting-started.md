---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查询服务开发人员指南
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# 查询服务开发人员指南

此开发人员指南提供了在Adobe Experience Platform查询服务API中执行各种操作的步骤。

## 入门指南

本指南要求对与使用Adobe Experience Platform服务相关的各种查询服务进行有效了解。

- [查询服务](../home.md): 提供查询数据集并将生成的查询捕获为Experience Platform中的新数据集的能力。
- [体验数据模型(XDM)系统](../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
- [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便成功使用API的查询服务。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关本文档中用于示例API调用的约定的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的一节。

### 收集所需标题的值

要调用Experience PlatformAPI，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有平台API调用中每个所需标头的值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定将在其中执行操作的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在Experience Platform中使用沙箱的更多信息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 示例API调用

现在，您已经了解要使用哪些标头，可以开始调用查询服务API。 以下文档将遍历您可以使用查询服务API进行的各种API调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求和示例响应。

- [查询](queries.md)
- [连接参数](connection-parameters.md)
- [计划查询](scheduled-queries.md)
- [为计划查询运行](runs-scheduled-queries.md)
- [查询模板](query-templates.md)

## 后续步骤

现在，您已学习了如何使用查询服务API进行调用，可以创建自己的非交互式查询。 有关如何创建查询的详细信息，请阅读 [SQL参考指南](../sql/overview.md)。