---
keywords: Experience Platform；主页；热门主题；Audience Manager连接器；Audience Manager;Audience Manager
solution: Experience Platform
title: Audience Manager源连接器概述
topic-legacy: overview
description: Adobe Audience Manager源连接器将Audience Manager中收集的第一方数据流传输到Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Audience Manager连接器

Adobe Audience Manager Data Connector将Adobe Audience Manager中收集的第一方数据流传输到Adobe Experience Platform。 Audience Manager连接器将两类数据摄取到平台：

- **实时数据：** 在Audience Manager的数据收集服务器上实时捕获的数据。 此数据用于Audience Manager以填充基于规则的特征，并将在最短的延迟时间内在Platform中显示。
- **用户档案数据：** Audience Manager使用实时和已载入的数据来获取客户配置文件。 这些配置文件用于填充区段实现中的身份图和特征。

Audience Manager连接器会将这些数据类别映射到Experience Data Model(XDM)架构，并将它们发送到Platform。 实时数据将作为XDM ExperienceEvent数据发送，而配置文件数据将作为XDM个人配置文件发送。

有关使用Platform UI创建与Adobe Audience Manager连接的说明，请参阅 [Audience Manager连接器教程](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## 什么是Experience Data Model(XDM)?

XDM是一项公开记录的规范，它提供了一个标准化框架，Platform可通过该框架组织客户体验数据。

遵循XDM标准可以统一整合客户体验数据，从而更轻松地提供数据和收集信息。

有关如何在Experience Platform中使用XDM的更多信息，请参阅 [XDM系统概述](../../../xdm/home.md). 要进一步了解XDM模式（如用户档案和ExperienceEvent）的结构，请参阅 [架构组合基础知识](../../../xdm/schema/composition.md).

## XDM模式示例

以下是映射到Platform中XDM ExperienceEvent和XDM个人配置文件的Audience Manager结构示例。

### ExperienceEvent — 用于实时数据和已载入数据

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM个人配置文件 — 用于配置文件数据

![](images/aam-profile-xdm-for-profile-data.png)

## 如何将字段从Adobe Audience Manager映射到XDM?

请参阅相关文档 [Audience Manager映射字段](./mapping/audience-manager.md) 以了解更多信息。

## 平台上的数据管理

### 数据集

数据集是用于数据集合的存储和管理结构，通常是一个表，其中包含架构（列）和字段（行），并且可通过数据连接使用。 Audience Manager数据由实时数据、入站数据和用户档案数据组成。 要查找Audience Manager数据集，请使用UI中的搜索函数，并为每个类型的数据提供命名约定。

Audience Manager数据集在默认情况下会禁用配置文件，并且用户可以根据其用例启用或禁用数据集。 不建议禁用将用于配置文件中区段成员资格的数据集。

>[!NOTE]
>
>AAM Real-time是唯一一个 [!DNL Data Lake]. 所有其他Audience Manager数据集将转到 [!DNL Profile]，如果为启用了 [!DNL Profile]. 如果未为 [!DNL Profile]，则他们将不会收到任何数据，并且将显示为空。

| 数据集名称 | 描述 | 类 |
| --- | --- | --- |
| AAM实时 | 此Audience Manager集包含通过DCS端点上的直接点击收集的数据以及Audience Manager配置文件的身份映射。 保持此数据集已启用用户档案摄取。 | 体验事件 |
| AAM实时配置文件更新 | 此数据集支持对Audience Manager特征和区段进行实时定位。 其中包含有关边缘区域路由、特征和区段成员资格的信息。 保持此数据集已启用用户档案摄取。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备数据 | 具有ECID的设备数据以及在Audience Manager中聚合的相应区段实现。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备配置文件数据 | 用于Audience Manager连接器诊断。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM Authenticated Profiles | 此数据集包含经过Audience Manager验证的用户档案。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM已验证的用户档案元数据 | 用于Audience Manager连接器诊断。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换，以直接将数据摄取到用户档案。 | 记录 |
| AAM设备数据回填 | 导入过去设备数据的数据集。 其中包含ECID和在Audience Manager中聚合的相应区段实现。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换以直接将数据摄取到用户档案。 | 记录 |
| AAM已验证的用户档案回填 | 引入过去经过身份验证的数据集。 其中包含经过Audience Manager验证的用户档案。 数据在数据集中以批次形式显示。 您可以启用 **[!UICONTROL 用户档案]** 切换以直接将数据摄取到用户档案。 | 记录 |

### 连接

Adobe Audience Manager在目录中创建一个连接：Audience Manager连接。 目录是Adobe Experience Platform中数据位置和谱系的记录系统。 连接是作为连接器客户特定实例的目录对象。 请参阅 [目录服务概述](../../../catalog/home.md) 有关目录、连接和连接器的详细信息。

## 平台上Audience Manager数据的预期滞后时间是多少？

| Audience Manager数据 | 延迟 | 注释 |
| --- | --- | --- |
| 实时数据 | &lt; 35 分钟. | 从在Audience Manager边缘节点捕获到在平台数据湖中显示的时间。 |
| 用户档案数据 | &lt; 2 天 | 从通过DCS/PCS Edge数据和已载入数据捕获的时间，处理到用户配置文件，然后显示在配置文件中。 此数据今天不会直接登陆Platform Data Lake。 可以为Audience Manager配置文件数据集启用配置文件切换，以便将此数据直接摄取到配置文件中。 |
