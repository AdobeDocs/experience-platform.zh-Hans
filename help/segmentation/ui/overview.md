---
keywords: Experience Platform；主页；热门主题；分段服务；分段；分段服务；用户指南；ui指南；分段ui指南；区段生成器；区段生成器；已实现；现有；退出；
solution: Experience Platform
title: Segmentation Service用户界面指南
description: Adobe Experience Platform Segmentation Service提供了一个用于创建和管理区段定义的用户界面。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '2650'
ht-degree: 3%

---

# Segmentation Service用户界面指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了用于创建和管理区段定义的用户界面。

## 快速入门

使用区段定义需要了解各种 [!DNL Experience Platform] 与分段相关的服务。 在阅读本用户指南之前，请查看文档以了解以下服务：

- [[!DNL Segmentation Service]](../home.md)： [!DNL Segmentation Service] 允许您划分存储于 [!DNL Experience Platform] 将个人（如客户、潜在客户、用户或组织）关联到较小的组中。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：通过桥接从被摄取到的不同数据源的身份，支持创建客户用户档案 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../../xdm/schema/best-practices.md).

了解本文档中使用的两个关键术语并了解它们之间的区别也很重要：
- **区段定义**：用于描述目标受众的关键特征或行为的规则集。
- **Audience**：符合区段定义标准的生成配置文件集。 可通过Adobe Experience Platform（平台生成的受众）或从外部源（外部生成的受众）创建受众。

## 概述

在Experience PlatformUI中，选择 **[!UICONTROL 区段]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡显示 [!UICONTROL 区段] 仪表板。

>[!NOTE]
>
>如果您的组织是初次使用Platform，但尚未创建活动配置文件数据集或合并策略，则 [!UICONTROL 区段] 仪表板不可见。 相反， [!UICONTROL 概述] 选项卡显示链接和文档，以帮助您开始使用区段。

### [!UICONTROL 区段] 仪表板 {#segments-dashboard}

此 **[!UICONTROL 区段]** 功能板概述了与贵组织的区段数据相关的关键量度。

要了解更多信息，请访问 [区段仪表板指南](../../dashboards/guides/segments.md).

![将显示区段仪表板。 它显示各种构件，包括受众规模、按身份划分的用户档案、身份叠加和受众规模变化趋势。](../../dashboards/images/segments/dashboard-overview.png)

## 浏览 {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="流失率"
>abstract="流失率表示与上次运行区段作业时相比，区段定义内正在更改的配置文件的百分比。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="评估方法"
>abstract="区段的评估方法包括批量评估、流式评估和边缘评估。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="将所有区段添加到计划"
>abstract="启用此项可在每日计划更新中包含所有批量评估区段。禁用此项可从计划更新中删除所有区段。"

选择 **[!UICONTROL 浏览]** 选项卡，查看组织的所有区段定义的列表。

![将显示区段浏览屏幕。 此时将显示属于组织的所有区段的列表。](../images/ui/overview/segment-browse-all.png)

此视图列出有关区段定义的信息，包括用户档案计数、创建日期和上次修改日期。

您可以通过选择向此显示添加其他字段 ![过滤器属性图标](../images/ui/overview/filter-attribute.png). 这些附加字段包括划分、评估方法和作业ID。

如果选择了“划分”，则显示区会显示一个条形图，其中概述了属于以下每种已计算用户档案状态的用户档案的百分比： [!UICONTROL 已实现] 和 [!UICONTROL 正在退出]. 此外，上显示的细分 [!UICONTROL 浏览] 选项卡是对区段状态最准确的划分。 如果此数字与 [!UICONTROL 概述] 选项卡中，您应使用 [!UICONTROL 浏览] 制表符作为正确的信息源，因为 [!UICONTROL 概述] 选项卡编号每天仅更新一次。

| 状态 | 描述 |
| ------ | ----------- |
| 已实现 | 过去24小时内符合区段资格的用户档案计数。 因此，自上次运行批处理区段作业以来，符合区段资格的用户档案数。 |
| 正在退出 | 过去24小时内退出区段的配置文件数。 因此，自上次运行批处理区段作业以来，不再符合区段资格的用户档案数。 |

评估方法可以是流式、批量或边缘。 当数据进入系统时，会不断评估流区段。 根据设定的计划评估批次区段。 将实时评估边缘区段，以允许使用相同的页面和下一页面个性化用例。

![区段浏览页面中的区段会高亮显示。](../images/ui/overview/segment-browse-segments.png)

页面顶部提供了一些选项，用于将所有区段添加到计划以及创建新区段。

切换 **[!UICONTROL 将所有区段添加到计划]** 将启用计划分段。 有关计划分段的更多信息，请参阅 [本用户指南的计划分段部分](#scheduled-segmentation).

选择 **[!UICONTROL 创建区段]** 会将您转到区段生成器。 要了解有关创建区段的更多信息，请阅读以下章节： [在用户指南中创建区段](#create-segment).

![区段浏览页面上的顶部导航栏会突出显示。 此栏包含一个用于向所有区段添加计划的切换开关和一个用于创建区段的按钮。](../images/ui/overview/segment-browse-top.png)

右侧边栏包含有关组织内所有区段的信息，其中列出了区段总数、上次评估日期、下次评估日期以及按评估方法划分的区段。

![区段浏览页面上的右侧边栏会高亮显示。 此时将显示有关组织中区段的信息。 这包括区段总数、上次评估时间、下次评估时间以及不同区段类型的划分等信息。](../images/ui/overview/segment-browse-segment-info.png)

选择区段定义的行可提供区段定义的摘要，其中包括编辑或删除区段、将区段激活到目标、区段的合格受众、总受众规模以及区段名称、描述、评估方法、创建日期和上次修改日期的选项。

>[!NOTE]
>
> 您将 **非** 能够删除目标激活中使用的区段。

![此时将显示有关选定区段的详细信息。 这包括有关合格配置文件数量的详细信息、合格配置文件与配置文件总数的百分比细分、上次评估日期。](../images/ui/overview/segment-browse-details.png)

## 区段定义详细信息 {#segment-details}

要查看有关特定区段定义的更多详细信息，请在 **[!UICONTROL 浏览]** 选项卡。

此时将显示区段详细信息页面。 顶部汇总了区段定义、有关合格受众规模的信息以及激活区段的目标。

![此时将显示区段定义详细信息页面。 区段摘要、区段中的受众总数以及激活的目标卡会突出显示。](../images/ui/overview/segment-details-summary.png)

### 区段摘要 {#segment-summary}

此 **[!UICONTROL 区段摘要]** 部分提供属性的ID、名称、描述和详细信息等信息。

此外，您还可以选择将区段激活到目标或编辑区段。 选择 **[!UICONTROL 激活到目标]** 将允许您激活区段到目标。 有关将区段激活到目标的更多详细信息，请阅读 [激活概述](../../destinations/ui/activation-overview.md).

![“激活到目标”按钮会突出显示。](../images/ui/overview/segment-details-activate.png)

选择 **[!UICONTROL 编辑区段]** 将带您进入 [!DNL Segment Builder]. 有关使用 [!DNL Segment Builder] 工作区，请阅读 [[!DNL Segment Builder] 用户指南](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### 区段中的受众总数

此 **[!UICONTROL 区段中的受众总数]** 部分显示符合区段资格的用户档案总数。

通过使用当天样本数据的样本大小来生成预估。 如果您的配置文件存储中的实体少于100万个，则使用完整数据集；对于100万到2,000万个之间的实体，使用100万个实体；而对于2,000万个以上的实体，使用总实体的5%。 有关产生分类估计之更多资料可参阅 [估算生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 区段创建教程的内容。

### 已激活的目标

此 **[!UICONTROL 已激活的目标]** 部分显示激活此区段的目标。

>[!NOTE]
>
> Destinations是一项功能，可用于 [!DNL Adobe Real-Time Customer Data Platform]，并允许您将数据导出到外部平台。 欲知目标的详情，请阅读 [目标概述](../../destinations/home.md). 要了解如何将区段激活到目标，请参阅 [激活概述](../../destinations/ui/activation-overview.md).

### 配置文件示例

下面是符合区段条件的配置文件采样，详细说明以下信息： [!DNL Profile] ID、名字、姓氏和个人电子邮件。

数据采样的触发方式取决于摄取方法。

对于批量摄取，每十五分钟自动扫描一次配置文件存储区，以查看自上次采样作业运行以来是否成功摄取了新批次。 如果是这种情况，随后扫描配置文件存储以查看记录数量是否至少有5%的变化。 如果满足这些条件，则会触发新的取样作业。

对于流式摄取，每小时自动扫描一次配置文件存储区，以查看记录数量是否至少有5%的更改。 如果满足此条件，则会触发新的取样作业。

扫描的样本大小取决于配置文件存储区中的实体总数。 下表显示了这些样本量：

| 配置文件存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 少于100万 | 完整数据集 |
| 100万到2000万 | 100万 |
| 超过2000万 | 占总数的5% |

有关每个报表包的更多详细信息 [!DNL Profile] 可以通过选择 [!DNL Profile] ID。 要了解有关用户档案的详细信息，请阅读 [[!DNL Real-Time Customer Profile] 用户指南](../../profile/ui/user-guide.md#profile-detail).

![区段定义的示例配置文件将突出显示。 示例配置文件信息包括配置文件ID、名字、姓氏和人员的电子邮件。](../images/ui/overview/segment-details-profiles.png)

## 创建区段 {#create-segment}

选择 **[!UICONTROL 创建区段]** 在右上角打开 [!DNL Segment Builder] 工作区，您可以在其中开始创建区段定义。

![在“区段浏览”页面上，“创建区段”按钮高亮显示。](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作区

[!DNL Segment Builder] 提供了一个丰富的工作区，允许您与 [!DNL Profile] 数据元素。 工作区为构建和编辑规则提供了直观的控件，例如用于表示数据属性的拖放图块。

有关使用 [!DNL Segment Builder] 工作区，请阅读 [[!DNL Segment Builder] 用户指南](./segment-builder.md).

![此时将显示区段生成器工作区。](../images/ui/overview/segment-builder.png)

## 计划分段 {#scheduled-segmentation}

创建区段定义后，您可以通过按需评估或计划（连续）评估来评估它们。 评估方式正在移动 [!DNL Real-Time Customer Profile] 数据区段定义，以便生成相应的受众。 创建受众后，将保存并存储这些受众，以便可以使用导出它们 [!DNL Experience Platform] API。

按需评估涉及使用API执行评估并根据需要构建受众，而计划评估（也称为“计划分段”）允许您创建循环计划来在特定时间（最多，每天一次）评估区段定义。

### 启用计划分段 {#enable-scheduled-segmentation}

可以使用UI或API为计划评估启用区段定义。 在UI中，返回到 **[!UICONTROL 浏览]** 选项卡范围 **[!UICONTROL 区段]** 和打开 **[!UICONTROL 将所有区段添加到计划]**. 这将导致根据贵组织设置的时间表来评估所有区段。

>[!NOTE]
>
>可以为最多具有五(5)个合并策略的沙盒启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略 [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划的评估。

当前只能使用API创建计划。 有关使用API创建、编辑和使用计划的详细步骤，请阅读有关评估和访问区段结果的教程，特别是以下部分： [使用API的计划评估](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![“区段浏览”页面上会突出显示用于将所有区段添加到计划的切换开关。](../images/ui/overview/segment-browse-scheduled.png)

## 受众 {#audiences}

>[!IMPORTANT]
>
>受众功能目前为有限测试版，并非对所有用户都可用。 文档和功能可能会发生变化。

选择 **[!UICONTROL 受众]** 选项卡，查看贵组织的所有受众的列表。

![贵组织的受众列表。](../images/ui/overview/list-audiences.png)

默认情况下，此视图会列出有关受众的信息，包括名称、配置文件计数、来源、创建日期和上次修改日期。

您可以选择 ![自定义表](../images/ui/overview/customize-table.png) 图标以更改显示的字段。

![自定义表按钮突出显示。 选择此按钮允许您自定义在受众浏览页面上显示的字段。](../images/ui/overview/select-customize-table.png)

此时会出现一个弹出窗口，其中列出了可显示在表格中的所有字段。

![可以为“浏览受众”部分显示的属性。](../images/ui/overview/customize-table-attributes.png)

| 字段 | 描述 |
| ----- | ----------- | 
| [!UICONTROL 名称] | 受众的名称。 |
| [!UICONTROL 配置文件计数] | 符合受众条件的配置文件总数。 |
| [!UICONTROL Origin] | 受众的来源。 如果此受众是平台生成的，则它将具有分段服务的来源。 |
| [!UICONTROL 生命周期状态] | 受众的状态。 此字段的可能值包括 `Draft`， `Published`、和 `Archived`. |
| [!UICONTROL 更新频率] | 表示受众数据更新频率的值。 此字段的可能值包括 `On Demand`， `Scheduled`、和 `Continuous`. |
| [!UICONTROL 上次更新者] | 上次更新受众的人员姓名。 |
| [!UICONTROL 已创建] | 创建受众的时间和日期。 |
| [!UICONTROL 上次更新时间] | 上次创建受众的时间和日期。 |
| [!UICONTROL 访问标签] | 受众的访问标签。 访问标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 这些标签可以随时应用，从而为您选择如何管理数据提供了灵活性。 有关访问标签的详细信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md). |

您可以选择 **[!UICONTROL 创建受众]** 以创建受众。

![创建受众按钮会突出显示，向您显示选择在何处创建受众。](../images/ui/overview/create-audience.png)

此时会出现一个弹出窗口，您可以在构成受众或构建规则之间进行选择。

![显示您可以创建的两种受众类型的弹出窗口。](../images/ui/overview/create-audience-type.png)

选择 **[!UICONTROL 撰写受众]** 将您带到Audience Builder。 要了解有关创建受众的更多信息，请阅读 [Audience Builder指南](./audience-builder.md).

选择 **[!UICONTROL 生成规则]** 将您带到区段生成器。 要了解有关创建区段的更多信息，请阅读 [Segment Builder指南](./segment-builder.md)

## 受众详细信息 {#audience-details}

要查看有关特定受众的更多详细信息，请在 [!UICONTROL 受众] 选项卡。

此时会显示受众详细信息页面。 根据受众是通过Adobe Experience Platform还是外部源（例如Audience Orchestration）生成的，此页面的详细信息有所不同。

### 平台生成的受众

有关平台生成的受众的更多信息，请阅读 [区段摘要部分](#segment-summary).

### 外部生成的受众

在受众详细信息页面顶部，提供了受众摘要以及有关受众保存所在数据集的详细信息。

![为外部生成的受众提供的详细信息。](../images/ui/overview/externally-generated-audience.png)

此 **[!UICONTROL 受众摘要]** 部分提供属性的ID、名称、描述和详细信息等信息。

此 **[!UICONTROL 数据集详细信息]** 部分提供名称、说明、表名、源和方案等信息。 您可以选择 **[!UICONTROL 查看数据集]** 查看有关数据集的更多信息。

| 字段 | 描述 |
| ----- | ----------- |
| [!UICONTROL 名称] | 数据集的名称。 |
| [!UICONTROL 描述] | 数据集的描述。 |
| [!UICONTROL 表名] | 数据集的表名称。 |
| [!UICONTROL 来源] | 数据集的源。 对于外部生成的受众，此值将为 **架构**. |
| [!UICONTROL 架构] | 数据集对应的XDM架构类型。 |

要了解有关数据集的更多信息，请阅读 [数据集概述](../../catalog/datasets/overview.md).

## 流式客户细分 {#streaming-segmentation}

流式分段是对进行分段的能力 [!DNL Platform] 近乎实时，同时专注于数据丰富性。 借助流式分段，现在当数据进入时，就会进行区段鉴别 [!DNL Platform]，从而无需安排和运行分段作业。

有关流式客户细分的更多信息，请参阅 [流式分段用户指南](./streaming-segmentation.md).

>[!NOTE]
>
>为了使流式分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅 [本用户指南中的流式分段部分](#scheduled-segmentation).

## 边缘分段 {#edge-segmentation}

边缘分段是在边缘上即时评估Platform中的区段的能力，从而启用同一页面和下一页面个性化用例。

有关边缘分段的更多信息，请参阅 [边缘分段UI指南](./edge-segmentation.md)

## 策略违规

>[!NOTE]
>
>策略违规仅适用于创建已分配给目标的区段。

创建完区段后，Adobe Experience Platform数据管理将分析该区段，以确保区段内没有违反策略的情况。 请参阅 [数据治理概述](../../data-governance/home.md) 了解更多信息。

![将显示区段的策略违规。](../images/ui/overview/segment-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

此 [!DNL Segmentation Service] UI提供了一个丰富的工作流，允许您从以下各项中分离出适销受众 [!DNL Real-Time Customer Profile] 数据。

要了解有关 [!DNL Segmentation Service]，请继续阅读文档。 要了解如何使用 [!DNL Segmentation Service] API，请参阅 [[!DNL Segmentation Service] 开发人员指南](../api/overview.md).
