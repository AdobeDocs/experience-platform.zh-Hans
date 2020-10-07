---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: 数据管理概述
seo-title: 实时客户数据平台中的数据治理
description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
seo-description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
translation-type: tm+mt
source-git-commit: 259c26a9d3b6ef397acd552e255f68ecb25b2dd1
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---


# [!DNL Data Governance] 实时CDP中

[!DNL Real-time Customer Data Platform] （实时CDP）将来自多个企业系统的数据整合在一起，使营销人员能够更好地识别、理解和吸引客户。 此数据可能受组织或法律法规定义的使用限制的约束。 因此，在处理数据时，务必确保实时CDP符合使用策略。

Adobe Experience Platform [!DNL Data Governance] 允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 它在实时CDP中起着关键作用，允许您定义使用策略，根据这些策略对数据进行分类，并在执行某些营销操作时检查是否存在违反策略的情况。

实时CDP构建在Adobe Experience Platform之上，因此文档中 [!DNL Data Governance] 涵盖了大部分功 [!DNL Experience Platform] 能。 本文档旨在补充 [Data Governance概述](../../data-governance/home.md)[!DNL Experience Platform]，并概述实时CDP中提供的Governance功能。 涵盖下列主题：

* [将使用标签应用于您的数据](#labels)
* [管理数据使用策略](#policies)
* [强制实施数据使用合规性](#enforce-data-usage-compliance)

## 将使用标签应用于您的数据 {#labels}

[!DNL Data Governance] 允许您在数据集或数据集字段级别将使用标签应用于数据。 数据使用标签允许您根据适用于该数据的使用策略对数据进行分类。

有关使用数据使用标签的详细信息，请参 [阅Adobe Experience Platform数据使用标签](../../data-governance/labels/overview.md) 用户指南。

## 为目标配置营销用例 {#destinations}

您可以通过为目标定义营销用例（也称为营销活动）来设置目标的数据使用限制。 目标的市场营销用例指明将导出到该目标的数据的用途。

>[!NOTE]
>
>有关营销操作及其在数据使用策略中的使用的更多信息，请参 [阅文档中的数据使用策](../../data-governance/policies/overview.md) 略 [!DNL Experience Platform] 概述。

在目标上定义营销使用案例，可确保发送到这些目标的任何用户档案或区段均符合数据使用策略。 因此，您应根据组织对激活实施策略限制的需要，向您的目标添加适当的营销使用案例。

只有在首次设置目标时，才能选择市场营销用例。 根据您所处理的目标类型，配置营销用例的机会将显示在设置工作流的不同位置。 有关如何 [配置特定目标](../destinations/destinations-overview.md) ，请参阅目标文档。


## 管理数据使用策略 {#policies}

为了使数据使用标签能够有效支持数据合规性，必须定义并启用数据使用策略。 数据使用策略是描述您允许在实时CDP内对数据执行的或从中限制的营销操作种类的规则。 有关详细信息，请参阅“数据管理” [!DNL Experience Platform] 概 [述中的](../../data-governance/home.md) “数据使用策略”部分。

Adobe Experience Platform为常见客户体验使用案例提供了若干核心策略。 通过导航到“策略”工作区并选择“浏览”选 **[!UICONTROL 项卡]** ，可以在UI中 **[!UICONTROL 查看这些]** 策略。 有关在 [UI中使用策略](../../data-governance/policies/user-guide.md) (包括 [!DNL Experience Platform] 如何制定您自己的自定义策略)的更详细步骤，请参阅文档中的策略用户指南。

## 强制实施数据使用合规性 {#enforce-data-usage-compliance}

在标记数据并定义使用策略后，您可以强制数据使用符合策略。 在实时CDP中将受众段激活到目标时，如果发 [!DNL Data Governance] 生任何违规，将自动实施使用策略。

下图说明如何将策略实施集成到区段激活的数据流中：

![](assets/enforcement-flow.png)

首次激活区段时，会 [!DNL Policy Service] 根据以下因素检查是否存在违反策略的情况：

* 应用于要激活的区段中的字段和数据集的数据使用标签。
* 目标的营销目的。

>[!NOTE]
>
>如果激活集（而非整个数据集）中的某些字段只应用了数据使用标签，则只有在以下条件下才会对这些字段级别标签进行强制执行：
>* 这些字段用在段定义中。
>* 字段将配置为目标目标的预计属性。


### 策略违规消息 {#enforcement}

如果策略违规无法尝试激活区段(或对已激 [活的区段进行编辑](#policy-enforcement-for-activated-segments))，则会阻止该操作，并显示一个弹出窗口，指示已违反一个或多个策略。 在弹出窗口的左列中选择策略违规，以显示该违规的详细信息。

![](assets/violation-popover.png)

弹出窗口的“详 **[!UICONTROL 细信息]** ”选项卡指示触发违规的操作以及发生违规的原因，并提供有关如何潜在解决该问题的建议。

单 **[!UICONTROL 击“数据谱系]** ”以跟踪其数据标签触发违规的目标、区段、合并策略或数据集。

![](assets/data-lineage.png)

触发违规后，激活 **[!UICONTROL 将禁]** 用“保存”按钮，直到相应组件更新以符合数据使用策略。

### 对激活的区段实施策略 {#policy-enforcement-for-activated-segments}

策略实施仍适用于激活区段后的区段，从而限制对区段或其目标的任何更改，这会导致策略违规。 由于将区段激活到目标涉及大量组件，以下任何操作都可能触发违规：

* 更新数据使用标签
* 更改区段的数据集
* 更改段谓词
* 更改目标配置

如果上述任何操作触发违规，则会阻止保存该操作并显示策略违规消息，从而确保激活的区段在被修改时继续遵守数据使用策略。

## 后续步骤

现在，您已经介绍了实时CDP [!DNL Data Governance] 的主要功能以及如何 [!DNL Experience Platform] 启用这些功能，请继续阅读Adobe Experience Platform [数据管理文档](../../data-governance/home.md)。 文档概述了基本 [!DNL Data Governance] 概念，以及管理数据使用标签和策略的分步工作流。

以下视频概述了实时 [!DNL Data Governance] CDP的功能，包括在目标上的营销用例和针对不同情景的示例工作流的使用：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)