---
keywords: Experience Platform；主页；热门主题；策略执行；自动执行；基于API的执行；数据管理
solution: Experience Platform
title: 自动策略实施
topic-legacy: guide
description: 本文档介绍了在将区段激活到Experience Platform中的目标时如何自动强制实施数据使用策略。
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: ca35b1780db00ad98c2a364d45f28772c27a4bc3
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# 自动策略执行

在标记数据并定义使用策略后，您可以强制数据使用符合策略。 在将受众区段激活到目标时，如果发生任何违规，Adobe Experience Platform会自动实施使用策略。

## 先决条件

本指南要求您对自动执行中涉及的平台服务有一定的了解。 在继续阅读本指南之前，请参阅以下文档以了解更多信息：

* [Adobe Experience Platform数据管理](../home.md):平台通过使用标签和策略来强制遵守数据使用规定的框架。
* [实时客户资料](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):中的分段引擎 [!DNL Platform] 用于根据客户行为和属性从客户配置文件创建受众区段。
* [目标](../../destinations/home.md):目标是与常用应用程序的预建集成，允许从平台无缝激活数据，以实现跨渠道营销活动、电子邮件促销活动、定向广告等。

## 执行流程 {#flow}

下图说明了如何将策略实施集成到区段激活的数据流中：

![](../images/enforcement/enforcement-flow.png)

首次激活区段时， [!DNL Policy Service] 根据以下因素检查适用的策略：

* 应用于要激活的区段中的字段和数据集的数据使用标签。
* 目标的营销目的。
<!-- * (Beta) The profiles that have consented to be included in the segment activation, based on your configured consent policies. -->

>[!NOTE]
>
>如果数据使用标签仅应用于数据集（而非整个数据集）中的某些字段，则仅在以下条件下才会对激活强制执行这些字段级别标签：
>
>* 区段定义中使用了这些字段。
>* 这些字段配置为目标目标的投影属性。


## 数据谱系 {#lineage}

数据谱系在平台中如何强制实施策略方面起着关键作用。 一般而言，数据谱系是指一组数据的来源，以及随着时间推移（或其移动的位置）发生的情况。

在“数据管理”上下文中，沿袭允许数据使用标签从数据集传播到使用其数据的下游服务，如实时客户资料和目标。 这允许在数据通过平台的历程中的几个关键点评估和强制执行策略，并为数据使用者提供关于为何发生策略违规的上下文。

在Experience Platform中，策略执行涉及以下血统：

1. 数据将被摄取到平台中并存储在 **数据集**.
1. 根据 **合并策略**.
1. 用户档案组分为 **区段** 基于常用属性。
1. 区段激活到下游 **目标**.

上述时间线中的每个阶段都表示一个实体，该实体可能会导致违反的策略，如下表所述：

| 数据谱系阶段 | 在策略执行中的作用 |
| --- | --- |
| 数据集 | 数据集包含数据使用情况标签（在数据集或字段级别应用），这些标签定义了整个数据集或特定字段可用于的用例。 如果某个数据集或包含某些标签的字段用于策略限制的目的，则会发生策略违规。 |
| 合并策略 | 合并策略是Platform用来确定在合并多个数据集中的片段时如何按优先级排列数据的规则。 如果您配置了合并策略，以便将具有受限标签的数据集激活到目标，则会发生策略违规。 请参阅 [合并策略概述](../../profile/merge-policies/overview.md) 以了解更多信息。 |
| 区段 | 区段规则定义应从客户配置文件中包含的属性。 根据区段定义包含的字段，区段将继承这些字段应用的所有使用情况标签。 如果您激活的区段继承的标签受目标目标目标的适用策略（基于其营销用例）的限制，则会发生策略违规。 |
| 目标 | 在设置目标时，可以定义营销操作（有时称为营销用例）。 此用例与策略中定义的营销操作关联。 换言之，您为目标定义的营销用例决定了哪些数据使用策略和同意策略适用于该目标。 如果激活的区段的使用标签受目标目标目标适用策略的限制，则会发生策略违规。 |
<!-- | Dataset | Datasets contain data usage labels (applied at the dataset or field level) that define which use cases the entire dataset or specific fields can be used for. Policy violations will occur if a dataset or field containing certain labels is used for a purpose that a policy restricts.<br><br>Any consent attributes collected from your customers are also stored in datasets. If you have access to [consent policies](../policies/user-guide.md#consent-policy) (currently in beta), any profiles that do not meet the consent attribute requirements of your policies will be excluded from segments that are activated to a destination. | -->
<!-- | Segment | Segment rules define which attributes should be included from customer profiles. Depending on which fields a segment definition includes, the segment will inherit any applied usage labels for those fields. Policy violations will occur if you activate a segment whose inherited labels are restricted by the target destination's applicable policies, based on its marketing use case. | -->

>[!IMPORTANT]
>
>某些数据使用策略可能指定具有AND关系的两个或多个标签。 例如，如果标签为营销活动，则策略可能会限制该活动 `C1` 和 `C2` 都存在，但如果只存在其中一个标签，则不会限制相同的操作。
>
>在自动强制实施方面，数据管理框架不考虑将单独的区段作为数据组合激活到目标。 因此，示例 `C1 AND C2` 策略 **NOT** 如果这些标签包含在单独的区段中，则会强制执行。 相反，仅当激活时同一区段中同时存在两个标签时，才会强制执行此策略。

当发生策略违规时，UI中显示的生成消息将提供有用的工具，用于探索违规的贡献数据谱系，以帮助解决此问题。 下一节将提供更多详细信息。

## 策略违规消息 {#enforcement}

<!-- (TO INCLUDE FOR PHASE 2)
The sections below outline the different policy enforcement messages that appear in the Platform UI:

* [Data usage policy violation](#data-usage-violation)
* [Consent policy evaluation](#consent-policy-evaluation)

### Data usage policy violation {#data-usage-violation} -->

如果发生策略违规，无法尝试激活区段(或 [对已激活的区段进行编辑](#policy-enforcement-for-activated-segments))操作被阻止，并出现一个弹出窗口，指示违反了一个或多个策略。 触发违规后， **[!UICONTROL 保存]** 按钮将被禁用，直到相应的组件更新以符合数据使用策略为止。

在弹出窗口的左列中选择一个策略违规，以显示该违规的详细信息。

![](../images/enforcement/violation-policy-select.png)

违规消息提供了所违反的策略的摘要，包括策略配置要检查的条件、触发违规的具体操作以及问题的可能解决方案列表。

![](../images/enforcement/violation-summary.png)

违规摘要下方会显示数据谱系图，以便显示与策略违规相关的数据集、合并策略、区段和目标。 图表中会突出显示您当前更改的实体，以指示流程中的哪个点导致违规发生。 您可以在图形中选择实体名称，以打开相关实体的详细信息页面。

![](../images/enforcement/data-lineage.png)

您还可以使用 **[!UICONTROL 过滤器]** 图标(![](../images/enforcement/filter.png))以按类别筛选显示的实体。 要显示数据，必须至少选择两个类别。

![](../images/enforcement/lineage-filter.png)

选择 **[!UICONTROL 列表视图]** 将数据谱系显示为列表。 要切换回可视图表，请选择 **[!UICONTROL 路径查看]**.

![](../images/enforcement/list-view.png)

<!-- (TO INCLUDE FOR PHASE 2)
### Consent policy evaluation (Beta) {#consent-policy-evaluation}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

If you have [created consent policies](../policies/user-guide.md#consent-policy) and are activating a segment to a destination, you can see how your consent policies will affect the percentage of profiles that will be included in the activation.

Once you reach at the **[!UICONTROL Review]** step in the [activation workflow](../../destinations/ui/activation-overview.md), select **[!UICONTROL View applied policies]**.

A policy check dialog appears, showing you a preview of how your consent policies affect the addressable audience of the activated segment.
 -->

## 对激活的区段执行策略 {#policy-enforcement-for-activated-segments}

策略实施仍适用于激活区段后的区段，从而限制对区段或其目标所做的任何更改，从而导致策略违规。 因为 [数据谱系](#lineage) 在策略实施中，以下任何操作都可能会触发违规：

* 更新数据使用情况标签
* 更改区段的数据集
* 更改区段谓词
* 更改目标配置

如果上述任何操作触发违规，将阻止保存该操作并显示策略违规消息，从而确保激活的区段在修改时继续遵守数据使用策略。

## 后续步骤

本文档介绍了自动策略执行在Experience Platform中的工作方式。 有关如何使用API调用以编程方式将策略实施集成到应用程序中的步骤，请参阅 [基于API的执行](./api-enforcement.md).
