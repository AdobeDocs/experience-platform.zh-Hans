---
keywords: Experience Platform;home;popular topics;Audience Manager connector;Audience manager;audience manager
solution: Experience Platform
title: Audience Manager连接器
topic: overview
description: Adobe Audience Manager数据连接器将在Adobe Audience Manager收集的第一方数据传送到Adobe Experience Platform。 Audience Manager连接器将三类别数据引入平台。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---


# Audience Manager连接器

Adobe Audience Manager数据连接器将在Adobe Audience Manager收集的第一方数据传送到Adobe Experience Platform。 Audience Manager连接器将三类别数据引入平台：

- **实时数据：** 在Audience Manager的数据收集服务器上实时捕获数据。 此数据用于Audience Manager以填充基于规则的特征，并将在最短的延迟时间内在平台中显示。
- **用户档案数据：** Audience Manager使用实时和载入的数据来推导客户用户档案。 这些用户档案用于填充区段实现上的身份图和特征。

Audience Manager连接器将这些类别映射到体验数据模型(XDM)模式，并将其发送到平台。 实时数据以XDM ExperienceEvent数据的形式发送，而用户档案数据以XDM单个用户档案的形式发送。

有关使用平台UI创建与Adobe Audience Manager的连接的说明，请参阅 [Audience Manager连接器教程](../../tutorials/ui/create/adobe-applications/audience-manager.md)。

## 什么是体验数据模型(XDM)?

XDM是一个公开记录的规范，它提供一个标准化框架，平台通过该框架组织客户体验数据。

遵循XDM标准，可统一整合客户体验数据，从而更轻松地提供数据和收集信息。

有关如何在Experience Platform中使用XDM的更多信息，请参 [阅XDM系统概述](../../../xdm/home.md)。 要进一步了解用户档案和ExperienceEvent等XDM模式的结构，请参阅 [模式合成基础知识](../../../xdm/schema/composition.md)。

## XDM模式示例

以下是映射到XDM ExperienceEvent和XDM Individual Platform的Audience Manager结构示例。

### ExperienceEvent —— 用于实时数据和载入的数据

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM个人用户档案-用于用户档案数据

![](images/aam-profile-xdm-for-profile-data.png)

## 如何将字段从Adobe Audience Manager映射到XDM?

有关详细信息，请参 [阅Audience Manager映射](./mapping/audience-manager.md) 字段的文档。

## 数据管理平台

### 数据集

数据集是存储和管理结构，用于模式集合，通常是表，它包含（列）和字段（行），并由数据连接提供。 Audience Manager数据包括实时数据、入站数据和用户档案数据。 要查找Audience Manager数据集，请在UI中使用搜索功能，并针对每种类型的数据提供命名约定。

Audience Manager数据集在默认情况下处于禁用状态，并且用户能够根据其使用案例启用或禁用数据集。 不建议禁用将用于用户档案中段成员资格的数据集。

| 数据集名称 | 描述 |
| ------------ | ----------- |
| Audience Manager实时 | 此数据集包含由Audience ManagerDCS端点上的直接点击收集的数据和Audience Manager用户档案的标识图。 启用此数据集进行用户档案摄取。 |
| Audience Manager实时用户档案更新 | 此数据集支持Audience Manager特征和区段的实时定位。 它包含Edge区域路由、特征和区段成员资格的信息。 启用此数据集进行用户档案摄取。 |
| Audience Manager设备数据 | 具有ECID的设备数据以及在Audience Manager中聚集的相应细分实现。 |
| Audience Manager设备用户档案数据 | 用于Audience Manager连接器诊断。 |
| Audience Manager验证用户档案 | 此数据集包含经Audience Manager验证的用户档案。 |
| Audience Manager认证用户档案元数据 | 用于Audience Manager连接器诊断。 |

### 连接

Adobe Audience Manager在目录中创建一个连接： **Audience Manager连接**。 目录是Adobe Experience Platform境内数据位置和谱系记录系统。 连接是Connectors客户特定实例的Catalog对象。 有关目录、 [连接和连接器](../../../catalog/home.md) ，请参阅目录服务概述。

## 平台上Audience Manager数据的预期延迟是什么？

| Audience Manager数据 | 延迟 | 注释 |
| --- | --- | --- |
| 实时数据 | &lt; 35 分钟. | 从在Realtime节点捕获到在Platform Data Lake上显示的时间。 |
| 入站数据 | &lt; 13 小时 | 从在S3存储桶捕获到在平台数据湖上显示的时间。 |
| 用户档案数据 | &lt; 2 天 | 从实时／入站数据捕获到添加到用户用户档案并最终显示在平台数据湖上的时间。 |