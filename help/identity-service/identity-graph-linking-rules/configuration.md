---
title: 身份图链接规则配置指南
description: 了解在使用身份图链接规则配置实施数据时要遵循的建议步骤。
badge: Beta 版
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 4%

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

## 设置权限 {#set-permissions}

Identity Service实施流程的第一步是，确保将您的Experience Platform帐户添加到设置了必要权限的角色中。 管理员可通过导航到Adobe Experience Cloud中的权限UI，配置您帐户的权限。 从那里，必须将您的帐户添加到具有以下权限的角色：

* [!UICONTROL 查看身份设置]：应用此权限以便在身份命名空间浏览页中查看唯一的命名空间和命名空间优先级。
* [!UICONTROL 编辑身份设置]：应用此权限以便能够编辑和保存您的身份设置。

有关权限的详细信息，请阅读[权限指南](../../access-control/abac/ui/permissions.md)。

## 创建您的身份命名空间 {#namespace}

如果您的数据需要它，则必须首先为组织创建适当的命名空间。 有关如何创建自定义命名空间的步骤，请阅读有关[在UI中创建自定义命名空间](../features/namespaces.md#create-custom-namespaces)的指南。

## 使用图形模拟工具 {#graph-simulation}

接下来，导航到Identity Service UI工作区中的[图形模拟工具](./graph-simulation.md)。 您可以使用图形模拟工具来模拟使用各种不同的唯一命名空间和命名空间优先级配置构建的身份图形。

通过创建不同的配置，您可以使用图形模拟工具来学习和更好地了解身份优化算法和某些配置如何影响图形的行为。

## 配置身份设置 {#identity-settings}

了解图形的行为方式后，请导航到Identity Service UI工作区中的[身份设置工具](./identity-settings-ui.md)。

使用身份设置工具指定唯一的命名空间并按优先级配置命名空间。 完成应用设置后，必须至少等待六小时才能继续摄取数据，因为新设置至少需要六小时才能反映在Identity Service中。

## 创建 XDM 架构 {#schema}

在建立唯一的命名空间和命名空间优先级后，您现在可以继续进行所需的设置以摄取数据。 首先，必须创建XDM架构。 根据您的数据，您可能需要为XDM Individual Profile和XDM ExperienceEvent创建架构。

要将数据摄取到Real-time Customer Profile，您必须确保您的架构至少包含一个已指定为主标识的字段。 通过设置主要身份，您可以为配置文件摄取启用给定架构。

有关如何创建架构的说明，请阅读有关[在UI中创建XDM架构](../../xdm/tutorials/create-schema-ui.md)的指南。

## 创建数据集 {#dataset}

接下来，创建一个数据集以为要摄取的数据提供结构。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集与架构配合使用，要将数据摄取到Real-time Customer Profile，必须为数据集启用配置文件摄取。 要为配置文件启用数据集，它必须引用为配置文件摄取启用的架构。

有关如何创建数据集的说明，请阅读[数据集UI指南](../../catalog/datasets/user-guide.md)。

## 引入数据 {#ingest}

此时，您应该具备以下内容：

* 访问Identity Service功能所需的权限。
* 数据的命名空间。
* 为命名空间指定的唯一命名空间和配置的优先级。
* 至少一个XDM架构。 （根据您的数据和特定用例，您可能需要创建用户档案和体验事件架构。）
* 基于架构的数据集。

完成上面列出的所有项目后，即可开始摄取数据以Experience Platform。 您可以通过多种不同的方式执行数据摄取。 您可以使用以下服务将数据引入Experience Platform：

* [批处理摄取和流式摄取](../../ingestion/home.md)
* [Experience Platform中的数据收集](../../collection/home.md)
* [Experience Platform源](../../sources/home.md)

>[!TIP]
>
>摄取数据后，XDM原始数据有效负载不会发生更改。 您仍可能会在UI中看到主要身份配置。 但是，这些配置将由身份设置覆盖。

若要获得任何反馈，请使用Identity Service UI工作区中的&#x200B;**[!UICONTROL Beta反馈]**&#x200B;选项。