---
title: Reactor API指南
description: 利用 Reactor API，开发人员能够以编程方式管理 Adobe Experience Platform 中标记的所有资源。参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 4%

---

# [!DNL Reactor] API指南

Reactor API提供了多个端点，允许您以编程方式管理Adobe Experience Platform中标记的所有资源。

下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅 [入门指南](./getting-started.md) 以了解有关如何对API进行身份验证的重要信息。

要查看所有可用的端点和CRUD操作，请访问 [Reactor API参考](https://www.adobe.io/experience-platform-apis/references/reactor/).

## 公司

公司表示标记用户的组织，通常是企业。 这些公司将1:1与组织ID匹配。 API用户将只能查看他们有权访问的公司。

请参阅 [《公司端点指南》](./endpoints/companies.md) 了解如何在API中查看可用公司。

## 属性

资产是一个容器，其中包含Reactor API中可用的大多数其他资源。 资产不拥有的唯一资源是审核事件、公司、扩展包和配置文件。 资产恰好属于一个公司，并且公司可以拥有多个资产。

请参阅 [属性端点指南](./endpoints/properties.md) 了解如何在API中管理资产。

## 数据元素

数据元素用作指向应用程序中重要数据段的变量。 数据元素在规则和扩展配置中使用。 当规则在浏览器或应用程序的运行时触发时，将解析数据元素的值并在规则中使用。

请参阅 [data elements endpoint指南](./endpoints/data-elements.md) 了解如何管理API中的数据元素。

## 规则

规则控制已部署库中所包含资源的行为。 规则是一个或多个规则组件的组，存在规则时，规则组件会以逻辑方式绑定在一起。

请参阅 [rules endpoint guide](./endpoints/rules.md) 了解如何在API中管理规则。

## 规则组件

规则组件是构成规则的各个项目。 规则组件有三种基本类型：

* **事件**:触发规则的因素
* **条件**:规则检查哪些内容以确定操作
* **操作**:根据是否满足条件，规则会执行哪些内容

请参阅 [rules endpoint guide](./endpoints/rules.md) 了解如何在API中管理规则。

## 扩展包

扩展包表示可供标记用户使用的单个功能的分组。 通常，这些功能以规则组件和数据元素的形式提供，但也可以包括主模块和共享模块。 当扩展包包含在库中时，扩展包提供的功能将作为扩展进行安装。

请参阅 [extension packages endpoint指南](./endpoints/extension-packages.md) 了解如何在API中管理扩展包。

## 扩展

扩展表示扩展包的已安装实例。 扩展可将扩展包定义的功能提供给资产。 创建数据元素和规则组件时，会利用这些功能。

请参阅 [extensions endpoint指南](./endpoints/extensions.md) 以了解如何在API中管理扩展。

## 库

库是资源（扩展、规则和数据元素）的集合，用于表示资产的所需行为。 库将编译为内部版本，并且当这些内部版本从测试向生产流程中不断移动时，会将这些内部版本分配给不同的环境。

请参阅 [库端点指南](./endpoints/libraries.md) 了解如何在API中管理库。

## 内部版本

标记库会编译为内部版本，以便将其分配到环境以进行测试和部署。 内部版本的内容会因库中包含的资源、内部版本被分配到的环境的配置以及内部版本所属的属性的平台而异。

请参阅 [生成endpoint指南](./endpoints/builds.md) 了解如何管理API中的内部版本。

## 环境

环境指示可在其中部署内部版本的特定主机，以及该内部版本是否应部署为一组文件或以存档格式压缩。 在Reactor API中，环境与主机本身是分开的，主机由 `/hosts` 端点。

请参阅 [生成endpoint指南](./endpoints/builds.md) 了解如何管理API中的内部版本。

## 托管

主机表示可在其中交付并最终部署库内部版本的托管目标。 主机可以是Akamai或SFTP服务器。

请参阅 [hosts endpoint指南](./endpoints/hosts.md) 了解如何在API中管理主机。

## 应用程序配置

应用程序配置允许存储和检索凭据以供日后使用。 请参阅 [应用程序配置端点指南](./endpoints/app-configurations.md) 了解如何在API中管理应用程序配置。

## 审核事件

审核事件是在进行更改时生成的对另一个标记资源进行特定更改的记录。 这些是可通过使用回调函数订阅的系统事件。

请参阅 [audit events endpoint指南](./endpoints/audit-events.md) 了解如何在API中管理审核事件。

## 回调

回调是一种消息，每当生成新的审核事件时，Platform都会将该消息发送到URL主机。 请参阅 [callbacks端点指南](./endpoints/callbacks.md) 了解如何在API中管理回调。

## 注释

注释是可添加到某些标签资源的文本批注，例如数据元素、扩展、库、属性、规则和规则组件。 请参阅 [注释终端指南](./endpoints/notes.md) 了解如何在API中管理注释。

## 配置文件

配置文件包含有关已登录用户的所有信息，包括其所属的所有Adobe组织、其所属在每个组织中的产品配置文件，以及他们从每个产品配置文件中拥有的权限。

请参阅 [profile endpoint指南](./endpoints/profile.md) 了解如何在API中查看此信息。

## 搜索

的 `/search` 端点提供了一种查找与所需条件匹配的资源的方法，以查询形式表示。 所有查询的范围均为您当前的公司和可访问属性。 请参阅 [search endpoint指南](./endpoints/search.md) 以了解如何使用此功能。

## 秘密

密钥包含允许事件转发向另一个系统进行身份验证以进行安全数据交换的凭据。 请参阅 [保密指南](./guides/secrets.md) 有关“机密在事件转发中的运行方式”的概述，以及 [secrets endpoint指南](./endpoints/secrets.md) 了解如何在Reactor API中管理它们。

## 后续步骤

要开始使用架构注册表API进行调用，请阅读 [入门指南](./getting-started.md) 然后，选择一个端点指南以了解如何使用特定端点。
