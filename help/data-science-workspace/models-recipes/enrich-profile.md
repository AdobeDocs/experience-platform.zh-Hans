---
keywords: Experience Platform；机器学习模型；Data Science Workspace；实时客户个人资料；热门主题；机器学习见解
solution: Experience Platform
title: 利用机器学习见解丰富实时客户档案
type: Tutorial
description: 本文档提供了有关如何使用机器学习见解丰富Real-time Customer Profile的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 扩充 [!DNL Real-Time Customer Profile] 使用机器学习见解

Adobe Experience Platform [!DNL Data Science Workspace] 提供用于创建、评估和利用机器学习模型以生成数据预测和洞察的工具和资源。 将机器学习分析摄取到 [!DNL Profile] — 启用的数据集，则同样的数据也会被摄取为 [!DNL Profile] 记录，然后可以使用以下方式对其进行分段： [!DNL Adobe Experience Platform Segmentation Service].

本文档提供了指向教程的链接，这些教程使您能够扩充 [!DNL Real-Time Customer Profile] 使用您的机器学习见解。

## 快速入门

要完成下面的教程，您需要对摄取有一定的了解 [!DNL Profile] 数据和创建区段。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据，为每个客户提供完整、统一的呈现。
- [[!DNL Identity Service]](../../identity-service/home.md)：启用 [!DNL Real-Time Customer Profile] 通过桥接从被引入到Platform中的不同数据源中的身份。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform用于组织客户体验数据的标准化框架。

除了上述文档之外，还强烈建议您查看有关架构和架构编辑器的以下指南：

- [模式组合基础](../../xdm/schema/composition.md)：描述用于构成架构的XDM架构、构建基块、原则和最佳实践，这些架构用于 [!DNL Experience Platform].
- [架构编辑器教程](../../xdm/tutorials/create-schema-ui.md)：提供有关使用中的架构编辑器创建架构的详细说明 [!DNL Experience Platform].

## 创建和配置输出架构和数据集 {#create-an-output-schema-and-dataset}

走向充实的第一步 [!DNL Real-Time Customer Profile] 有了评分洞察，您就可以知道数据定义的真实世界对象（如人员）。 了解数据使您能够描述和设计结构以添加含义，就像设计关系数据库一样。

架构的构建从指定类开始。 类定义架构将包含的数据的行为方面（记录或时间序列）。 要开始自行创建架构，请按照以下教程中的步骤操作： [使用架构编辑器创建架构](../../xdm/tutorials/create-schema-ui.md). 请注意，在为启用数据集之前 [!DNL Profile]，您需要配置数据集的架构以使其包含主标识字段，然后为启用架构 [!DNL Profile]. 当数据被摄取到 [!DNL Profile] — 启用的数据集，则同样的数据也会被摄取为 [!DNL Profile] 记录。

如果您希望使用 [!DNL Schema Registry] API，请首先阅读 [[!DNL Schema Registry] 开发人员指南](../../xdm/api/getting-started.md) 在尝试教程之前，请执行以下操作 [使用API创建架构](../../xdm/tutorials/create-schema-api.md).

准备好架构和数据集后，您可以使用适当的模型执行评分运行，从而生成评分数据并将其摄取到数据集。

## 使用创建区段 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

生成评分数据见解并将其摄取到您的之后 [!DNL Profile]-enabled dataset，您可以使用 [!DNL Segment Builder].

此 [!DNL Segment Builder] 提供了一个丰富的工作区，允许您与 [!DNL Profile] 数据元素。 工作区为构建和编辑规则提供了直观的控件，例如用于表示数据属性的拖放图块。 请遵循 [[!DNL Segment Builder] 用户指南](../../segmentation/ui/segment-builder.md) 要了解以下内容：

- 将属性、事件和现有受众的组合用作构建块来创建区段定义。
- 使用规则生成器画布和容器控制区段规则的执行顺序。
- 查看潜在受众的估计，允许您根据需要调整区段定义。
- 启用计划分段的所有区段定义。
- 为流式分段启用指定的区段定义。

## 后续步骤 {#next-steps}

要了解有关区段和 [!DNL Segment Builder]，请阅读 [分段服务概述](../../segmentation/home.md).

要了解有关 [!DNL Real-Time Customer Profile]，请阅读 [Real-time Customer Profile概述](../../profile/home.md)
