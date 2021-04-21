---
keywords: Experience Platform；入门；客户ai；热门主题
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客户人工智能入门
topic-legacy: Getting started
description: 本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 客户人工智能入门

客户人工智能指南需要了解使用客户人工智能所涉及的各种平台服务。 在您开始之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md):XDM是基本框架，它允 [!DNL Adobe Experience Cloud]许在Experience Platform的支持下，在恰当的时间，在适当的渠道向适当的人提供适当的信息。构建Experience Platform的方法，即XDM系统，可操作由平台服务使用的体验数据模型模式。
- [模式合成的基础](../../xdm/schema/composition.md):本文档介绍了体验数据模型(XDM)模式，以及构建要在中使用的模式的构件、原则和最佳做法 [!DNL Adobe Experience Platform]。
- [构建模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用模式编辑器创建模式的步骤。
- [实时客户用户档案概述](../../rtcdp/overview.md):构建在实 [!DNL Adobe Experience Platform]时客户数据平台（实时CDP）上，可帮助公司将已知和未知的数据整合在一起，通过在整个客户旅程中的智能决策激活客户用户档案。实时CDP将多个企业用户档案源组合在一起，以实时创建统一的数据，这些数据可用于在所有渠道和设备上提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md):分段是定义由用户档案子集从用户档案库共享的特定属性或行为的过程，以区分有价人群和客户群。例如，在名为“您忘记购买运动鞋了吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑鞋但未完成购买的所有用户。 使用不同的细分，您可以专注于各种受众，提供更加自定义的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md):平台允许您轻松创建和访问区段，并使用不同的构建块来进一步描述区段特征。

## 下载客户人工智能得分

>[!NOTE]
>
>如果您不需要下载原始分数，可以跳过此步骤并继续阅读[配置指南](./user-guide/configure.md)。

下载客户AI得分是通过API调用的组合完成的。 要调用平台API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权：承载`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定的虚拟沙箱。 对平台API的所有请求都需要一个头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md)的部分。[

## 后续步骤

完成上述文档中概述的步骤后，请访问[输入和输出](./input-output.md)文档。 本文档简要概述了在客户人工智能中使用和生成的数据类型。
