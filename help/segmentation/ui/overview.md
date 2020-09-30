---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: 分段服务用户指南
topic: ui guide
description: Adobe Experience Platform分段服务为创建和管理段定义提供了用户界面。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 0%

---


# [!UICONTROL 分段服务] 用户指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了用于创建和管理区段定义的用户界面。

## 入门指南

使用细分定义需要了解与细分相关 [!DNL Experience Platform] 的各种服务。 在阅读本用户指南之前，请查阅以下服务的文档：

- [[!DNL分段服务]](../home.md): [!DNL Segmentation Service] 允许您将与个人(如 [!DNL Experience Platform] 客户、潜在客户、用户或组织)相关的数据分为较小的组。
- [[!DNL实时客户用户档案]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [[!DNLAdobe Experience Platform身份服务]](../../identity-service/home.md):通过将来自不同数据源的身份融入其中，实现客户用户档案的创建 [!DNL Platform]。
- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

了解本文档使用的两个关键术语并了解它们之间的区别也很重要：
- **细分定义**:用于描述目标受众的关键特性或行为的规则集。
- **受众**:生成的一组符合区段定义条件的用户档案。

## 概述

在UI [[!DNL Experience Platform] 中](http://platform.adobe.com/)，在左 **[!UICONTROL 侧导航]** 中选择 **[!UICONTROL “区段]** ”以打开“概述”选项卡。 此选项卡提供文档和视频链接，帮助您了解和开始使用区段。

![](../images/ui/overview/segment-overview.png)

## 浏览

选择“ **[!UICONTROL 浏览]** ”选项卡，查看IMS组织的所有区段定义的列表。

![](../images/ui/overview/segment-browse-all.png)

此视图列表有关细分、客户流失、用户档案计数、评估方法、创建日期和上次修改日期的细分信息。

细分显示一个条形图，概述了属于以下各种状态的用户档案百分比： [!UICONTROL 已输入]、 [!UICONTROL 已实现]和已 [!UICONTROL 退出]。

![](../images/ui/overview/segment-browse-breakdown.png)

| 状态 | 描述 |
| ------ | ----------- |
| 已输入 | 区段内的新用户档案。 |
| 已实现 | 现有用户档案，其仍属于分部。 |
| 正在退出 | 离开区段的现有用户档案。 |

客户流失是指在区段定义中发生更改的用户档案与上次运行区段作业时的用户档案百分比，而计数则指符合区段条件的用户档案总数。

评估方法可以是流式的，也可以是批量的。 当数据进入系统时，会持续评估流段。 批区段根据一组计划进行评估。

![](../images/ui/overview/segment-browse-segments.png)

页面顶部有选项，可向计划添加所有区段和创建新区段。

将所 **[!UICONTROL 有区段添加到计划]** ，将启用计划分段。 有关计划分段的详细信息，请参 [阅本用户指南的计划分段部分](#scheduled-segmentation)。

选择 **[!UICONTROL 创建区段]** ，将转到区段生成器。 要了解有关创建区段的更多信息，请阅读用户指南 [中有关创建区段的部分](#create-segment)。

![](../images/ui/overview/segment-browse-top.png)

右侧提要栏包含有关IMS组织内所有细分的信息，列出细分总数、上次评估日期、下次评估日期，以及按评估方法划分的细分。

![](../images/ui/overview/segment-browse-segment-info.png)

选择区段定义的行会提供区段定义的摘要，包括编辑或删除区段的选项、区段的限定受众、受众总大小，以及区段的名称、描述、评估方法、创建日期和上次修改日期。

![](../images/ui/overview/segment-browse-details.png)

## 细分定义详细信息 {#segment-details}

要查看有关特定区段定义的更多详细信息，请在“浏览”选项卡中选择区段 **[!UICONTROL 的名]** 称。

此时会显示区段详细信息页面。 在顶部，会汇总区段定义、有关限定受众大小的信息，以及区段的激活目标。

![](../images/ui/overview/segment-details-summary.png)

### 细分摘要

区段 **[!UICONTROL 摘要]** 部分提供诸如ID、名称、说明和属性详细信息等信息。

此外，您还可以选择编辑区段。 选择 **[!UICONTROL 编辑区段]** ，将转到 [!DNL Segment Builder]。 有关使用工作区的更 [!DNL Segment Builder] 多详细信息，请阅 [[!DNL Segment Builder] 读用户指南](./segment-builder.md)。

### 细分受众总数

区段 **[!UICONTROL 中的受众总数]** ，显示符合区段条件的用户档案总数。

估计是使用当天样本数据的样本大小生成的。 如果您的用户档案存储中少于100万个实体，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2000万个单位，占全部单位的5%。 有关生成区段估计的更多信息，请参 [阅区段创建教程](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 的估计生成部分。

### 已激活的目标

“已 **[!UICONTROL 激活的目标]** ”部分显示此区段已激活的目标。

>[!NOTE]
>
> 目标是可用的功 [!DNL Real-time Customer Data Platform]能，允许您将数据导出到外部平台。 有关目标的更多信息，请阅读目 [标概述](../../rtcdp/destinations/destinations-overview.md)。 要了解如何将区段激活到目标，请阅读将区 [段激活到目标的指南](../../rtcdp/destinations/activate-destinations.md)。

### 用户档案范例

下面是符合该区段资格的用户档案样本，详细介绍了包括 [!DNL Profile] ID、名字、姓氏和个人电子邮件在内的信息。

数据采样的触发方式取决于摄取的方法。

对于批量摄取，用户档案存储区每十五分钟自动扫描一次，以查看自上次采样作业运行以来是否成功摄取了新批量。 如果是这样，随后扫描用户档案存储，以查看记录数是否至少有5%的变化。 如果满足这些条件，将触发新的采样作业。

对于流式摄取，每小时自动扫描用户档案商店，以查看记录数是否至少有5%的变化。 如果满足此条件，将触发新的采样作业。

扫描的样本大小取决于用户档案存储中的实体总数。 下表显示了这些示例大小：

| 用户档案商店中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1000万到2000万 | 100万 |
| 2000多万 | 总共5% |

通过选择ID可以 [!DNL Profile] 查看有关每个ID的更详细 [!DNL Profile] 信息。 要进一步了解用户档案的详细信息，请阅读 [[!DNL Real-time Customer Profile] 用户指南](../../profile/ui/user-guide.md#profile-detail)。

![](../images/ui/overview/segment-details-profiles.png)

## 创建区段 {#create-segment}

选 **[!UICONTROL 择右上]** 角的创建区段会打开工作区 [!DNL Segment Builder] ，您可以在工作区中开始创建区段定义。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作区

[!DNL Segment Builder] 提供丰富的工作区，允许您与数据元素 [!DNL Profile] 交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。

有关使用工作区的更 [!DNL Segment Builder] 多详细信息，请阅 [[!DNL Segment Builder] 读用户指南](./segment-builder.md)。

![](../images/ui/overview/segment-builder.png)

## 计划分段 {#scheduled-segmentation}

在创建区段定义后，您便可以通过按需或计划（连续）评估来评估这些定义。 评估是指通 [!DNL Real-time Customer Profile] 过细分定义移动数据，以产生相应的受众。 创建受众后，会保存并存储这些数据，以便使用API导出 [!DNL Experience Platform] 它们。

点播评估包括根据需要使用API执行评估和构建受众，而计划评估（也称为“计划分段”）允许您创建循环计划以在特定时间（最多每天一次）评估区段定义。

### 启用计划分段 {#enable-scheduled-segmentation}

可以使用UI或API为计划评估启用区段定义。 在UI中，返回至“区段” **[!UICONTROL 中的]** “浏 **[!UICONTROL 览”选]** 项卡 **[!UICONTROL ，并打开]**“将所有区段添加到计划”。 这将导致所有区段都根据您的组织设置的计划进行评估。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可启用计划评估 [!DNL XDM Individual Profile]。 如果您的组织在单个沙箱环境内 [!DNL XDM Individual Profile] 有五个以上的合并策略，您将无法使用计划的评估。

计划当前只能使用API创建。 有关使用API创建、编辑和使用计划的详细步骤，请按照教程来评估和访问区段结果，特别是使用API进 [行计划评估的部分](../tutorials/evaluate-a-segment.md#scheduled-evaluation)。

![](../images/ui/overview/segment-browse-scheduled.png)

## 流细分 {#streaming-segmentation}

流细分是一种在关注数据丰 [!DNL Platform] 富性的同时近乎实时地进行细分的能力。 利用流细分，当数据进入时，细分资格现在会 [!DNL Platform]发生，从而减轻计划和运行细分作业的需求。

有关流分段的更多信息，请参 [阅流分段用户指南](./streaming-segmentation.md)。

>[!NOTE]
>
>为了使流分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参 [阅本用户指南中的流分段部分](#scheduled-segmentation)。

## 违反策略

>[!NOTE]
>
>策略违规仅在创建已分配到目标的区段时适用。

创建完细分后，Adobe Experience Platform数据管理将对细分进行分析，以确保细分不违反政策。 有关更多 [[!DNL Data Governance] 信息](../../data-governance/home.md) ，请参阅概述。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

UI提 [!DNL Segmentation Service] 供了一个丰富的工作流，允许您从数据中隔离可销售的 [!DNL Real-time Customer Profile] 受众。

要了解更多 [!DNL Segmentation Service]信息，请继续阅读文档。 要了解如何使用API, [!DNL Segmentation Service] 请阅读开发人 [[!DNL Segmentation Service] 员指南](../api/overview.md)。
