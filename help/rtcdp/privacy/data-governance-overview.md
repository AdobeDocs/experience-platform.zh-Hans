---
keywords: 数据治理rtcdp；rtcdp数据治理；实时客户数据配置文件数据治理
title: 数据治理概述
description: 数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Real-Time CDP中的数据治理

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)将来自多个企业系统的数据汇集在一起，使营销人员能够更好地识别、理解和吸引其客户。 贵组织或法律法规可能会对此数据设置使用限制。因此，在处理您的数据时，请务必确保Real-Time CDP符合使用策略。

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在Real-Time CDP中起着关键作用，允许您定义使用策略，根据这些策略对数据分类，并在执行某些营销操作时检查策略违规。

Real-Time CDP基于Adobe Experience Platform而构建，因此[!DNL Experience Platform]文档涵盖了大多数数据管理功能。 本文档旨在补充[!DNL Experience Platform]的[数据管理概述](../../data-governance/home.md)，并概述了Real-Time CDP中可用的管理功能。 涵盖以下主题：

* [将使用标签应用于您的数据](#labels)
* [管理数据使用策略](#policies)
* [强制数据使用合规性](#enforce)

## 将使用标签应用于您的数据 {#labels}

数据管理允许您在数据集或数据集字段级别将使用标签应用于数据。 数据使用标签允许您根据应用于数据的使用策略将数据分类。

有关使用数据使用标签的详细信息，请参阅Adobe Experience Platform的[数据使用标签用户指南](../../data-governance/labels/overview.md)。

## 配置目标的营销操作 {#destinations}

您可以通过定义目标的营销操作（也称为营销用例），在该目标上设置数据使用限制。 目标的营销操作指示要导出到该目标的数据的意图。

>[!NOTE]
>
>有关营销操作及其在数据使用策略中的使用的更多信息，请参阅[!DNL Experience Platform]文档中的[数据使用策略概述](../../data-governance/policies/overview.md)。

通过在目标上定义营销操作，您可以确保发送到这些目标的任何用户档案或受众都符合数据使用策略。 因此，您应根据组织对激活实施策略限制的需要，向目标添加适当的营销操作。

只有在首次设置目标时才能选择营销操作。 根据您使用的目标类型，配置营销操作的机会将显示在设置工作流的不同位置。 有关如何配置特定目标的步骤，请参阅[目标文档](../destinations/overview.md)。

## 管理数据使用策略 {#policies}

为了使数据使用标签有效地支持数据合规性，必须定义和启用数据使用策略。 数据使用策略是描述允许或限制您对Real-Time CDP中的数据执行的营销操作类型的规则。 有关详细信息，请参阅[!DNL Experience Platform] [数据管理概述](../../data-governance/home.md)中的“数据使用策略”部分。

Adobe Experience Platform为常见的客户体验用例提供了几个核心策略。 通过导航到&#x200B;**[!UICONTROL 策略]**&#x200B;工作区并选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，可以在UI中查看这些策略。 有关在UI中使用策略的更多详细步骤，包括如何创建自己的自定义策略，请参阅[!DNL Experience Platform]文档中的[策略用户指南](../../data-governance/policies/user-guide.md)。

## 强制数据使用合规性 {#enforce}

标记数据并定义使用策略后，您可以强制实施符合策略的数据使用。 在Real-Time CDP中将受众激活到目标时，数据管理会在发生任何违规时自动强制实施使用策略。

有关详细信息，请参阅[自动策略实施](../../data-governance/enforcement/auto-enforcement.md)文档。

## 后续步骤

现在您已经了解了Real-Time CDP上的关键数据管理功能以及[!DNL Experience Platform]如何启用它们，请继续查看[有关Adobe Experience Platform上的数据管理文档](../../data-governance/home.md)。 本文档概述了基本的数据管理概念，以及管理数据使用标签和策略的分步工作流程。

以下视频概述了Real-Time CDP中的数据治理，包括在目标上使用营销用例，以及不同场景的示例工作流：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
