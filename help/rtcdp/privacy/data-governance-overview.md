---
keywords: 数据管理rtcdp;rtcdp数据管理；实时客户数据配置文件数据管理
title: 数据管理概述
description: '通过“数据管理”，您可以管理客户数据，并确保符合适用于数据使用的法规、限制和策略。 '
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# 实时CDP中的数据管理

[!DNL Real-time Customer Data Platform] （实时CDP）将多个企业系统的数据整合在一起，使营销人员能够更好地识别、了解和吸引其客户。 此数据可能受贵组织或法律法规定义的使用限制的约束。 因此，在处理数据时务必确保实时CDP符合使用策略。

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和政策。 它在实时CDP中发挥着关键作用，允许您定义使用策略，根据这些策略对数据进行分类，并在执行某些营销操作时检查是否存在违反策略的情况。

Real-time CDP是以Adobe Experience Platform为基础构建的，因此，大多数数据管理功能都在 [!DNL Experience Platform] 文档。 本文档旨在补充 [数据管理概述](../../data-governance/home.md) 表示 [!DNL Experience Platform]，并概述了Real-time CDP中提供的管理功能。 涵盖以下主题：

* [将使用情况标签应用于数据](#labels)
* [管理数据使用策略](#policies)
* [强制数据使用合规性](#enforce)

## 将使用情况标签应用于数据 {#labels}

“数据管理”允许您在数据集或数据集字段级别将使用情况标签应用于数据。 数据使用标签允许您根据应用于该数据的使用策略对数据进行分类。

有关使用数据使用标签的详细信息，请参阅 [数据使用标签用户指南](../../data-governance/labels/overview.md) Adobe Experience Platform。

## 为目标配置营销操作 {#destinations}

您可以通过为目标定义营销操作（也称为营销用例）来设置目标的数据使用限制。 目标的营销操作指示要导出到该目标的数据的意图。

>[!NOTE]
>
>有关营销操作及其在数据使用策略中的用法的更多信息，请参阅 [数据使用策略概述](../../data-governance/policies/overview.md) 在 [!DNL Experience Platform] 文档。

通过在目标上定义营销操作，可确保发送到这些目标的任何用户档案或区段均符合数据使用策略。 因此，您应根据贵组织对激活实施策略限制的需求，向目标添加适当的营销操作。

只有在首次设置目标时，才能选择营销操作。 根据您所使用的目标类型，配置营销操作的机会将显示在设置工作流中的不同位置。 请参阅 [目标文档](../destinations/overview.md) 以了解有关如何配置特定目标的步骤。

## 管理数据使用策略 {#policies}

为了有效支持数据合规性的数据使用标签，必须定义并启用数据使用策略。 数据使用策略是描述您允许在实时CDP中对数据执行或限制执行的营销操作类型的规则。 请参阅 [!DNL Experience Platform] [数据管理概述](../../data-governance/home.md) 以了解更多信息。

Adobe Experience Platform为常见客户体验用例提供了多项核心策略。 可通过导航到 **[!UICONTROL 策略]** 工作区和选择 **[!UICONTROL 浏览]** 选项卡。 请参阅 [策略用户指南](../../data-governance/policies/user-guide.md) 在 [!DNL Experience Platform] 文档提供了有关在UI中使用策略的更多详细步骤，包括如何制定您自己的自定义策略。

## 强制数据使用合规性 {#enforce}

在标记数据并定义使用策略后，您可以强制数据使用符合策略。 在实时CDP中将受众区段激活到目标时，“数据管理”会在发生任何违规时自动强制实施使用策略。

请参阅 [自动策略执行](../../data-governance/enforcement/auto-enforcement.md) 以了解更多信息。

## 后续步骤

现在，您已经介绍了Real-time CDP上的关键数据管理功能以及如何 [!DNL Experience Platform] 启用，请继续 [有关Adobe Experience Platform上的数据管理文档](../../data-governance/home.md). 本文档概述了基本的“数据管理”概念，以及用于管理数据使用标签和策略的分步工作流程。

以下视频概述了实时CDP中的数据管理，包括对目标的营销用例的使用以及不同情景的工作流示例：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
