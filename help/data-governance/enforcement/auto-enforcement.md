---
keywords: Experience Platform；主页；热门主题；策略实施；自动实施；基于API的实施；数据治理
solution: Experience Platform
title: 自动策略实施
description: 本文档介绍了在将受众激活到Experience Platform中的目标时，如何自动实施数据使用策略。
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 0%

---

# 自动策略实施

>[!IMPORTANT]
>
>自动策略实施仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**.

在标记数据并定义数据使用策略后，您可以强制实施符合策略的数据使用。 将受众激活到目标时，Adobe Experience Platform会在发生任何违规时自动实施使用策略。

>[!NOTE]
>
>本文档重点介绍数据治理和同意政策的执行情况。 有关访问控制策略的信息，请参阅有关以下内容的文档： [基于属性的访问控制](../../access-control/abac/overview.md).

## 先决条件

本指南需要深入了解自动实施中涉及的Platform服务。 在继续阅读本指南之前，请参阅以下文档以了解更多信息：

* [Adobe Experience Platform数据管理](../home.md)：Platform通过使用标签和策略来强制实现数据使用合规性的框架。
* [Real-time Customer Profile](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)：内的分段引擎 [!DNL Platform] 用于根据客户行为和属性从客户配置文件创建受众。
* [目标](../../destinations/home.md)：目标是与常用应用程序预建的集成，允许从Platform无缝激活数据，用于跨渠道营销活动、电子邮件活动、定向广告等。

## 实施流程 {#flow}

下图说明了如何将策略实施集成到受众激活的数据流中：

![说明如何将策略实施集成到受众激活的数据流中。](../images/enforcement/enforcement-flow.png)

首次激活受众时， [!DNL Policy Service] 根据以下因素检查适用的策略：

* 应用于要激活受众中的字段和数据集的数据使用标签。
* 目标的营销目的。
* 根据您配置的同意策略，同意包含在受众激活中的用户档案。

>[!NOTE]
>
>如果有数据使用标签仅应用于数据集内的某些字段（而不是整个数据集），则仅在以下条件下实施这些字段级别的激活标签：
>
>* 这些字段在受众中使用。
>* 这些字段配置为目标目标的投影属性。

## 数据谱系 {#lineage}

数据谱系对于如何在Platform中实施策略起着关键作用。 一般而言，数据谱系是指一组数据的起源，以及随着时间推移对一组数据会发生（或移动到何处）什么。

在数据治理的上下文中，谱系使数据使用标签能够从架构传播到使用其数据的下游服务，例如实时客户档案和目标。 这允许在数据通过Platform的历程中的几个关键点评估和执行策略，并向数据使用者提供有关策略冲突发生原因的上下文。

在Experience Platform，政策的执行涉及以下血统：

1. 数据被摄取到Platform并存储在 **数据集**.
1. 客户配置文件是通过根据 **合并策略**.
1. 用户档案组分为 **受众** 基于通用属性。
1. 受众被激活到下游 **目标**.

上述时间轴中的每个阶段都表示一个可能有助于策略实施的实体，如下表所示：

| 数据谱系阶段 | 在策略执行中的作用 |
| --- | --- |
| 数据集 | 数据集包含数据使用标签（在架构字段级别或整个数据集级别应用），这些标签定义整个数据集或特定字段可用于哪些用例。 如果包含特定标签的数据集或字段用于策略限制的目的，则会发生策略违规。<br><br>从客户处收集的任何同意属性也存储在数据集中。 如果您有权访问同意策略，则任何不符合策略的同意属性要求的配置文件都将从激活到目标的受众中排除。 |
| 合并策略 | 合并策略是Platform用来确定在将来自多个数据集的片段合并到一起时数据优先顺序的规则。 如果将合并策略配置为将带有受限标签的数据集激活到目标，则会发生策略违规。 请参阅 [合并策略概述](../../profile/merge-policies/overview.md) 了解更多信息。 |
| Audience | 分段规则定义应从客户配置文件中包含哪些属性。 根据区段定义包含哪些字段，受众将继承这些字段的任何应用使用标签。 如果您激活的受众的继承标签受目标目标的适用策略限制（基于其营销用例），则会发生策略违规。 |
| 目标 | 在设置目标时，可以定义营销操作（有时称为营销用例）。 此用例与策略中定义的营销操作相关联。 换言之，您为目标定义的营销操作确定哪些数据使用策略和同意策略适用于该目标。<br><br>如果激活的使用标签受限于目标目标的营销操作的受众，则会发生数据使用策略违规。<br><br>（测试版）激活受众后，任何不包含营销操作（由您的同意政策定义）所需的同意属性的用户档案都将从激活的受众中排除。 |

>[!IMPORTANT]
>
>某些数据使用策略可能会指定两个或多个具有AND关系的标签。 例如，如果存在标签，策略可以限制营销操作 `C1` 和 `C2` 都存在，但只要存在其中一个标签，就不会限制相同的操作。
>
>在自动实施方面，数据管理框架不会将单独的受众激活到目标作为数据的组合。 因此，示例 `C1 AND C2` 策略是 **NOT** 如果这些标签包含在单独的受众中，则强制实施。 相反，仅当激活时同一受众中同时存在两个标签时，才强制执行此策略。

当发生策略违规时，UI中显示的结果消息提供了有用的工具，可用于探索违规的贡献数据谱系以帮助解决问题。 下一节将提供更多详细信息。

## 策略实施消息 {#enforcement}

以下各节概述了Platform UI中显示的不同策略实施消息：

* [数据使用策略违规](#data-usage-violation)
* [同意政策评估](#consent-policy-evaluation)

### 数据使用策略违规 {#data-usage-violation}

如果尝试激活受众时发生策略冲突(或 [对已激活的受众进行编辑](#policy-enforcement-for-activated-audiences))操作被阻止，并且出现弹出窗口，指示已违反一个或多个策略。 一旦触发违规， **[!UICONTROL 保存]** 在更新相应的组件以符合数据使用策略之前，对于您正在修改的实体，按钮处于禁用状态。

在弹出框的左列中选择策略违规以显示该违规的详细信息。

![](../images/enforcement/violation-policy-select.png)

违规消息提供了所违反的策略的摘要，包括配置策略以检查的条件、触发违规的特定操作以及问题的可能解决方案列表。

![](../images/enforcement/violation-summary.png)

数据族图显示在违规摘要下方，允许您可视化与策略违规相关的数据集、合并策略、受众和目标。 图形中会加亮当前更改的图元，指示流中哪个点导致发生违规。 可在图形内选择实体名称，以打开相关实体的详细信息页面。

![](../images/enforcement/data-lineage.png)

您还可以使用 **[!UICONTROL 筛选条件]** 图标(![](../images/enforcement/filter.png))以按类别筛选显示的实体。 必须至少选择两个类别才能显示数据。

![](../images/enforcement/lineage-filter.png)

选择 **[!UICONTROL 列表视图]** 将数据谱系显示为列表。 要切换回可视化图表，请选择 **[!UICONTROL 路径查看]**.

![](../images/enforcement/list-view.png)

### 同意政策评估 {#consent-policy-evaluation}

如果您拥有 [创建的同意政策](../policies/user-guide.md#consent-policy) 并且将受众激活到目标，您可以了解同意策略对激活中包含的用户档案百分比有何影响。

#### 付费媒体的同意策略增强 {#consent-policy-enhancement}

增强对的同意政策的执行 [批次](../../destinations/destination-types.md#file-based) 和 [流](../../destinations/destination-types.md#streaming-destinations) 已创建目标，包括付费媒体激活。 此增强功能适用于Privacy and Security Shield或Healthcare Shield的客户，并且会在同意状态发生变化时主动从批处理和流式处理目标中删除用户档案。 它还确保立即传播同意更改，以便始终定位正确的受众。

这些改进增强了营销策略的可信度，因为营销人员无需手动将同意属性添加到其区段表达式。 这可确保在撤销同意或不再符合同意策略条件后，不会无意中将任何用户档案定位到任何营销体验中。 现在，在下游解决方案的激活工作流中，会自动实施营销同意策略，该策略可设置有关如何跨各种营销工作流管理同意或偏好设置数据的规则。

>[!NOTE]
>
>由于此增强功能，UI没有变化。

#### 预激活评估

一旦您到达以下位置 **[!UICONTROL 审核]** 步骤时间 [激活目标](../../destinations/ui/activation-overview.md)，选择 **[!UICONTROL 查看应用的策略]**.

![在激活目标工作流中查看应用的策略按钮](../images/enforcement/view-applied-policies.png)

此时将显示策略检查对话框，其中预览了同意策略对已激活受众的同意受众有何影响。

![Platform UI中的同意策略检查对话框](../images/enforcement/consent-policy-check.png)

该对话框每次显示一个受众的同意受众。 要查看不同受众的策略评估，请使用图表上方的下拉菜单从列表中选择一个受众。

![策略检查对话框中的受众切换器。](../images/enforcement/audience-switcher.png)

使用左边栏可在所选受众的适用同意策略之间进行切换。 未选择的策略将在“[!UICONTROL 其他策略]”部分。

![策略检查对话框中的策略切换器](../images/enforcement/policy-switcher.png)

该图显示了三组配置文件之间的重叠：

1. 符合所选受众条件的配置文件
1. 符合所选同意策略的配置文件
1. 符合受众其他适用同意政策的用户档案(称为&quot;[!UICONTROL 其他策略]“（在图表中）

符合以上所有三个组资格的用户档案表示同意的受众，在右边栏中汇总。

![策略检查对话框中的“摘要”部分](../images/enforcement/summary.png)

将鼠标悬停在图中的某个受众上，可显示它包含的用户档案数。

![在策略检查对话框中突出显示图表部分](../images/enforcement/highlight-segment.png)

同意的受众由图的中心重叠部分表示，并且可以像其他部分一样突出显示。

![在图表中突出显示已同意的受众](../images/enforcement/consented-audience.png)

#### 流量运行实施

将数据激活到目标时，流运行详细信息会显示由于有效同意策略而被排除的身份数量。

![数据流运行的排除身份量度](../images/enforcement/dataflow-run-enforcement.png)

## 针对已激活受众的策略实施 {#policy-enforcement-for-activated-audiences}

策略实施仍然适用于激活后的受众，限制对受众或其目标所做的任何会导致策略违规的更改。 原因如下 [数据谱系](#lineage) 在策略实施中工作，以下任何操作都可能触发违规：

* 更新数据使用标签
* 更改受众的数据集
* 更改受众谓词
* 更改目标配置

如果以上任何操作触发了违规，则将阻止保存该操作并显示策略违规消息，从而确保激活的受众在修改时继续遵守数据使用策略。

## 后续步骤

本文档介绍了如何在Experience Platform中自动执行策略。 有关如何使用API调用以编程方式将策略实施集成到应用程序的步骤，请参阅以下指南： [基于API的实施](./api-enforcement.md).
