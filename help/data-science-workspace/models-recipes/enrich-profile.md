---
keywords: Experience Platform；机器学习模型；数据科学Workspace；实时客户个人资料；热门主题；机器学习见解
solution: Experience Platform
title: 利用机器学习见解丰富实时客户档案
type: Tutorial
description: 本文档提供了有关如何使用机器学习见解丰富Real-time Customer Profile的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 使用机器学习见解丰富[!DNL Real-Time Customer Profile]

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

Adobe Experience Platform [!DNL Data Science Workspace]提供了用于创建、评估和利用机器学习模型生成数据预测和洞察的工具和资源。 将机器学习分析摄取到启用了[!DNL Profile]的数据集时，还会将该相同数据作为[!DNL Profile]记录摄取，然后可以使用[!DNL Adobe Experience Platform Segmentation Service]对其进行分段。

分段过程取决于受众的评估方法。 如果受众配置为&#x200B;**流式传输**，它将实时处理模型写入配置文件的所有新更新。 但是，如果为&#x200B;**批次**&#x200B;评估配置了受众，则将在下一个批次中评估新值。

此文档提供指向教程的链接，这些教程使您能够用机器学习见解扩充[!DNL Real-Time Customer Profile]。

## 快速入门

要完成下面的教程，您需要对摄取[!DNL Profile]数据和创建受众有一定的了解。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据，为每个单独的客户提供完整、统一的表示形式。
- [[!DNL Identity Service]](../../identity-service/home.md)：通过桥接被摄取到Experience Platform中的不同数据源中的标识来启用[!DNL Real-Time Customer Profile]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。

除了上述文档之外，还强烈建议您查看有关架构和架构编辑器的以下指南：

- [架构组合的基础知识](../../xdm/schema/composition.md)：描述用于组合要在[!DNL Experience Platform]中使用的架构的XDM架构、构建块、原则和最佳实践。
- [架构编辑器教程](../../xdm/tutorials/create-schema-ui.md)：提供了有关在[!DNL Experience Platform]中使用架构编辑器创建架构的详细说明。

## 创建和配置输出架构和数据集 {#create-an-output-schema-and-dataset}

使用得分见解丰富[!DNL Real-Time Customer Profile]的第一步是了解您的数据定义的真实对象（如人员）。 了解数据使您能够描述和设计结构以添加含义，就像设计关系数据库一样。

架构的合成从指定类开始。 类定义架构将包含的数据的行为方面（记录或时间序列）。 要开始创建自己的架构，请按照教程中有关[使用架构编辑器创建架构](../../xdm/tutorials/create-schema-ui.md)的步骤操作。 请注意，在为[!DNL Profile]启用数据集之前，您需要配置数据集的架构以使其具有主标识字段，然后为[!DNL Profile]启用架构。 当数据被摄取到启用了[!DNL Profile]的数据集时，同样的数据也会被摄取为[!DNL Profile]条记录。

如果您希望改用[!DNL Schema Registry] API编写架构，请先阅读[[!DNL Schema Registry] 开发人员指南](../../xdm/api/getting-started.md)，然后再尝试阅读有关[使用API创建架构](../../xdm/tutorials/create-schema-api.md)的教程。

准备好架构和数据集后，您可以使用适当的模型执行评分运行，从而生成评分数据并将其摄取到数据集。

## 使用[!DNL Segment Builder]创建受众 {#create-audiences-using-the-segment-builder}

生成评分数据洞察并将其引入启用了[!DNL Profile]的数据集后，即可使用[!DNL Segment Builder]创建动态受众。

[!DNL Segment Builder]提供了一个丰富的工作区，允许您与[!DNL Profile]数据元素进行交互。 工作区为构建和编辑规则提供了直观的控件，例如用于表示数据属性的拖放图块。 请按照[[!DNL Segment Builder] 用户指南](../../segmentation/ui/segment-builder.md)了解以下内容：

- 将属性、事件和现有受众的组合用作构建块来创建区段定义。
- 使用规则生成器画布和容器控制受众规则的执行顺序。
- 查看潜在受众的估计，允许您根据需要调整区段定义。
- 为计划分段启用所有区段定义。
- 为流式分段启用指定的区段定义。

## 后续步骤 {#next-steps}

要了解有关受众和[!DNL Segment Builder]的更多信息，请阅读[分段服务概述](../../segmentation/home.md)。

若要了解有关[!DNL Real-Time Customer Profile]的更多信息，请阅读[实时客户个人资料概述](../../profile/home.md)
