---
keywords: Experience Platform；快速入门；客户ai；热门主题
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI快速入门
description: 本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 596921163bf64d11545dcde49039bcdd07c253dd
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Customer AI快速入门

Customer AI指南需要对使用Customer AI时涉及的各种平台服务有一定的了解。 开始之前，请查阅以下文档：

- [Experience Data Model(XDM)系统概述](../../xdm/home.md):XDM是允许 [!DNL Adobe Experience Cloud]由Experience Platform提供支持，在适当的时间通过适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法 — XDM系统，可操作Experience Data Model模式以供Platform服务使用。
- [架构组合的基础知识](../../xdm/schema/composition.md):本文档简要介绍Experience Data Model(XDM)架构，以及组合架构以在 [!DNL Adobe Experience Platform].
- [构建模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用架构编辑器创建架构的步骤。
- [实时客户资料概述](../../rtcdp/overview.md):内置 [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform(Real-Time CDP)可帮助公司将已知和未知数据整合在一起，通过智能决策在整个客户历程中激活客户用户档案。 Real-Time CDP整合了多个企业数据源以实时创建统一的配置文件，可用于跨所有渠道和设备提供一对一的个性化客户体验。
- [Segmentation Service概述](../../segmentation/home.md):分段是定义用户档案库中用户档案子集共享的特定属性或行为的过程，用于将可销售的人群与客户群区分开来。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件促销活动中，您可能希望看到过去30天内搜索跑鞋但未完成购买的所有用户的受众。 使用不同的区段，您可以专注于各个受众，从而提供更加自定义的营销体验。
- [区段生成器用户指南](../../segmentation/tutorials/create-a-segment.md):通过平台，您可以轻松创建和访问区段，并使用不同的构建基块进一步描述区段的特性。

## 下载Customer AI分数

>[!NOTE]
>
>如果您不需要下载原始分数，则可以跳过此步骤并继续 [配置指南](./user-guide/configure.md).

下载Customer AI得分可通过组合API调用来完成。 要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙箱的更多信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md) (位于Experience Platform疑难解答指南中)。

## 后续步骤

完成上述文档中所述的步骤后，请访问 [输入和输出](./input-output.md) 文档。 本文档简要概述了在Customer AI中使用和生成的数据类型。
