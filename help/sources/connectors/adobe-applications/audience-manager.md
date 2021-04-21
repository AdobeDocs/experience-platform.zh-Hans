---
keywords: Experience Platform；主页；热门主题；Audience Manager连接器；受众管理器；受众管理器
solution: Experience Platform
title: Audience Manager源连接器概述
topic-legacy: overview
description: Adobe Audience Manager源连接器将在Audience Manager中收集的第一方数据流化到Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Audience Manager连接器

Adobe Audience Manager数据连接器将在Adobe Audience Manager中收集的第一方数据流化到Adobe Experience Platform。 Audience Manager连接器将两类别数据引入平台：

- **实时数据：在** Audience Manager的数据收集服务器上实时捕获数据。此数据用于Audience Manager以填充基于规则的特征，并将在最短的延迟时间内在平台中显示。
- **用户档案数** 据：Audience Manager使用实时和已载入的数据衍生客户用户档案。这些用户档案用于填充区段实现上的标识图和特征。

Audience Manager连接器将这些类别映射到Experience Data Model(XDM)模式，并将其发送到平台。 实时数据以XDM ExperienceEvent数据的形式发送，而用户档案数据以XDM单个用户档案的形式发送。

有关使用平台UI创建与Adobe Audience Manager连接的说明，请参阅[Audience Manager连接器教程](../../tutorials/ui/create/adobe-applications/audience-manager.md)。

## 什么是体验数据模型(XDM)?

XDM是一个公开记录的规范，它提供了一个标准化框架，平台可通过该框架组织客户体验数据。

遵循XDM标准可统一整合客户体验数据，从而更轻松地提供数据和收集信息。

有关如何在Experience Platform中使用XDM的详细信息，请参阅[XDM系统概述](../../../xdm/home.md)。 要进一步了解用户档案和ExperienceEvent等XDM模式的结构，请参阅模式合成的[基础知识](../../../xdm/schema/composition.md)。

## XDM模式示例

以下是映射到平台中XDM ExperienceEvent和XDM个人Audience Manager的用户档案结构示例。

### ExperienceEvent — 用于实时数据和载入的数据

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM个人用户档案 — 用于用户档案数据

![](images/aam-profile-xdm-for-profile-data.png)

## 如何将字段从Adobe Audience Manager映射到XDM?

有关详细信息，请参阅[Audience Manager映射字段](./mapping/audience-manager.md)的文档。

## 数据管理平台

### 数据集

数据集是存储和管理结构，用于数据集合，通常是表格，它包含模式（列）和字段（行），并通过数据连接使用。 Audience Manager数据包括实时数据、入站数据和用户档案数据。 要定位Audience Manager数据集，请在UI中使用搜索功能，并针对每种类型的数据提供命名约定。

默认情况下，Audience Manager数据集在用户档案时处于禁用状态，用户可以根据其使用案例启用或禁用数据集。 不建议禁用将用作用户档案中区段成员身份的数据集。

| 数据集名称 | 描述 |
| ------------ | ----------- |
| AAM实时 | 此数据集包含由Audience ManagerDCS端点上的直接点击收集的Audience Manager和身份映射。 使此数据集保持启用状态，以获取用户档案。 |
| AAM实时用户档案更新 | 此数据集支持实时定位Audience Manager特征和细分。 它包含有关Edge区域路由、特征和区段成员资格的信息。 使此数据集保持启用状态，以获取用户档案。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换，以直接将数据收录到用户档案。 |
| AAM设备数据 | 具有ECID的设备数据和在Audience Manager中聚集的相应段实现。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换，以直接将数据收录到用户档案。 |
| AAM设备用户档案数据 | 用于Audience Manager连接器诊断。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换，以直接将数据收录到用户档案。 |
| AAM认证用户档案 | 此数据集包含经过Audience Manager验证的用户档案。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换，以直接将数据收录到用户档案。 |
| AAM认证用户档案元数据 | 用于Audience Manager连接器诊断。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换，以直接将数据收录到用户档案。 |
| AAM Devices Data Backfill | 从导入过去的设备数据中获取数据集。 它包含ECID和Audience Manager中聚集的相应细分实现。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换以直接将数据收录到用户档案。 |
| AAM认证用户档案回填 | 数据集导入过去经过身份验证的数据。 它包含经Audience Manager验证的用户档案。 数据在数据集中不以批处理形式显示。 您可以启用&#x200B;**[!UICONTROL Profile]**&#x200B;切换以直接将数据收录到用户档案。 |

### 连接

Adobe Audience Manager在目录中创建一个连接：Audience Manager连接。 Catalog是Adobe Experience Platform中数据位置和谱系记录的系统。 连接是Connectors的客户特定实例的Catalog对象。 有关目录、连接和连接器的详细信息，请参阅[目录服务概述](../../../catalog/home.md)。

## 平台上的Audience Manager数据预期的延迟是什么？

| Audience Manager数据 | 延迟 | 注释 |
| --- | --- | --- |
| 实时数据 | &lt; 35 分钟. | 从在Audience Manager Edge节点捕获到在平台数据湖上显示的时间。 |
| 用户档案数据 | &lt; 2 天 | 从通过DCS/PCS Edge数据和已载入的数据捕获到的时间，被处理到用户用户档案，然后以用户档案显示。 此数据今天不会直接登陆Platform Data Lake。 可以为Audience Manager用户档案数据集启用用户档案切换，以将此数据直接引入用户档案。 |
