---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: 利用机器学习洞察丰富实时客户用户档案
topic: tutorial
type: Tutorial
description: 此文档提供了如何通过机器学习的洞察丰富实时客户用户档案的指南。
translation-type: tm+mt
source-git-commit: 62e6bb7e72637b06808ff87dc21f40af2c4e2d45
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# 利用机器学习洞察丰富[!DNL Real-time Customer Profile]

Adobe Experience Platform[!DNL Data Science Workspace]提供用于创建、评估和利用机器学习模型生成数据预测和洞察的工具和资源。 当机器学习洞察被引入支持[!DNL Profile]的数据集时，同一数据也作为[!DNL Profile]记录被引入，然后使用[!DNL Adobe Experience Platform Segmentation Service]进行分段。 在摄取用户档案和时间序列数据时，实时客户用户档案会自动决定在将数据与现有数据合并并更新合并视图之前，通过一个称为流分段的持续过程将数据包括或排除在细分中。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。

本文档提供教程链接，这些教程使您能够利用机器学习的洞察丰富[!DNL Real-time Customer Profile]。

## 入门指南

要完成以下教程，您必须对收录[!DNL Profile]数据和创建区段有一定的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，提供每个客户的完整、统一的表示形式。
- [[!DNL Identity Service]](../../identity-service/home.md):通过 [!DNL Real-time Customer Profile] 将来自不同数据源的身份引入平台实现。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台组织客户体验数据的标准化框架。

除了上述文档之外，还强烈建议您查看以下模式和模式编辑指南：

- [模式合成基础](../../xdm/schema/composition.md):介绍XDM模式、构件、原则以及编写要在中使用的模式的最佳实践 [!DNL Experience Platform]。
- [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):提供有关使用中的模式编辑器创建模式的详细说明 [!DNL Experience Platform]。

## 创建和配置输出模式和数据集{#create-an-output-schema-and-dataset}

通过评分洞察丰富[!DNL Real-time Customer Profile]的第一步是了解数据定义的真实对象（如人）。 了解数据使您能够描述和设计一种能够增加意义的结构，就像设计关系数据库一样。

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 要开始制作自己的模式，请按照教程中的步骤操作：使用模式编辑器](../../xdm/tutorials/create-schema-ui.md)创建模式。 [请注意，在为[!DNL Profile]启用数据集之前，您需要先配置数据集的模式以具有主标识字段，然后为[!DNL Profile]启用模式。 当数据被引入启用[!DNL Profile]的数据集时，同一数据也作为[!DNL Profile]记录被引入。

如果您希望使用[!DNL Schema Registry] API编写模式，请先阅读[[!DNL Schema Registry] 开发人员指南](../../xdm/api/getting-started.md)，然后再尝试使用[ API](../../xdm/tutorials/create-schema-api.md)创建模式的教程。

准备模式和数据集后，您可以使用适当的模型执行评分运行，从而生成评分数据并将其收录到数据集。

## 使用[!DNL Segment Builder] {#create-segments-using-the-segment-builder}创建区段

在生成并将评分数据洞察引入支持[!DNL Profile]的数据集后，您可以使用[!DNL Segment Builder]创建动态细分。

[!DNL Segment Builder]提供丰富的工作区，允许您与[!DNL Profile]数据元素进行交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。 请按照[[!DNL Segment Builder] 用户指南](../../segmentation/ui/segment-builder.md)了解：

- 使用属性、事件和现有受众的组合作为构件块创建区段定义。
- 使用规则构建器画布和容器控制段规则的执行顺序。
- 查看对潜在受众的评估，以便根据需要调整细分定义。
- 为计划分段启用所有段定义。
- 为流分段启用指定的段定义。

## 后续步骤 {#next-steps}

要进一步了解区段和[!DNL Segment Builder]，请阅读[分段服务概述](../../segmentation/home.md)。

要详细了解[!DNL Real-time Customer Profile]，请阅读[实时客户用户档案概述](../../profile/home.md)