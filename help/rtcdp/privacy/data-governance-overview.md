---
title: 数据管理概述
seo-title: 实时客户数据平台中的数据治理
description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
seo-description: '数据管理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 '
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---


# 实时CDP中的数据管理

实时客户数据平台(Real-time CDP)将多个企业系统的数据整合在一起，使营销人员能够更好地识别、理解和吸引客户。 此数据可能受组织或法律法规定义的使用限制的约束。 因此，在处理数据时，务必确保实时CDP符合使用策略。

Adobe Experience Platform数据管理允许您管理客户数据并确保符合适用于数据使用的法规、限制和政策。 它在实时CDP中起着关键作用，允许您定义使用策略，根据这些策略对数据进行分类，并在执行某些营销操作时检查是否存在违反策略的情况。

实时CDP构建在Adobe Experience Platform的基础上，因此Experience Platform文档中涵盖了大多数数据管理功能。 本文档旨在补充Experience Platform的 [“数据治理](../../data-governance/home.md) ”概述，并概述实时CDP中提供的“治理”功能。 涵盖下列主题：

* [将使用标签应用于您的数据](#labels)
* [管理数据使用策略](#policies)
* [强制实施数据使用合规性](#enforcement)

## 将使用标签应用于您的数据 {#labels}

Data Governance允许您在数据集或数据集字段级别对数据应用使用标签。 数据使用标签允许您根据适用于该数据的使用策略对数据进行分类。

有关使用数据使用标签的详细信息，请参 [阅适用于Adobe Experience Platform的数据使用](../../data-governance/labels/overview.md) 标签用户指南。

## 设置目标限制

您可以通过为目标定义市场营销用例来设置目标的数据使用限制。 定义目标的使用案例允许您检查是否存在使用策略违规，并确保发送到该目标的任何用户档案或区段均与数据管理规则兼容。

市场营销用例可以在编辑目标工作 _流的_ “设置” _阶段定义_ 。 有关详细信息，请参阅目标文档。


## 管理数据使用策略 {#policies}

为了使数据使用标签能够有效支持数据合规性，必须定义并启用数据使用策略。 数据使用策略是描述您允许在实时CDP内对数据执行的或从中限制的营销操作种类的规则。 有关详细信息，请参阅Experience Platform数据管理概述 [中的“数据使用策](../../data-governance/home.md) 略”部分。

Adobe Experience Platform为常见客户 **体验使用** 案例提供了多个核心策略。 通过向DULE Policy Service API发出请 [求可查看这些策略](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)，如Policy Service Developer Guide中的“列表所有策 [略”部分所示](../../data-governance/policies/overview.md)。 您还可以创建自己的自 **定义策略** ，以模拟自定义使用限制，如开发人员指南的“创建策略”部分所示。

## （测试版）强制数据使用合规性 {#enforce-data-usage-compliance}

>[!IMPORTANT]
>此功能当前为测试版，并非所有用户都可使用。 可以根据请求启用它。 文档和功能可能会发生变化。

在标记数据并定义使用策略后，您可以强制数据使用符合策略。 在实时CDP中将受众段激活到目标时，如果发生任何违规行为，数据管理将自动实施使用策略。

下图说明如何将策略实施集成到区段激活的数据流中：

![](assets/enforcement-flow.png)

在首次激活区段时，DULE策略服务会根据以下因素检查是否存在违反策略的情况：

* 应用于要激活的区段中的字段和数据集的数据使用标签。
* 目标的营销目的。

### 策略违规消息 {#enforcement}

如果策略违规无法尝试激活区段(或对已激 [活的区段进行编辑](#policy-enforcement-for-activated-segments))，则会阻止该操作，并显示一个弹出窗口，指示已违反一个或多个策略。 在弹出窗口的左列中选择策略违规，以显示该违规的详细信息。

![](assets/violation-popover.png)

弹出窗口的“详 *细信息* ”选项卡指示触发违规的操作以及发生违规的原因，并提供有关如何潜在解决该问题的建议。

单 **击“数据谱系** ”以跟踪其数据标签触发违规的目标、区段、合并策略或数据集。

![](assets/data-lineage.png)

触发违规后，激活 **将禁** 用“保存”按钮，直到相应组件更新以符合数据使用策略。

### 对激活的区段实施策略 {#policy-enforcement-for-activated-segments}

策略实施仍适用于激活区段后的区段，从而限制对区段或其目标的任何更改，这会导致策略违规。 由于将区段激活到目标涉及大量组件，以下任何操作都可能触发违规：

* 更新数据使用标签
* 更改区段的数据集
* 更改段谓词
* 更改目标配置

如果上述任何操作触发违规，则会阻止保存该操作并显示策略违规消息，从而确保激活的区段在被修改时继续遵守数据使用策略。

## 后续步骤

现在，您已经介绍了实时CDP上的主要数据管理功能以及Experience Platform如何支持这些功能，请继续阅读Adobe [Experience Platform上的数据管理文档](../../data-governance/home.md)。 本文档概述了基本的“数据管理”概念，以及管理数据使用标签和策略的分步工作流。

以下视频概述了实时CDP中的工作流治理，包括在目标上使用营销用例以及针对不同情景使用示例：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)