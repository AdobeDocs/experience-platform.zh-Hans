---
keywords: Experience Platform；快速入门；客户人工智能；热门主题
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI入门
description: 本指南提供了示例 API 调用来演示如何格式化请求。这些资源包括路径、必需的标头和格式正确的请求负载。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 8%

---

# Customer AI入门

客户人工智能指南要求实际了解使用客户人工智能所涉及的各种Experience Platform服务。 在开始之前，请查看以下文档：

- [体验数据模型(XDM)系统概述](../../xdm/home.md)： XDM是一个基础框架，它允许[!DNL Adobe Experience Cloud]在正确的时间通过正确的渠道向正确的人员传递正确的消息，该框架由Experience Platform提供支持。 构建Experience Platform所基于的方法XDM系统可使Experience Data Model架构可操作以供Experience Platform服务使用。
- [架构组合的基础知识](../../xdm/schema/composition.md)：本文档介绍了体验数据模型(XDM)架构以及用于组合要在[!DNL Adobe Experience Platform]中使用的架构的构建块、原则和最佳实践。
- [构建架构](../../xdm/tutorials/create-schema-ui.md)：本教程介绍了在Experience Platform中使用“架构编辑器”创建架构的步骤。
- [实时客户配置文件概述](../../rtcdp/overview.md)：Adobe Real-Time Customer Data Platform (Real-Time CDP)构建于[!DNL Adobe Experience Platform]，可帮助公司汇总已知和未知数据，以通过客户历程中的智能决策激活客户配置文件。 Real-Time CDP将多个企业数据源整合在一起，实时创建统一的用户档案，用于跨所有渠道和设备提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md)：分段是定义配置文件存储中由配置文件子集共享的特定属性或行为的过程，以便区分可销售的人员组和您的客户群。 例如，在名为“您是否忘记购买运动鞋？”的电子邮件促销活动中，您可能希望受众包含在最近30天内搜索跑鞋但未完成购买的所有用户。 通过使用不同的区段，您可以专注于各种受众，从而提供更加定制的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md)：通过Experience Platform，您可以轻松地创建和访问区段，并使用不同的构建块来进一步表示区段的特征。

## 下载客户人工智能分数

>[!NOTE]
>
>如果您不需要下载原始得分，则可以跳过此步骤，继续阅读[配置指南](./user-guide/configure.md)。

下载客户人工智能得分是通过API调用的组合完成的。 要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的所有资源都被隔离到特定的虚拟沙盒中。 对Experience Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md)的部分。

## 后续步骤

完成上述文档中所述的步骤后，请访问[输入和输出](./data-requirements.md)文档。 本文档简要概述在客户人工智能中使用和生成的数据类型。
