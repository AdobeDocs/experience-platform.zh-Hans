---
keywords: Experience Platform；主页；热门主题；分段服务；分段；分段服务；用户指南；UI指南；分段UI指南；区段生成器；区段生成器；已实现；现有；正在退出；
solution: Experience Platform
title: Segmentation Service UI指南
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service提供了用于创建和管理区段定义的用户界面。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Segmentation Service UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了用于创建和管理区段定义的用户界面。

## 快速入门

使用区段定义需要了解 [!DNL Experience Platform] 涉及分段的服务。 在阅读本用户指南之前，请查阅以下服务的文档：

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 允许您将存储在 [!DNL Experience Platform] 与属于较小群组的个人（例如客户、潜在客户、用户或组织）相关。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通过将来自被摄取到的不同数据源的身份桥接到 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../../xdm/schema/best-practices.md).

另外，还必须了解本文档中使用的两个关键术语，并了解它们之间的区别：
- **区段定义**:用于描述目标受众的关键特征或行为的规则集。
- **受众**:生成的一组符合区段定义标准的用户档案。

## 概述

在Experience PlatformUI中，选择 **[!UICONTROL 区段]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡 [!UICONTROL 区段] 功能板。

>[!NOTE]
>
>如果贵组织是Platform的新用户，并且尚未创建活动的配置文件数据集或合并策略，则 [!UICONTROL 区段] 功能板不可见。 相反， [!UICONTROL 概述] 选项卡会显示可帮助您开始使用区段的链接和文档。

### [!UICONTROL 区段] 仪表板 {#segments-dashboard}

的 **[!UICONTROL 区段]** 功能板概述了与贵组织的区段数据相关的关键量度。

要了解更多信息，请访问 [区段仪表板指南](../../dashboards/guides/segments.md).

![](../../dashboards/images/segments/dashboard-overview.png)

## 浏览

选择 **[!UICONTROL 浏览]** 选项卡，以查看IMS组织的所有区段定义列表。

![](../images/ui/overview/segment-browse-all.png)

此视图列出有关区段定义的信息，包括划分、流失率、用户档案计数、评估方法、创建日期和上次修改日期。

划分会显示一个条形图，其中概述了属于以下每种状态的用户档案百分比： [!UICONTROL 已实现], [!UICONTROL 现有]和 [!UICONTROL 正在退出]. 此外， [!UICONTROL 浏览] 选项卡是区段状态的最准确划分。 如果此数字与 [!UICONTROL 概述] 选项卡，您应使用 [!UICONTROL 浏览] 选项卡作为正确的信息源，因为 [!UICONTROL 概述] 选项卡号每天只更新一次。

![](../images/ui/overview/segment-browse-breakdown.png)

| 状态 | 描述 |
| ------ | ----------- |
| 已实现 | 区段中的新用户档案。 |
| 现有 | 保留在区段内的现有用户档案。 |
| 正在退出 | 离开区段的现有用户档案。 |

流失率表示与上次运行区段作业相比，区段定义中发生更改的配置文件的百分比，而配置文件计数表示符合区段资格的配置文件总数。

评估方法可以是流评估或批量评估。 当数据进入系统时，会不断评估流区段。 批区段将根据设置的计划进行评估。

![](../images/ui/overview/segment-browse-segments.png)

页面顶部提供了用于向计划添加所有区段和创建新区段的选项。

切换 **[!UICONTROL 添加所有要计划的区段]** 将启用计划分段。 有关计划分段的更多信息，请参阅 [本用户指南中的计划分段部分](#scheduled-segmentation).

选择 **[!UICONTROL 创建区段]** 会将您转到区段生成器。 要了解有关创建区段的更多信息，请阅读 [在用户指南中创建区段](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

右侧侧栏包含有关IMS组织内所有区段的信息，列出区段总数、上次评估日期、下次评估日期，以及按评估方法划分区段。

![](../images/ui/overview/segment-browse-segment-info.png)

选择区段定义的行可提供区段定义的摘要，包括用于编辑或删除区段、将区段激活到目标、区段的合格受众、总受众大小的选项，以及区段的名称、描述、评估方法、创建日期和上次修改日期的选项。

>[!NOTE]
>
> 您将 **not** 能够删除目标激活中使用的区段。

![](../images/ui/overview/segment-browse-details.png)

## 区段定义详细信息 {#segment-details}

要查看有关特定区段定义的更多详细信息，请在 **[!UICONTROL 浏览]** 选项卡。

此时将显示区段详细信息页面。 在顶部，提供了区段定义的摘要、有关符合条件的受众大小以及区段激活的目标的信息。

![](../images/ui/overview/segment-details-summary.png)

### 区段摘要

的 **[!UICONTROL 区段摘要]** 部分提供了ID、名称、描述和属性详细信息等信息。

此外，您还可以选择将区段激活到目标或编辑区段。 选择 **[!UICONTROL 激活到目标]** 将允许您将区段激活到目标。 有关将区段激活到目标的更多详细信息，请阅读 [激活概述](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

选择 **[!UICONTROL 编辑区段]** 会带你去 [!DNL Segment Builder]. 有关使用 [!DNL Segment Builder] 工作区，请阅读 [[!DNL Segment Builder] 用户指南](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### 区段中的受众总数

的 **[!UICONTROL 区段中的受众总数]** 部分显示符合区段资格的用户档案总数。

使用当天样本数据的样本量生成估计值。 如果您的用户档案存储中的实体少于100万个，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2000万个单位使用5%的单位。 有关生成区段估计的更多信息，请参阅 [估计生成节](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 区段创建教程的“受众”部分。

### 已激活的目标

的 **[!UICONTROL 已激活的目标]** 部分显示激活此区段的目标。

>[!NOTE]
>
> 目标是 [!DNL Real-time Customer Data Platform]，并允许您将数据导出到外部平台。 有关目标的更多信息，请阅读 [目标概述](../../destinations/home.md). 要了解如何将区段激活到目标，请参阅 [激活概述](../../destinations/ui/activation-overview.md).

### 配置文件示例

下面是符合区段资格的用户档案取样，其中详细介绍了 [!DNL Profile] ID、名字、姓氏和个人电子邮件。

数据采样的触发方式取决于摄取方法。

对于批量摄取，将每15分钟自动扫描一次配置文件存储，以查看自运行上次取样作业以来是否成功摄取了新批次。 如果是这种情况，随后将扫描用户档案存储，以查看记录数是否至少发生了5%的更改。 如果满足这些条件，则会触发新的取样作业。

对于流式摄取，每小时会自动扫描配置文件存储，以查看记录数量是否至少发生了5%的更改。 如果满足此条件，则会触发新的取样作业。

扫描的样本大小取决于配置文件存储中的实体总数。 下表显示了这些样本大小：

| 配置文件存储中的实体 | 示例大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1到2000万 | 100万 |
| 2000多万 | 总共5% |

有关每个 [!DNL Profile] 可通过选择 [!DNL Profile] ID。 要进一步了解用户档案的详细信息，请阅读 [[!DNL Real-time Customer Profile] 用户指南](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## 创建区段 {#create-segment}

选择 **[!UICONTROL 创建区段]** 在右上角，打开 [!DNL Segment Builder] 工作区中，您可以开始创建区段定义。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作区

[!DNL Segment Builder] 提供了丰富的工作区，可让您与 [!DNL Profile] 数据元素。 工作区提供了用于构建和编辑规则的直观控件，例如用于表示数据属性的拖放图块。

有关使用 [!DNL Segment Builder] 工作区，请阅读 [[!DNL Segment Builder] 用户指南](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## 计划分段 {#scheduled-segmentation}

创建区段定义后，您可以通过按需或计划（连续）评估来评估区段定义。 评估手段移动 [!DNL Real-time Customer Profile] 通过区段定义获取数据，以生成相应的受众。 创建受众后，将保存并存储受众，以便使用 [!DNL Experience Platform] API。

按需评估包括使用API执行评估并根据需要构建受众，而计划评估（也称为“计划分段”）则允许您创建定期计划以在特定时间（最多每天一次）评估区段定义。

### 启用计划分段 {#enable-scheduled-segmentation}

可以使用UI或API来启用区段定义以进行计划评估。 在UI中，返回到 **[!UICONTROL 浏览]** 选项卡 **[!UICONTROL 区段]** 打开 **[!UICONTROL 添加所有要计划的区段]**. 这将导致根据您的组织设置的计划来评估所有区段。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可以启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略， [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划评估。

当前只能使用API创建计划。 有关使用API创建、编辑和使用计划的详细步骤，请按照有关评估和访问区段结果的教程(特别是 [使用API进行计划评估](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## 流分段 {#streaming-segmentation}

流式客户细分是对 [!DNL Platform] 近乎实时，同时关注数据的丰富性。 通过流式客户细分，现在，当数据进入 [!DNL Platform]，以缓解计划和运行分段作业的需求。

有关流式分段的更多信息，请参阅 [流式分段用户指南](./streaming-segmentation.md).

>[!NOTE]
>
>为了使流式客户细分正常工作，您需要为组织启用计划客户细分。 有关启用计划分段的详细信息，请参阅 [本用户指南中的流分段部分](#scheduled-segmentation).

## 边缘分割 {#edge-segmentation}

边缘分段功能可以即时评估Platform中的边缘区段，从而实现同一页面和下一页面个性化用例。

有关边缘分割的更多信息，请参阅 [边缘分段UI指南](./edge-segmentation.md)

## 违反策略

>[!NOTE]
>
>仅当您创建的区段已分配给目标时，才会应用策略违规。

创建完区段后，Adobe Experience Platform数据管理将对该区段进行分析，以确保该区段内没有违反策略的情况。 请参阅 [数据管理概述](../../data-governance/home.md) 以了解更多信息。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

的 [!DNL Segmentation Service] UI提供了一个丰富的工作流，允许您将可销售的受众与 [!DNL Real-time Customer Profile] 数据。

详细了解 [!DNL Segmentation Service]，请继续阅读文档。 了解如何使用 [!DNL Segmentation Service] API，请阅读 [[!DNL Segmentation Service] 开发人员指南](../api/overview.md).
