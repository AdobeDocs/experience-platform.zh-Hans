---
keywords: Experience Platform；主页；热门主题；分段服务；分段服务；用户指南；用户指南；用户指南；分段ui指南；区段生成器；实现；现有；退出；
solution: Experience Platform
title: 分段服务UI指南
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service为创建和管理区段定义提供了用户界面。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# 分段服务UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了用于创建和管理区段定义的用户界面。

## 入门指南

使用细分定义需要了解与细分相关的各种[!DNL Experience Platform]服务。 在阅读此用户指南之前，请查阅以下服务的文档：

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 允许您将存储在与个人( [!DNL Experience Platform] 如客户、潜在客户、用户或组织)相关的数据划分为较小的组。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通过将来自不同数据源的身份融入其中，可创建客户用户档案 [!DNL Platform]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

了解本文档中使用的两个关键术语并了解它们之间的差异也很重要：
- **细分定义**:用于描述目标受众的关键特性或行为的规则集。
- **受众**:最终的一组符合区段定义条件的用户档案。

## 概述

在[[!DNL Experience Platform] UI](http://platform.adobe.com/)中，选择左侧导航中的&#x200B;**[!UICONTROL Segments]**&#x200B;以打开&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。 此选项卡提供文档和视频链接，帮助您理解和开始使用区段。

![](../images/ui/overview/segment-overview.png)

## 浏览

选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，查看IMS组织的所有区段定义的列表。

![](../images/ui/overview/segment-browse-all.png)

此视图列表有关区段定义的信息，包括划分、客户流失、用户档案计数、评估方法、创建日期和上次修改日期。

划分显示一个条形图，概述了属于以下各种状态的用户档案百分比：[!UICONTROL Entered]、[!UICONTROL Realized]和[!UICONTROL Exiting]。

![](../images/ui/overview/segment-browse-breakdown.png)

| 状态 | 描述 |
| ------ | ----------- |
| 已输入 | 区段内的新用户档案。 |
| 已实现 | 现有用户档案，仍保留于分部内。 |
| 正在退出 | 离开区段的现有用户档案。 |

客户流失是指在区段定义中更改的用户档案与上次运行区段作业时的用户档案百分比，而计数则表示符合区段条件的用户档案总数。

评估方法可以是流或批。 在数据进入系统时，流段会不断评估。 批区段根据一组计划进行评估。

![](../images/ui/overview/segment-browse-segments.png)

页面顶部有选项，可向计划添加所有区段和创建新区段。

切换&#x200B;**[!UICONTROL Add all segments to schedule]**&#x200B;将启用计划分段。 有关计划分段的详细信息，请参阅本用户指南](#scheduled-segmentation)的[计划分段部分。

选择&#x200B;**[!UICONTROL Create segment]**&#x200B;将转到区段生成器。 要了解有关创建区段的更多信息，请阅读用户指南](#create-segment)中关于创建区段的部分。[

![](../images/ui/overview/segment-browse-top.png)

右侧提要栏包含有关IMS组织内所有区段的信息，列出区段总数、上次评估日期、下次评估日期，以及按评估方法划分的区段。

![](../images/ui/overview/segment-browse-segment-info.png)

选择区段定义的行可提供区段定义的汇总，包括编辑或删除区段的选项、区段的限定受众、总受众大小，以及区段的名称、描述、评估方法、创建日期和上次修改日期。

![](../images/ui/overview/segment-browse-details.png)

## 区段定义详细信息{#segment-details}

要查看有关特定区段定义的更多详细信息，请在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中选择区段名称。

此时将显示区段详细信息页面。 在顶部，会汇总区段定义、有关合格受众大小的信息，以及区段激活的目标。

![](../images/ui/overview/segment-details-summary.png)

### 区段摘要

**[!UICONTROL Segment summary]**&#x200B;部分提供ID、名称、说明和属性详细信息等信息。

此外，您还可以选择编辑区段。 选择&#x200B;**[!UICONTROL Edit segment]**&#x200B;将转到[!DNL Segment Builder]。 有关使用[!DNL Segment Builder]工作区的详细信息，请阅读[[!DNL Segment Builder] 用户指南](./segment-builder.md)。

### 细分受众总数

**[!UICONTROL Total audience in segment]**&#x200B;部分显示符合区段条件的用户档案总数。

估计是使用当天样本数据的样本大小生成的。 如果您的用户档案存储中的实体少于100万个，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2,000万个单位，占全部单位的5%。 有关生成区段估计的详细信息，请参阅区段创建教程的[估计生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

### 已激活的目标

**[!UICONTROL Activated destinations]**&#x200B;部分显示此区段的激活目标。

>[!NOTE]
>
> 目标是[!DNL Real-time Customer Data Platform]提供的功能，允许您将数据导出到外部平台。 有关目标的详细信息，请阅读[目标概述](../../destinations/home.md)。 要了解如何将区段激活到目标，请阅读[将区段激活到目标](../../destinations/ui/activate-destinations.md)指南。

### 用户档案范例

下面是符合该区段资格的用户档案的样本，详细列出了包括[!DNL Profile] ID、名、姓和个人电子邮件在内的信息。

数据采样的触发方式取决于摄取方法。

对于批处理摄取，将每15分钟自动扫描用户档案存储，以查看自上次取样作业运行以来是否成功摄取了新批。 如果是这样，随后扫描用户档案存储，以查看记录数是否至少有5%的变化。 如果满足这些条件，将触发新的采样作业。

对于流摄取，每小时自动扫描用户档案存储，以查看记录数是否至少有5%的变化。 如果满足此条件，将触发新的采样作业。

扫描的样本大小取决于用户档案存储中的实体总数。 下表显示了这些样本大小：

| 用户档案存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1到2000万 | 100万 |
| 2000多万 | 总共5% |

通过选择[!DNL Profile] ID，可以查看有关每个[!DNL Profile]的详细信息。 要了解有关用户档案详细信息的更多信息，请阅读[[!DNL Real-time Customer Profile] 用户指南](../../profile/ui/user-guide.md#profile-detail)。

![](../images/ui/overview/segment-details-profiles.png)

## 创建区段 {#create-segment}

选择右上角的&#x200B;**[!UICONTROL Create segment]**&#x200B;将打开[!DNL Segment Builder]工作区，您可以在其中开始创建区段定义。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作区

[!DNL Segment Builder] 提供丰富的工作区，允许您与数据元 [!DNL Profile] 素交互。工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。

有关使用[!DNL Segment Builder]工作区的详细信息，请阅读[[!DNL Segment Builder] 用户指南](./segment-builder.md)。

![](../images/ui/overview/segment-builder.png)

## 计划分段{#scheduled-segmentation}

在创建区段定义后，您便可以通过按需或计划（连续）评估来评估这些定义。 评估是指通过段定义移动[!DNL Real-time Customer Profile]数据以生成相应的受众。 创建受众后，会保存并存储这些应用程序，以便使用[!DNL Experience Platform] API导出它们。

按需评估包括使用API执行评估并根据需要构建受众，而计划评估（也称为“计划分段”）允许您创建循环计划以在特定时间（最多每天一次）评估区段定义。

### 启用计划分段{#enable-scheduled-segmentation}

可以使用UI或API为计划评估启用区段定义。 在UI中，返回至&#x200B;**[!UICONTROL Segments]**&#x200B;中的&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，并打开&#x200B;**[!UICONTROL Add all segments to schedule]**。 这将导致所有区段都根据您的组织设置的计划进行评估。

>[!NOTE]
>
>对于[!DNL XDM Individual Profile]最多五(5)个合并策略的沙箱，可启用计划评估。 如果您的组织在单个沙箱环境内有5个以上的[!DNL XDM Individual Profile]合并策略，您将无法使用计划的评估。

计划当前只能使用API创建。 有关使用API创建、编辑和使用计划的详细步骤，请按照教程来评估和访问区段结果，特别是使用API](../tutorials/evaluate-a-segment.md#scheduled-evaluation)计划评估的[部分。

![](../images/ui/overview/segment-browse-scheduled.png)

## 流分段{#streaming-segmentation}

流分段是一种能够近乎实时地对[!DNL Platform]进行分段，同时专注于数据丰富性的能力。 通过流分段，当数据进入[!DNL Platform]时，现在会发生细分资格，从而缓解了计划和运行分段作业的需求。

有关流分段的详细信息，请参阅[流分段用户指南](./streaming-segmentation.md)。

>[!NOTE]
>
>为了使流分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅本用户指南](#scheduled-segmentation)中的[流分段部分。

## 边缘分割{#edge-segmentation}

边缘细分是指在Platform中即时评估边缘区段的能力，支持相同页面和下一页个性化使用案例。

有关边缘分割的详细信息，请参阅[边缘分割UI指南](./edge-segmentation.md)

## 违反策略

>[!NOTE]
>
>策略违规仅在创建已分配到目标的区段时才适用。

创建完区段后，Adobe Experience Platform Data Governance会分析该区段，以确保该区段内没有违反政策的行为。 有关详细信息，请参阅[[!DNL Data Governance] 概述](../../data-governance/home.md)。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 后续步骤和其他资源{#next-steps}

[!DNL Segmentation Service] UI提供了一个丰富的工作流，允许您从[!DNL Real-time Customer Profile]数据中隔离可销售受众。

要了解有关[!DNL Segmentation Service]的更多信息，请继续阅读文档。 要了解如何使用[!DNL Segmentation Service] API，请阅读[[!DNL Segmentation Service] 开发人员指南](../api/overview.md)。
