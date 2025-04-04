---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务API指南
description: 查询服务API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# [!DNL Query Service] API指南

本开发人员指南提供了在Adobe Experience Platform [!DNL Query Service] API中执行各种操作的步骤。

## 快速入门

本指南需要深入了解与使用[!DNL Query Service]有关的各种Adobe Experience Platform服务。

- [[!DNL Query Service]](../home.md)：提供查询数据集并将生成的查询捕获为[!DNL Experience Platform]中的新数据集的功能。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
- [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功使用[!DNL Query Service]时需要了解的其他信息。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关本文档中用于示例API调用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 示例API调用

现在您了解了要使用哪些标头，就可以开始调用[!DNL Query Service] API了。 以下文档介绍了您可以使用[!DNL Query Service] API进行的各种API调用。 每个示例调用包括常规API格式、显示所需标头的示例请求以及示例响应。

- [查询](queries.md)
- [连接参数](connection-parameters.md)
- [计划的查询](scheduled-queries.md)
- [针对计划的查询运行](runs-scheduled-queries.md)
- [查询模板](query-templates.md)
- [加速查询](./accelerated-queries.md)
- [警报订阅](./alert-subscriptions.md)

## 后续步骤

现在您已了解如何使用[!DNL Query Service] API进行调用，您可以创建自己的非交互式查询。 有关如何创建查询的详细信息，请参阅[SQL参考指南](../sql/overview.md)。
