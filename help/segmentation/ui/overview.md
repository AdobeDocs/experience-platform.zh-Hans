---
solution: Experience Platform
title: 分段服务UI指南
description: 了解如何在Adobe Experience Platform UI中创建和管理受众和区段定义。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# 分段服务UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了一个用于创建和管理受众和区段定义的用户界面。

## 快速入门

使用受众和区段定义需要了解各种 [!DNL Experience Platform] 与分段相关的服务。 在阅读本用户指南之前，请查看以下服务的文档：

- [[!DNL Segmentation Service]](../home.md)： [!DNL Segmentation Service] 允许您对存储在以下位置的数据分段： [!DNL Experience Platform] 将个人（如客户、潜在客户、用户或组织）关联到较小的组中。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：通过桥接被摄取到的不同数据源中的身份来创建客户用户档案 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被作为配置文件和事件摄取，并根据 [数据建模的最佳实践](../../xdm/schema/best-practices.md).

您还应该了解通过本文档使用的以下关键术语并了解它们之间的差异：

- **受众**：一组具有相似行为和/或特征的人。 此人员集合既可以通过Adobe Experience Platform使用区段定义（Platform生成的受众）生成并由受众组合生成，也可以从外部源(例如自定义上传（外部生成的受众）)生成。
- **区段定义**：Adobe Experience Platform用于描述目标受众关键特征或行为的规则。
- **区段**：将用户档案划分为受众的操作。

## 概述

在Experience PlatformUI中，选择 **[!UICONTROL 受众]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡显示 [!UICONTROL 受众] 仪表板。

>[!NOTE]
>
>如果您的组织是初次使用Platform，但尚未创建活动配置文件数据集或合并策略，则 [!UICONTROL 受众] 仪表板不可见。 相反， [!UICONTROL 概述] 选项卡会显示链接和文档，以帮助您开始使用受众。

### [!UICONTROL 受众] 仪表板 {#segments-dashboard}

此 **[!UICONTROL 受众]** 仪表板概述了与贵组织的受众数据相关的关键量度。

要了解更多信息，请访问 [受众仪表板指南](../../dashboards/guides/audiences.md).

![将显示受众仪表板。 该可视化图表显示各种构件，包括受众规模、按身份列出的配置文件、身份重叠以及受众规模变化趋势。](../../dashboards/images/segments/dashboard-overview.png)

## 浏览 {#browse}

选择 **[!UICONTROL 浏览]** 选项卡以查看受众门户。 Audience Portal提供了属于您的组织和沙盒的所有受众的列表，并包括配置文件计数、来源、创建日期、上次修改日期、标记和划分等详细信息。

此外，通过受众门户，您可以使用区段生成器或受众构成创建新受众，并将外部生成的受众导入Platform。

欲知受众门户的更多信息，请阅读 [受众门户概述](./audience-portal.md).

## 构成 {#compositions}

选择 **[!UICONTROL 合成]** 选项卡，查看通过受众构成为您的组织生成的所有受众的列表。

![在受众构成中为您的组织创建的受众列表。](../images/ui/overview/compositions.png)

默认情况下，此视图会列出有关受众的信息，包括名称、状态、创建日期、创建者、上次更新日期和上次更新者。

每个受众旁边都有一个省略号图标。 选择此选项将显示受众可用的快速操作列表。

| 操作 | 描述 |
| ------ | ----------- |
| 复制 | 复制所选受众。 |
| 管理访问权限 | 管理属于受众的访问标签。 有关访问标签的详细信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md). |
| Delete | 删除所选受众。 在下游目标中使用或属于其他受众依赖对象的受众 **无法** 将被删除。 有关删除受众的更多信息，请阅读 [分段常见问题解答](../faq.md#lifecycle-states). |

您可以选择 ![自定义表](../images/ui/overview/customize-table.png) 图标以更改显示的字段。

![自定义表格按钮会突出显示。 选择此按钮允许您自定义在受众组合页面上显示的字段。](../images/ui/overview/compositions-select-customize-table.png)

此时会出现一个弹出窗口，其中列出了可在该表中显示的所有字段。

![可以为“构成”部分显示的属性。](../images/ui/overview/compositions-customize-table.png)

| 字段 | 描述 |
| ----- | ----------- | 
| [!UICONTROL 名称] | 受众的名称。 |
| [!UICONTROL 状态] | 受众的状态。 此字段的可能值包括 `Draft`， `Inactive`、和 `Published`. |
| [!UICONTROL 已创建] | 创建受众的时间和日期。 |
| [!UICONTROL 创建者] | 创建受众的人员姓名。 |
| [!UICONTROL 已更新] | 上次更新受众的时间和日期。 |
| [!UICONTROL 更新者] | 上次更新受众的人员姓名。 |

要查看受众的构成方式，请在左侧导航栏中选择受众的名称， [!UICONTROL 受众] 选项卡。

此时将显示“受众构成”页面，其中包含构成受众的构建基块。 有关如何使用受众构图的更多详细信息，请参阅 [受众合成UI指南](./audience-composition.md).

## 流式客户细分 {#streaming-segmentation}

流式分段是在以下项上进行分段的能力 [!DNL Platform] 近乎实时，同时专注于数据丰富性。 借助流式分段，现在可以在数据进入时进行分段鉴别 [!DNL Platform]，从而无需安排和运行分段作业。

有关流式客户细分的更多信息，请参阅 [流式分段用户指南](./streaming-segmentation.md).

>[!NOTE]
>
>为了使流式分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅 [本用户指南中的流分段部分](#scheduled-segmentation).

## 边缘分段 {#edge-segmentation}

Edge分段能够在边缘即时评估Platform中的受众，启用同一页面和下一页面个性化用例。

有关边缘分段的更多信息，请参阅 [边缘分段UI指南](./edge-segmentation.md)

## 策略违规

>[!NOTE]
>
>策略违规仅适用于创建已分配给目标的受众。

创建完受众后，Adobe Experience Platform数据管理将分析受众，以确保受众内没有违反策略的情况。 请参阅 [数据管理概述](../../data-governance/home.md) 以了解更多信息。

![将显示受众的策略违规。](../images/ui/overview/audience-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

此 [!DNL Segmentation Service] UI提供了一个丰富的工作流，允许您从创建可营销受众 [!DNL Real-Time Customer Profile] 数据。

要了解有关 [!DNL Segmentation Service]，请继续阅读文档。 要了解如何使用 [!DNL Segmentation Service] API，请阅读 [[!DNL Segmentation Service] 开发人员指南](../api/overview.md).
