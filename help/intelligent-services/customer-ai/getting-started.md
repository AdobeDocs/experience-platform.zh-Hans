---
keywords: Experience Platform；快速入门；客户人工智能；热门主题
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI入门
description: 本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Customer AI入门

客户人工智能指南要求实际了解使用客户人工智能所涉及的各种Platform服务。 在开始之前，请查看以下文档：

- [Experience Data Model (XDM)系统概述](../../xdm/home.md)：XDM是允许使用以下项操作的基础框架： [!DNL Adobe Experience Cloud](由Experience Platform提供支持)在正确的时间通过正确的渠道向正确的人员传递正确的信息。 构建Experience Platform所基于的方法XDM System可使Experience Data Model架构可操作以供Platform服务使用。
- [模式组合基础](../../xdm/schema/composition.md)：本文档介绍了Experience Data Model (XDM)架构，以及构成要使用的架构的构建基块、原则和最佳实践。 [!DNL Adobe Experience Platform].
- [构建架构](../../xdm/tutorials/create-schema-ui.md)：本教程介绍了在Experience Platform中使用架构编辑器创建架构的步骤。
- [Real-time Customer Profile概述](../../rtcdp/overview.md)：构建 [!DNL Adobe Experience Platform]， Adobe Real-time Customer Data Platform (Real-Time CDP)可帮助企业整合已知和未知数据，以便通过在整个客户历程中的智能决策激活客户档案。 Real-Time CDP将多个企业数据源整合在一起，实时创建统一的用户档案，用于跨所有渠道和设备提供一对一的个性化客户体验。
- [分段服务概述](../../segmentation/home.md)：分段是定义配置文件存储中的配置文件子集共享的特定属性或行为的过程，用于将可销售人群与客户群区分开来。 例如，在名为“您是否忘记购买运动鞋？”的电子邮件营销活动中，您可能希望了解过去30天内搜索跑鞋但未完成购买的所有用户。 通过使用不同的区段，您可以专注于各种受众，从而提供更加定制的营销体验。
- [Segment Builder用户指南](../../segmentation/tutorials/create-a-segment.md)：通过Platform，您可以轻松地创建和访问区段，并使用不同的构建基块来进一步表示区段的特征。

## 下载Customer AI分数

>[!NOTE]
>
>如果您不需要下载原始分数，则可以跳过此步骤并转到 [配置指南](./user-guide/configure.md).

通过组合API调用下载客户人工智能分数。 要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有资源都与特定的虚拟沙盒隔离。 对Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙盒的更多信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md) 在Experience Platform疑难解答指南中。

## 后续步骤

完成上述文档中概述的步骤后，请访问 [输入和输出](./data-requirements.md) 文档。 本文档简要概述客户人工智能中使用和生成的数据类型。
