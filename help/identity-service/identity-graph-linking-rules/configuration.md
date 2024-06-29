---
title: 身份图链接规则配置指南
description: 了解在使用身份图链接规则配置实施数据时要遵循的建议步骤。
badge: Beta 版
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 5%

---

# 身份图链接规则配置指南

阅读本文档以了解在使用Adobe Experience Platform Identity服务实施数据时可以遵循的分步指南。

分步概述：

1. [创建必要的身份命名空间](#namespace)
2. [使用图形仿真工具熟悉身份优化算法](#graph-simulation)
3. [使用身份设置工具指定唯一的命名空间并配置命名空间的优先级排名](#identity-settings)
4. [创建Experience Data Model (XDM)架构](#schema)
5. [创建数据集](#dataset)
6. [将您的数据摄取到Experience Platform](#ingest)

## 实施前先决条件

在开始之前，您必须首先确保系统中的已验证事件始终包含人员标识符。

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## 创建您的身份命名空间 {#namespace}

如果您的数据需要它，则必须首先为组织创建适当的命名空间。 有关如何创建自定义命名空间的步骤，请阅读上的指南 [在UI中创建自定义命名空间](../features/namespaces.md#create-custom-namespaces).

## 使用图形模拟工具 {#graph-simulation}

接下来，导航到 [图形仿真工具](./graph-simulation.md) 在Identity Service UI工作区中。 您可以使用图形模拟工具来模拟使用各种不同的唯一命名空间和命名空间优先级配置构建的身份图形。

通过创建不同的配置，您可以使用图形模拟工具来学习和更好地了解身份优化算法和某些配置如何影响图形的行为。

## 配置身份设置 {#identity-settings}

当您更好地了解了希望图形的行为方式后，可导航至 [身份设置工具](./identity-settings-ui.md) 在Identity Service UI工作区中。

使用身份设置工具指定唯一的命名空间并按优先级配置命名空间。 完成应用设置后，必须至少等待六小时才能继续摄取数据，因为新设置至少需要六小时才能反映在Identity Service中。

## 创建 XDM 架构 {#schema}

在建立唯一的命名空间和命名空间优先级后，您现在可以继续进行所需的设置以摄取数据。 首先，必须创建XDM架构。 根据您的数据，您可能需要为XDM Individual Profile和XDM ExperienceEvent创建架构。

要将数据摄取到Real-time Customer Profile，您必须确保您的架构至少包含一个已指定为主标识的字段。 通过设置主要身份，您可以为配置文件摄取启用给定架构。

有关如何创建架构的说明，请阅读以下内容的指南： [在UI中创建XDM架构](../../xdm/tutorials/create-schema-ui.md).

## 创建数据集 {#dataset}

接下来，创建一个数据集以为要摄取的数据提供结构。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集与架构配合使用，要将数据摄取到Real-time Customer Profile，必须为数据集启用配置文件摄取。 要为配置文件启用数据集，它必须引用为配置文件摄取启用的架构。

有关如何创建数据集的说明，请参阅 [数据集用户界面指南](../../catalog/datasets/user-guide.md).

## 引入数据 {#ingest}

此时，您应该具备以下内容：

* 访问Identity Service功能所需的权限。
* 数据的命名空间。
* 为命名空间指定的唯一命名空间和配置的优先级。
* 至少一个XDM架构。 （根据您的数据和特定用例，您可能需要创建用户档案和体验事件架构。）
* 基于架构的数据集。

完成上面列出的所有项目后，即可开始摄取数据以Experience Platform。 您可以通过多种不同的方式执行数据摄取。 您可以使用以下服务将数据引入Experience Platform：

* [批量摄取和流式摄取](../../ingestion/home.md)
* [Experience Platform中的数据收集](../../collection/home.md)
* [Experience Platform源](../../sources/home.md)

>[!TIP]
>
>摄取数据后，XDM原始数据有效负载不会发生更改。 您仍可能会在UI中看到主要身份配置。 但是，这些配置将由身份设置覆盖。

如有任何反馈，请使用 **[!UICONTROL Beta反馈]** 选项。