---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: 归因AI快速入门
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# 归因AI快速入门

以下指南需要了解使用归因 [!DNL Adobe Experience Platform] AI时涉及的各种服务。 在开始教程之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md): XDM是一个基本框架，它 [!DNL Adobe Experience Cloud]允许在Experience Platform的支持下，在正确的渠道，在恰当的时刻，向正确的人提供正确的信息。 构建Experience Platform的方法体系XDM系统可操作由平台服务使用的体验数据模型模式。
- [模式合成基础](../../xdm/schema/composition.md): 本文档介绍了体验数据模型(XDM)模式，以及构成要用于的模式的构件、原则和最佳做法 [!DNL Adobe Experience Platform]。
- [构建模式](../../xdm/tutorials/create-schema-ui.md): 本教程介绍了在模式中使用模式编辑器创建Experience Platform的步骤。

归因AI要求数据集符合消费者体验事件(CEE)模式，该是体验数据模型(XDM) [中的一个组](../../xdm/home.md) 合体。 请通过attributionai-support@adobe.com与Adobe支持部门联系，以实施或更改此数据。 如果存在媒体支出数据，您可以进行进一步的分析，如增加收入和ROI。 如果客户用户档案数据可用，您可以进一步将积分归因到客户用户档案级别。

## 术语

- **转换事件:** 客户为表明目标（如会议注册）的里程碑而进行的任何数字事件或数字交互。 其他示例包括付费转换、免费帐户注册或特征资格鉴定。

- **触点：** 客户在实现目标的过程中进行的任何数字事件或数字交互。 示例包括与购买前相关的营销工作、已查看的展示广告印象和付费搜索点击。

## 下载归因AI得分

>[!NOTE]
>
>如果您不需要下载原始分数，您可以跳过此步骤并继续执行下 [一步](#next-steps)。

下载归因AI得分可通过API调用的组合完成。 要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

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

## 后续步骤 {#next-steps}

准备好并准备好所有凭据和模式后，请遵循归因AI用户界 [面指南进行开始](./user-guide.md)。 本指南将指导您创建实例并提交它以进行培训和评分。