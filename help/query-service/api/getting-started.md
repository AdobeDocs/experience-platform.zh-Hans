---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务API指南
topic-legacy: query templates
description: 查询服务API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 4f85f38e4870f0c2429a3a2a50bd7f95075c6be4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 5%

---

# [!DNL Query Service] API指南

本开发人员指南提供了在Adobe Experience Platform中执行各种操作的步骤 [!DNL Query Service] API。

## 快速入门

本指南要求您对使用涉及的各种Adobe Experience Platform服务有一定的了解 [!DNL Query Service].

- [[!DNL Query Service]](../home.md):提供在 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了为成功使用而需要了解的其他信息 [!DNL Query Service] 使用API。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关本文档中用于示例API调用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Experience Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Platform] API调用，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在 [!DNL Experience Platform]，请参阅 [沙箱概述文档](../../sandboxes/home.md).

## API调用示例

既然您了解了要使用的标头，接下来便可以开始调用 [!DNL Query Service] API。 以下文档将介绍您可以使用 [!DNL Query Service] API。 每个示例调用都包括常规API格式、显示所需标头的示例请求以及示例响应。

- [查询](queries.md)
- [连接参数](connection-parameters.md)
- [计划查询](scheduled-queries.md)
- [针对计划查询运行](runs-scheduled-queries.md)
- [查询模板](query-templates.md)
- [警报订阅](./alert-subscriptions.md)

## 后续步骤

现在，您已经学习了如何使用 [!DNL Query Service] API，您可以创建自己的非交互式查询。 有关如何创建查询的详细信息，请阅读 [SQL参考指南](../sql/overview.md).
