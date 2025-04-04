---
title: 扩展开发概述
description: 了解 Adobe Experience Platform 中的不同标记扩展类型的主要组件以及扩展开发流程。
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 23%

---

# 扩展开发概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

Adobe Experience Platform中标记的主要目标之一是创建一个开放的生态系统，在该生态系统中，Adobe以外的工程师可以在其网站和移动应用程序上展示其他功能。 这可以通过标记扩展来实现。 将扩展安装在标记资产上后，该扩展的功能即可供该资产的所有用户使用。

本文档概述了扩展的主要组件，并提供了指向更多文档的链接，以帮助您完成扩展开发过程。

## 扩展结构

扩展由文件目录组成。具体而言，扩展包含清单文件、库模块和视图。

### 清单文件

清单文件([`extension.json`](./manifest.md))必须存在于目录的根中。 此文件描述扩展的组成以及某些文件在目录中的位置。 清单的功能与[npm](https://www.npmjs.com/)项目中的[`package.json`](https://docs.npmjs.com/files/package.json)文件类似。

### 库模块

库模块是描述扩展提供的不同[组件](#components)的文件（换句话说，就是要在标记运行时库中发出的逻辑）。 每个库模块文件的内容必须遵循[CommonJS模块标准](https://nodejs.org/api/modules.html#modules-commonjs-modules)。

例如，如果要构建名为“发送信标”的操作类型，则必须拥有一个包含发送信标逻辑的文件。 如果使用JavaScript，则文件可以称为`sendBeacon.js`。 此文件的内容将在标记运行时库中发出。

您可以将库模块文件放在扩展目录中的任何位置，但前提是说明它们在`extension.json`中的位置。

### 视图

视图是一个HTML文件，该文件能够加载到Tags应用程序中的[`iframe`元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe)中，尤其是通过Experience Platform UI和数据收集UI。 视图必须包含由扩展提供的脚本，并符合小型API要求，才能与应用程序进行通信。

对于任何扩展，最重要的视图文件都是其配置。 有关详细信息，请参阅[扩展配置](#configuration)部分。

对于在视图中使用的库，目前没有任何限制。换言之，您可以使用jQuery、Underscore、React、Angular、Bootstrap或其他。 但是，仍建议让扩展具有与UI相似的外观。

建议将所有与视图相关的文件（HTML、CSS、JavaScript）放置在与库模块文件分离的单个子目录中。在`extension.json`中，您可以描述此视图子目录的位置。 然后，Experience Platform将从其Web服务器为此子目录（仅此子目录）提供服务。

## 库组件 {#components}

每个扩展定义了一组功能。 这些功能通过包含在部署到您的网站或应用程序的[库](../ui/publishing/libraries.md)中来实现。 库是单个组件的集合，包括条件、操作、数据元素等。 每个库组件都是一段可重用代码（由扩展提供），它会在标记运行时内发出。

根据您正在开发的是Web扩展还是Edge扩展，可用组件类型及其用例会有所不同。 有关每种扩展类型可用的组件的概述，请参阅下面的子部分。

### Web扩展的组件 {#web}

在 Web 扩展中，规则是通过事件触发的，如果满足给定的条件集，规则即可执行特定的操作。有关更多信息，请参阅有关 [Web 扩展中的模块流](./web/flow.md)的概述。

除了Adobe提供的[核心模块](./web/core.md)之外，您还可以在Web扩展中定义以下库组件：

* [事件](./web/event-types.md)
* [条件](./web/condition-types.md)
* [操作](./web/action-types.md)
* [数据元素](./web/data-element-types.md)
* [共享模块](./web/shared.md)

>[!NOTE]
>
>有关在Web扩展中实施库组件所需格式的详细信息，请参阅[模块格式概述](./web/format.md)。

### Edge扩展的组件 {#edge}

在 Edge 扩展中，规则是通过条件检查触发的，如果这些检查通过，规则将执行特定的操作。有关详细信息，请参阅[Edge扩展流程](./edge/flow.md)的概述。

您可以在Edge扩展中定义以下库组件：

* [条件](./edge/condition-types.md)
* [操作](./edge/action-types.md)
* [数据元素](./edge/data-element-types.md)

>[!NOTE]
>
>有关在 Edge 扩展中实施库模块所需格式的详细信息，请参阅[模块格式概述](./edge/format.md)。

## 扩展配置 {#configuration}

扩展配置是指收集来自用户的全局设置的方式。配置由一个视图组件组成，该组件将标记运行时库中的设置作为纯对象导出和发出。

例如，假定某个扩展允许用户使用“发送信标”操作发送信标，并且该信标必须始终包含帐户ID。 每次配置“Send Beacon”操作时，扩展都不应询问用户帐户ID，而是应从扩展配置视图中询问一次帐户ID。 每次发送信标时，“Send Beacon”操作都可从扩展配置中提取帐户ID并将其添加到信标。

当用户在UI中将扩展安装到属性时，将向用户显示扩展配置视图，用户必须完成该视图才能完成安装。

若要了解详细信息，请参阅[扩展配置](./configuration.md)指南。

## 提交扩展

构建完扩展后，您可以提交该扩展，以将其列在Experience Platform的扩展目录中。 有关详细信息，请参阅[扩展提交过程概述](./submit/overview.md)。
