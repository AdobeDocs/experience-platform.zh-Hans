---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: 客户人工智能入门
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# 客户人工智能入门

客户人工智能指南需要对使用客户人工智能所涉及的各种平台服务进行有效的了解。 在开始之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md): XDM是一个基本框架，它 [!DNL Adobe Experience Cloud]允许在Experience Platform的支持下，在正确的渠道，在恰当的时刻，向正确的人提供正确的信息。 构建Experience Platform的方法体系XDM系统可操作由平台服务使用的体验数据模型模式。
- [模式合成基础](../../xdm/schema/composition.md): 本文档介绍了体验数据模型(XDM)模式，以及构成要用于的模式的构件、原则和最佳做法 [!DNL Adobe Experience Platform]。
- [构建模式](../../xdm/tutorials/create-schema-ui.md): 本教程介绍了在模式中使用模式编辑器创建Experience Platform的步骤。
- [实时客户用户档案概述](../../rtcdp/overview.md): 构建在 [!DNL Adobe Experience Platform]上 [!DNL Adobe Real-time Customer Data Platform] （实时CDP）可帮助公司将已知和未知的数据整合在一起，通过在整个客户旅程中的智能决策激活客户用户档案。 实时CDP结合了多个企业用户档案源，以实时创建统一的渠道，这些数据可用于在所有和设备上提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md): 分段是定义用户档案子集从用户档案商店共享的特定属性或行为的过程，以区分有价人群和客户群。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑步鞋但未完成购买的所有用户。 使用不同的细分，您可以专注于各种受众，提供更加自定义的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md): 平台允许您轻松创建和访问细分，并使用不同的构件块进一步描述细分。

## 下载客户AI得分

>[!NOTE]
>
>如果您不需要下载原始分数，可以跳过此步骤并继续阅读配置 [指南](./user-guide/configure.md)。

下载客户AI得分是通过API调用的组合完成的。 要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md) 用的章节。

## 后续步骤

完成上述文档中概述的步骤后，请访 [问输入和输出](./input-output.md) 。 本文档简要概述了客户人工智能中使用和生成的数据类型。