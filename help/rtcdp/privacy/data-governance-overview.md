---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: 数据管理概述
seo-title: 实时客户数据平台中的数据治理
description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
seo-description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# [!DNL Data Governance] 实时CDP中

[!DNL Real-time Customer Data Platform] （实时CDP）将来自多个企业系统的数据整合在一起，使营销人员能够更好地识别、理解和吸引客户。此数据可能受组织或法律法规定义的使用限制的约束。 因此，在处理数据时，务必确保实时CDP符合使用策略。

Adobe Experience Platform[!DNL Data Governance]允许您管理客户数据并确保符合适用于数据使用的法规、限制和政策。 它在实时CDP中起着关键作用，允许您定义使用策略，根据这些策略对数据进行分类，并在执行某些营销操作时检查是否存在违反策略的情况。

实时CDP构建在Adobe Experience Platform之上，因此[!DNL Experience Platform]文档中涵盖了大部分[!DNL Data Governance]功能。 本文档旨在补充[[!DNL Experience Platform]的&lt;a0/>数据治理概述](../../data-governance/home.md)，并概述实时CDP中提供的治理功能。 涵盖下列主题：

* [将使用标签应用于您的数据](#labels)
* [管理数据使用策略](#policies)
* [强制实施数据使用合规性](#enforce)

## 将使用标签应用于数据{#labels}

[!DNL Data Governance] 允许您在数据集或数据集字段级别将使用标签应用于数据。数据使用标签允许您根据适用于该数据的使用策略对数据进行分类。

有关使用数据使用标签的详细信息，请参阅[数据使用标签用户指南](../../data-governance/labels/overview.md) forAdobe Experience Platform。

## 为目标{#destinations}配置营销用例

您可以通过为目标定义营销用例（也称为营销活动）来设置目标的数据使用限制。 目标的市场营销用例指明将导出到该目标的数据的用途。

>[!NOTE]
>
>有关营销操作及其在数据使用策略中的使用的详细信息，请参阅[!DNL Experience Platform]文档中的[数据使用策略概述](../../data-governance/policies/overview.md)。

在目标上定义营销使用案例，可确保发送到这些目标的任何用户档案或区段均符合数据使用策略。 因此，您应根据组织对激活实施策略限制的需要，向您的目标添加适当的营销使用案例。

只有在首次设置目标时，才能选择市场营销用例。 根据您所处理的目标类型，配置营销用例的机会将显示在设置工作流的不同位置。 有关如何配置特定目标的步骤，请参见[目标文档](../destinations/overview.md)。

## 管理数据使用策略{#policies}

为了使数据使用标签能够有效支持数据合规性，必须定义并启用数据使用策略。 数据使用策略是描述您允许在实时CDP内对数据执行的或从中限制的营销操作种类的规则。 有关详细信息，请参阅[!DNL Experience Platform] [数据治理概述](../../data-governance/home.md)中的“数据使用策略”部分。

Adobe Experience Platform为常见客户体验使用案例提供了若干核心策略。 通过导航到&#x200B;**[!UICONTROL 策略]**&#x200B;工作区并选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，可以在UI中查看这些策略。 有关在UI中使用策略的更详细步骤，请参阅[!DNL Experience Platform]文档中的[策略用户指南](../../data-governance/policies/user-guide.md)，包括如何制定您自己的自定义策略。

## 强制符合数据使用情况{#enforce}

在标记数据并定义使用策略后，您可以强制数据使用符合策略。 在实时CDP中将受众段激活到目标时， [!DNL Data Governance]会在发生任何违规时自动实施使用策略。

有关详细信息，请参阅[自动策略实施](../../data-governance/enforcement/auto-enforcement.md)上的文档。

## 后续步骤

现在，您已经介绍了Real-time CDP上的关键[!DNL Data Governance]功能以及[!DNL Experience Platform]如何启用这些功能，请继续阅读Adobe Experience Platform](../../data-governance/home.md)上的[数据治理文档。 本文档提供基本[!DNL Data Governance]概念的概述，以及用于管理数据使用标签和策略的分步工作流。

以下视频概述了实时CDP中的[!DNL Data Governance]，包括对目标和不同场景的示例工作流的营销用例的使用：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)