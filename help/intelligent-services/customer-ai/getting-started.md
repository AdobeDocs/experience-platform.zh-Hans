---
keywords: Experience Platform；快速入门；客户人工智能；热门主题
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI入门
description: 本指南提供了示例 API 调用来演示如何格式化请求。这些资源包括路径、必需的标头和格式正确的请求负载。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 8%

---

# Customer AI入门

客户人工智能指南要求对使用客户人工智能所涉及的各种Platform服务有一定的了解。 在开始之前，请查看以下文档：

- [Experience Data Model (XDM)系统概述](../../xdm/home.md)： XDM是允许使用以下操作的基本框架： [!DNL Adobe Experience Cloud](由Experience Platform提供支持)，可在适当的时间通过适当的渠道将适当的消息传递给适当的个人。 构建Experience Platform所基于的方法XDM System可将Experience Data Model架构可操作以供Platform服务使用。
- [模式组合基础](../../xdm/schema/composition.md)：本文档介绍了Experience Data Model (XDM)架构以及用于构成要使用的架构的构建块、原则和最佳实践 [!DNL Adobe Experience Platform].
- [构建架构](../../xdm/tutorials/create-schema-ui.md)：本教程介绍了在Experience Platform中使用架构编辑器创建架构的步骤。
- [Real-time Customer Profile概述](../../rtcdp/overview.md)：构建于 [!DNL Adobe Experience Platform]， Adobe Real-time Customer Data Platform (Real-Time CDP)可帮助企业汇总已知和未知数据，通过在整个客户历程中的智能决策激活客户配置文件。 Real-Time CDP将多个企业数据源整合在一起，实时创建统一的用户档案，用于跨所有渠道和设备提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md)：分段是定义由配置文件存储中的配置文件子集共享的特定属性或行为的过程，以区分可营销的人员组和您的客户群。 例如，在名为“您是否忘记购买运动鞋？”的电子邮件促销活动中，您可能希望受众包含在最近30天内搜索跑鞋但未完成购买的所有用户。 通过使用不同的区段，您可以专注于各种受众，从而提供更加定制的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md)：通过Platform，您可以轻松创建和访问区段，并使用不同的构建块来进一步表示区段的特征。

## 下载客户人工智能分数

>[!NOTE]
>
>如果您不需要下载原始分数，则可以跳过此步骤并转到 [配置指南](./user-guide/configure.md).

下载客户人工智能得分是通过API调用的组合完成的。 要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的所有资源都被隔离到特定的虚拟沙盒中。 所有对Platform API的请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙盒的更多信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md) 在Experience Platform疑难解答指南中。

## 后续步骤

完成本文档中概述的步骤后，请访问 [输入和输出](./data-requirements.md) 文档。 本文档简要概述在客户人工智能中使用和生成的数据类型。
