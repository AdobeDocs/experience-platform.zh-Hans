---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: 查询服务开发人员指南
topic: query templates
description: 此开发人员指南提供在Adobe Experience Platform查询服务API中执行各种操作的步骤。
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# [!DNL Query Service] 开发人员指南

此开发人员指南提供在Adobe Experience PlatformAPI中执行各种操作的 [!DNL Query Service] 步骤。

## 入门指南

本指南要求对Adobe Experience Platform与使用有关的各项服务有工作的了解 [!DNL Query Service]。

- [[!DNL查询服务]](../home.md):提供查询数据集并将生成的查询捕获为中的新数据集的能力 [!DNL Experience Platform]。
- [[!DNL体验数据模型(XDM)系统]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL沙箱]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功使用API所需了解的其 [!DNL Query Service] 他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关本文档中用于示例API调用的约定的信息，请参阅疑难解答 [指南中有关如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 的一节。

### 收集所需标题的值

要调用API，您必 [!DNL Experience Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Platform] 标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定要在其中执行操作的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在中使用沙箱的更多信 [!DNL Experience Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 示例API调用

现在，您已经了解要使用哪些标头，便可开始调用 [!DNL Query Service] API。 以下文档将遍历您可以使用API进行的各种API [!DNL Query Service] 调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求和示例响应。

- [查询](queries.md)
- [连接参数](connection-parameters.md)
- [计划查询](scheduled-queries.md)
- [为计划查询运行](runs-scheduled-queries.md)
- [查询模板](query-templates.md)

## 后续步骤

现在您已经学习了如何使用API进行 [!DNL Query Service] 调用，您可以创建自己的非交互式查询。 有关如何创建查询的详细信息，请阅读 [SQL参考指南](../sql/overview.md)。