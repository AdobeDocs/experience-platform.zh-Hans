---
keywords: Experience Platform；机器学习模型；Data Science Workspace；实时客户资料；热门主题；机器学习分析
solution: Experience Platform
title: 使用机器学习分析丰富实时客户资料
topic-legacy: tutorial
type: Tutorial
description: 本文档提供了有关如何利用机器学习分析扩充实时客户资料的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 89a9b64f2fb238c08a281f29a035ce0b24b34804
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 丰富 [!DNL Real-time Customer Profile] 使用机器学习分析

Adobe Experience Platform [!DNL Data Science Workspace] 提供用于创建、评估和利用机器学习模型生成数据预测和分析的工具和资源。 将机器学习分析引入 [!DNL Profile]启用的数据集，该数据也被摄取为 [!DNL Profile] 随后可使用 [!DNL Adobe Experience Platform Segmentation Service].

本文档提供了教程的链接，这些教程使您能够丰富 [!DNL Real-time Customer Profile] 学习机器知识。

## 快速入门

要完成以下教程，您需要对摄取有一定的了解 [!DNL Profile] 数据和创建区段。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，为每个客户提供完整、统一的表示形式。
- [[!DNL Identity Service]](../../identity-service/home.md):启用 [!DNL Real-time Customer Profile] 通过将来自不同数据源的身份桥接到平台中。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。

除了上述文档之外，还强烈建议您查看以下架构和架构编辑器指南：

- [架构组合的基础知识](../../xdm/schema/composition.md):介绍XDM架构、构建基块、原则以及组合要在 [!DNL Experience Platform].
- [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):提供了有关在 [!DNL Experience Platform].

## 创建和配置输出架构和数据集 {#create-an-output-schema-and-dataset}

迈向富裕的第一步 [!DNL Real-time Customer Profile] 借助评分分析，您可以了解数据定义的真实对象（如人员）。 了解数据后，您可以描述和设计一个结构以添加含义，就像设计关系数据库一样。

从分配类开始合成架构。 类定义架构将包含的数据的行为方面（记录或时间系列）。 要开始创建您自己的模式，请按照 [使用模式编辑器创建模式](../../xdm/tutorials/create-schema-ui.md). 请注意，在为 [!DNL Profile]，您需要将数据集的架构配置为具有主标识字段，然后为 [!DNL Profile]. 将数据摄取到 [!DNL Profile]启用的数据集，该数据也被摄取为 [!DNL Profile] 记录。

如果您希望使用 [!DNL Schema Registry] 而是从读取 [[!DNL Schema Registry] 开发人员指南](../../xdm/api/getting-started.md) 在尝试教程之前 [使用API创建模式](../../xdm/tutorials/create-schema-api.md).

准备好架构和数据集后，您可以使用相应的模型执行评分运行，以生成评分数据并将其摄取到数据集。

## 使用 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

在生成并将评分数据分析摄取到您的 [!DNL Profile]启用的数据集，您可以使用 [!DNL Segment Builder].

的 [!DNL Segment Builder] 提供了丰富的工作区，可让您与 [!DNL Profile] 数据元素。 工作区提供了用于构建和编辑规则的直观控件，例如用于表示数据属性的拖放图块。 关注 [[!DNL Segment Builder] 用户指南](../../segmentation/ui/segment-builder.md) 要了解：

- 使用属性、事件和现有受众的组合作为构建基块来创建区段定义。
- 使用规则生成器画布和容器控制区段规则执行的顺序。
- 查看潜在受众的估计值，以便根据需要调整区段定义。
- 为计划分段启用所有区段定义。
- 为流分段启用指定的区段定义。

## 后续步骤 {#next-steps}

了解有关区段和 [!DNL Segment Builder]，阅读 [Segmentation Service概述](../../segmentation/home.md).

详细了解 [!DNL Real-time Customer Profile]，阅读 [实时客户资料概述](../../profile/home.md)
