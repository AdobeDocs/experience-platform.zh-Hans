---
keywords: Experience Platform；机器学习模型；数据科学工作区；实时客户用户档案；热门主题；机器学习洞察
solution: Experience Platform
title: 使用机器学习洞察丰富实时客户用户档案
topic-legacy: tutorial
type: Tutorial
description: 本文档提供了如何通过机器学习洞察丰富实时客户用户档案的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 利用机器学习洞察丰富[!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Data Science Workspace]提供用于创建、评估和利用机器学习模型生成数据预测和洞察的工具和资源。 当机器学习洞察被引入支持[!DNL Profile]的数据集时，同一数据也被引入为[!DNL Profile]记录，然后可以使用[!DNL Adobe Experience Platform Segmentation Service]进行分段。 在摄取用户档案和时间序列数据时，实时用户档案会自动决定在将数据与现有数据合并并更新合并视图之前，通过称为流分段的持续过程将数据包括在细分中或从细分中排除该数据。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。

本文档提供了教程链接，这些教程使您能够利用机器学习洞察丰富[!DNL Real-time Customer Profile]。

## 入门指南

要完成以下教程，您必须对获取[!DNL Profile]数据和创建区段有一定的了解。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，提供每个客户的完整、统一的表示形式。
- [[!DNL Identity Service]](../../identity-service/home.md):通过将 [!DNL Real-time Customer Profile] 来自被引入平台的不同数据源的身份桥接来实现。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台通过该标准化框架组织客户体验数据。

除了上述文档之外，还建议您查看以下模式和模式编辑器指南：

- [模式合成的基础](../../xdm/schema/composition.md):介绍XDM模式、构件块、原则以及编写要在中使用的模式的最佳实践 [!DNL Experience Platform]。
- [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):提供有关使用中的模式编辑器创建模式的详细说 [!DNL Experience Platform]明。

## 创建并配置输出模式和数据集{#create-an-output-schema-and-dataset}

通过评分洞察丰富[!DNL Real-time Customer Profile]的第一步是了解您的数据定义的真实对象（如人）。 了解数据使您能够描述和设计一个结构以增加意义，这与设计关系数据库非常相似。

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 要开始制作您自己的模式，请按照教程中的步骤操作：使用模式编辑器](../../xdm/tutorials/create-schema-ui.md)创建模式。 [请注意，在为[!DNL Profile]启用模式集之前，您需要先配置数据集的模式，使其具有主标识字段，然后为[!DNL Profile]启用数据集。 当将数据引入启用[!DNL Profile]的数据集时，同一数据也作为[!DNL Profile]记录被引入。

如果您希望使用[!DNL Schema Registry] API编写模式，请先阅读[[!DNL Schema Registry] 开发人员指南](../../xdm/api/getting-started.md)，然后尝试使用[创建模式时的教程](../../xdm/tutorials/create-schema-api.md)。

准备模式和数据集后，您可以使用适当的模型执行评分运行，从而生成评分数据并将其收录到数据集。

## 使用[!DNL Segment Builder] {#create-segments-using-the-segment-builder}创建区段

在生成并将评分数据洞察引入支持[!DNL Profile]的数据集后，您可以使用[!DNL Segment Builder]创建动态细分。

[!DNL Segment Builder]提供一个丰富的工作区，允许您与[!DNL Profile]数据元素进行交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。 请按照[[!DNL Segment Builder] 用户指南](../../segmentation/ui/segment-builder.md)了解以下信息：

- 使用属性、事件和现有受众的组合作为构件块创建区段定义。
- 使用规则生成器画布和容器控制执行区段规则的顺序。
- 查看对您的潜在受众的估计，让您能够根据需要调整区段定义。
- 为计划分段启用所有区段定义。
- 为流分段启用指定的段定义。

## 后续步骤 {#next-steps}

要了解有关区段和[!DNL Segment Builder]的详细信息，请阅读[分段服务概述](../../segmentation/home.md)。

要了解有关[!DNL Real-time Customer Profile]的更多信息，请阅读[实时客户用户档案概述](../../profile/home.md)
