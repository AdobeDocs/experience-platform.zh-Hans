---
title: 标记的用户权限
description: 了解可用于标记的不同类型权限以及针对不同业务用例的一些基本实施策略。
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 17%

---

# 标记的用户权限

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中标记的用户权限通过Adobe Admin Console分配给用户。 不同的权限集不会分配给单个用户，而是单独配置为产品配置文件。 然后，会将用户分配到这些产品配置文件，以授予他们配置的权限。

本指南概述了可用于标记的不同类型的权限、它们授予的访问权限以及针对不同业务用例的一些基本实施策略。

>[!NOTE]
>
>有关如何使用Admin Console为用户配置权限的步骤，请参阅 [管理数据收集的权限](../../../collection/permissions.md).

## 权限类型

在产品配置文件中，标记的权限分为四类：

1. 平台
1. 属性
1. 资产权限
1. 公司权限

### 平台

每个标记属性都有一个平台。 当前，可以对标记使用两个平台：Web和移动设备。 您可以使用此权限类型来限制或授予对特定类型属性的访问权限。当管理移动设备应用程序的团队与管理网站的团队不同时，此功能会非常有用。

### 属性

默认情况下，产品配置文件会授予对公司中当前和将来存在的所有资产的访问权限。 使用此权限类型，您可以按名称限制或授予对特定现有属性的访问权限。

### 资产权限 {#property-rights}

您在数据收集UI中创建的任何资产都将在Admin Console中可用，从而允许您使用同一产品配置文件中的特定资产权限对资产进行分组。

例如，如果给定的产品配置文件无权访问资产A1，则属于该配置文件的用户将无法查看或修改资产A1中的任何设置。

如果用户属于有权访问资产A1的配置文件，则他们在资产A1中可以执行的操作取决于他们从该配置文件获得的权限。 如果用户拥有资产A1的权限，但没有分配权限，则他们对该资产具有只读访问权限。

下表概述了可用资产权限及其授予访问权限的功能：

| 资产权限 | 描述 |
| --- | --- |
| **开发** | 这允许您执行以下操作：<ul><li>创建规则和数据元素</li><li>在现有开发环境中创建并构建库</li><li>提交库以供审批</li></ul>数据收集UI中的大多数日常任务都需要此权限。 |
| **批准** | 这允许您获取已提交的库并将其生成到暂存环境。 测试完成后，您还可以批准库以进行发布。 |
| **发布** | 这允许您将已批准的库发布到生产环境。 |
| **管理扩展** | 这允许您执行以下操作： <ul><li>将新扩展安装到资产</li><li>修改已安装扩展的配置</li><li>删除扩展</li></ul>请参阅的扩展概述文档 [有关扩展的更多信息](../managing-resources/extensions/overview.md). 此角色通常属于 IT 或营销组，具体取决于您的组织。 |
| **管理环境** | 这允许您创建和修改环境。 请参阅 [环境文档](../publishing/environments.md) 以了解更多信息。 此角色通常属于 IT 组。 |

{style=&quot;table-layout:auto&quot;}

### 公司权限

公司权限适用于跨多个资产的权限。下表概述了这些内容：

| 公司权 | 描述 |
| --- | --- |
| **管理资产** | 这允许您执行以下操作：<ul><li>创建新资产</li><li>在属性级别修改元数据和设置</li><li>删除属性</li></ul>管理员通常执行此角色。请参阅 [属性文档](companies-and-properties.md) 以了解更多信息。 |
| **开发扩展** | 允许创建和修改公司拥有的扩展包，包括私有版本和公开发布请求。 |
| **管理应用程序配置** | 仅当您拥有Adobe Journey Optimizer的许可证或其他授予对移动应用程序内消息和推送消息访问权限的解决方案时，才可使用此功能。  这允许您管理Experience Cloud了解的应用程序以及与Firebase Cloud Messaging服务和Apple推送通知服务通信所需的推送凭据。 |

{style=&quot;table-layout:auto&quot;}

## 用户总权限

单个用户的总权限取决于其在不同产品配置文件中的总成员资格。 如果用户属于多个产品配置文件，则每个配置文件的权限相加而不是相乘。

例如，产品配置文件A授予您资产1的开发权限。 产品配置文件B授予您资产2的发布权限。 在这种情况下，您可以在资产1中开发，在资产2中发布，但不能在资产1中发布，或在资产2中开发，因为您没有获得执行此操作的明确权限。

## 权限方案

创建新的产品配置文件时，不同的公司具有不同的需求。 这些需求因公司规模、组织结构、网站数量、参与标记管理的人员数量等而异。

在创建产品配置文件并将用户添加到产品配置文件时，您需要考虑以下一些常见方案和建议起点。

### 独掌大权

如果您运营的小公司一切事务均由一人负责，请授予此用户所有资产的权限，并为其分配上面所列的所有权限。

### 职责分离

假设您组织中的许多人参与了标记操作。 您有一组人员（例如外部顾问）负责创建规则和数据元素，但您不希望他们有权访问生产环境。 在这种情况下，您需要确保除IT团队之外，任何人都不能部署到生产环境。

要实现此目的，请执行以下操作：

1. 为顾问创建帐户，并仅授予他们开发权限。
1. 该顾问会在您设定的范围内进行生成和测试。
1. 如果顾问想要新扩展或准备就绪可上线，则您组织的代表（具有相应的权限）会执行这些操作。

### 企业

企业公司可能已按地理区域划分其多个网站，每个地理区域由不同的团队负责。在这些团队中，开发和发布均由不同的人员负责。

这类似于上面的“职责分明”，不同之处在于企业是按地理区域进行组织的。例如，您可以为北美地区创建“开发”配置文件和“发布”配置文件，并为欧洲创建单独的“开发”和“发布”组。

## 示例角色

下表提供了一些示例，说明您在组织中可能拥有的角色类型以及您应该为这些角色分配哪些权限：

| 角色 | 描述 | 属性 | 资产权限 | 公司权限 |
| --- | --- | --- | --- | --- |
| 经理 | 想要查看系统中正在发生的事件，但不应进行任何更改。 | 自动包含 | (None) | （无） |
| 营销人员 | 可以安装扩展并为现有资产设置新标记，但无法发布到暂存或生产环境。 | 自动包含 | <ul><li>开发</li><li>管理扩展</li></ul> | <ul><li>管理资产</li></ul> |
| 移动设备应用程序开发人员 | 负责在本机移动设备应用程序中实施Adobe和第三方解决方案。 | 自动包含 | <ul><li>开发</li><li>管理扩展</li></ul> | <li>管理资产</li><li>管理应用程序配置</li> |
| IT 团队 | 实际上不会修改任何标记，但它们可以完全控制暂存环境和生产环境及其中的内容。 | 自动包含 | （无） | <ul><li>批准</li><li>发布</li><li>管理环境</li></ul> |
| 扩展开发人员 | 开发扩展并可以提交以供审批，但无法发布扩展或将其添加到现有资产。 | 自动包含 | <ul><li>开发</li></ul> | <ul><li>管理资产</li><li>开发扩展</li></ul> |
| 超级用户 | 做所有事。 | 自动包含 | <ul><li>开发</li><li>批准</li><li>发布</li><li>管理扩展</li><li>管理环境</li></ul> | <ul><li>管理资产</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

本文档概述了Experience Platform中标记的可用权限。 有关如何在Adobe Admin Console中为标记配置产品配置文件的步骤，请参阅 [管理数据收集的用户权限](../../../collection/permissions.md).
