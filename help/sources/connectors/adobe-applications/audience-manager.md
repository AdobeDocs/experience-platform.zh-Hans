---
keywords: Experience Platform；主页；热门主题；Audience Manager连接器；Audience Manager；Audience Manager
solution: Experience Platform
title: Audience Manager源概述
description: Adobe Audience Manager源将Audience Manager中收集的第一方数据流式传输到Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Audience Manager源

Adobe Audience Manager源可流式传输在Adobe Audience Manager中收集的第一方数据，以便在Adobe Experience Platform中激活。 Audience Manager源向Platform摄取两种类型的数据：

- **实时数据：** 在Audience Manager的数据收集服务器上实时捕获的数据。 这些数据用于Audience Manager以填充基于规则的特征，并将在最短延迟时间内出现在Platform中。
- **配置文件数据：** Audience Manager使用实时数据和已载入数据获取客户档案。 这些配置文件用于在区段实现中填充身份图和特征。

Audience Manager源将这些数据类型映射到Experience Data Model (XDM)架构，然后将它们发送到Platform。 实时数据作为XDM ExperienceEvent数据发送，而配置文件数据作为XDM个人配置文件数据发送。

有关详细信息，请阅读以下指南： [在UI中创建Audience Manager源连接](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## 什么是Experience Data Model (XDM)？

XDM是一个公开记录的规范，它提供了一个标准化框架，平台通过它来组织客户体验数据。

遵守XDM标准允许统一合并客户体验数据，从而更轻松地提供数据和收集信息。

有关如何在Experience Platform中使用XDM的更多信息，请阅读 [XDM系统概述](../../../xdm/home.md). 要了解有关如何在不同用户档案之间构建XDM架构和构建事件的更多信息，请参阅 [模式组合基础](../../../xdm/schema/composition.md).

## XDM架构示例

以下是映射到Platform中的XDM ExperienceEvent和XDM Individual Profile的Audience Manager结构示例。

### ExperienceEvent — 用于实时数据和载入的数据

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM个人资料 — 用于个人资料数据

![](images/aam-profile-xdm-for-profile-data.png)

有关如何将字段从Audience Manager映射到XDM的信息，请阅读以下文档： [Audience Manager映射字段](./mapping/audience-manager.md).

## 平台上的数据管理

### 数据集

数据集是数据集合的存储和管理结构，通常是表，包含架构（列）和字段（行），可通过数据连接使用。 Audience Manager数据包括实时数据、入站数据和配置文件数据。 要查找Audience Manager数据集，请在UI中使用搜索函数，并为每种类型的数据提供命名约定。

默认情况下，配置文件的Audience Manager数据集处于禁用状态，用户能够根据自己的用例启用或禁用数据集。 建议不要禁用将用于配置文件中区段成员资格的数据集。

>[!NOTE]
>
>AAM Real-time是唯一发送到数据湖的数据集。 所有其他的Audience Manager数据集将转至 [!DNL Profile]，前提是它们已启用 [!DNL Profile]. 如果它们未启用 [!DNL Profile]，则他们不会收到任何数据，并且将显示为空白。

| 数据集名称 | 描述 | 类 |
| --- | --- | --- |
| AAM Real-time | 此数据集包含由Audience ManagerDCS端点的直接点击收集的数据，以及Audience Manager配置文件的标识映射。 将此数据集保留为配置文件摄取启用。 | 体验事件 |
| AAM实时配置文件更新 | 此数据集可实时定位Audience Manager特征和区段。 其中包括有关Edge区域路由、特征和区段成员资格的信息。 将此数据集保留为配置文件摄取启用。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备数据 | Audience Manager中聚合的具有ECID和相应区段实现的设备数据。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备配置文件数据 | 用于Audience Manager连接器诊断。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM验证的配置文件 | 此数据集包含Audience Manager已验证的用户档案。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM已验证的用户档案元数据 | 用于Audience Manager连接器诊断。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备数据回填 | 数据集来自引入过去的设备数据。 其中包含在Audience Manager中聚合的ECID和相应的区段实现。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换以将数据直接摄取到用户档案。 | 记录 |
| AAM已验证的用户档案回填 | 数据集来自引入过去经过身份验证的数据。 这包含Audience Manager验证的配置文件。 数据在数据集中不可见为批次。 您可以启用 **[!UICONTROL 个人资料]** 切换以将数据直接摄取到用户档案。 | 记录 |

### 连接

Adobe Audience Manager在“目录：Audience Manager连接”中创建了一个连接。 目录是Adobe Experience Platform中数据位置和族系的记录系统。 连接是一个目录对象，它是特定于客户的连接器实例。 请阅读 [目录服务概述](../../../catalog/home.md) 有关目录、连接和连接器的详细信息。

### 区段人口对个人资料的影响

首次将Audience Manager区段发送到Platform时，区段人口大小会对用户档案数量产生直接影响。 这意味着选择所有区段可能会导致配置文件超出您的许可证使用授权。 Platform还会将新数据与配置文件提取的历史数据区分开。 具有100个基于第一方的身份的区段将创建100个配置文件。 但是，如果该区段的人口增至150人，并引入到Platform，则用户档案的数量将仅增加50人，因为只有50个新用户档案。

您还可以通过查看您的帐户可用的用户档案使用情况 [许可证使用情况仪表板](../../../dashboards/guides/license-usage.md).

## Platform上Audience Manager数据的预期滞后时间是多少？

| Audience Manager数据 | 类型 | 延迟 | 注释 |
| --- | --- | --- | --- |
| 实时数据 | 事件 | &lt;25 分钟 | 从Audience Manager边缘节点捕获到出现在数据湖中的时间。 |
| 实时数据 | 配置文件更新 | &lt;10 分钟 | 进入实时客户档案的时间。 |
| 实时数据和已载入数据 | 配置文件更新 | 24到36小时 | 从通过DCS/PCS Edge数据和载入的数据捕获、处理到用户配置文件，再到显示在实时客户配置文件中的时间。 目前，此数据不会直接进入数据湖。 可以为Audience Manager配置文件数据集启用配置文件切换，以将此数据直接摄取到Real-time Customer Profile。 |
