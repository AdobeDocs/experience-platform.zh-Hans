---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: 客户AI快速入门
topic: Getting started
translation-type: tm+mt
source-git-commit: 0eeb41fa06864cc28b3a76c2a69c76ea5430d45a

---


# 客户AI快速入门

客户人工智能指南需要对使用客户人工智能所涉及的各种平台服务进行有效理解。 在开始之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md):XDM是一个基本框架，它允许Adobe Experience Cloud以Experience Platform为后盾，在恰当的时机在正确的渠道上向正确的人员提供正确的信息。 构建Experience Platform的方法(XDM System)可操作Experience Data Model模式，供Platform服务使用。
- [模式合成的基础知识](../../xdm/schema/composition.md):本文档介绍了Experience Data Model(XDM)模式，以及构成要在Adobe Experience Platform中使用的模式的构件块、原则和最佳做法。
- [建筑模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用模式编辑器创建模式的步骤。
- [实时客户用户档案概述](../../rtcdp/overview.md):Adobe实时客户数据平台(Real-time CDP)构建于Adobe Experience Platform之上，可帮助公司整合已知和未知的数据，在整个客户旅程中通过智能决策激活客户用户档案。 实时CDP结合了多个企业数据源，以实时创建统一的用户档案，这些数据可用于在所有渠道和设备上提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md):细分是定义用户档案子集与用户档案商店共享的特定属性或行为的过程，以区分可销售的人群和客户群。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑鞋但未完成购买的所有用户。 使用不同的细分，您可以专注于各种受众，提供更加自定义的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md):平台允许您轻松创建和访问区段，并使用不同的构建块进一步描述区段。

## 下载客户AI得分

>[!NOTE] 如果您不需要下载原始分数，可以跳过此步骤并继续阅读用户界面指南。

通过组合API调用，可以下载客户AI得分。 要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md) 。

## 后续步骤

准备就绪并准备好所有凭据和模式后，请遵循客户AI用户界面指 [南进行开始](./user-guide.md)。 本指南将指导您逐步创建实例，并提交该实例进行培训和评分。