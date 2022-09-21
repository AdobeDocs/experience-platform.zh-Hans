---
title: 扩展开发概述
description: 了解 Adobe Experience Platform 中的不同标记扩展类型的主要组件以及扩展开发流程。
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 22%

---

# 扩展开发概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

Adobe Experience Platform中标记的主要目标之一是创建一个开放的生态系统，在该生态系统中，Adobe以外的工程师可以在其网站和移动设备应用程序上展示其他功能。 这可通过标记扩展实现。 在标记资产上安装扩展后，该扩展的功能便可供该资产的所有用户使用。

本文档概述了扩展的主要组件，并提供了指向进一步文档的链接，以帮助您了解扩展开发过程。

## 扩展结构

扩展由文件目录组成。具体而言，扩展包含清单文件、库模块和视图。

### 清单文件

清单文件([`extension.json`](./manifest.md))必须存在于目录的根中。 此文件描述扩展的组成以及某些文件在目录中的位置。 清单的函数与 [`package.json`](https://docs.npmjs.com/files/package.json) 文件 [npm](https://www.npmjs.com/) 项目。

### 库模块

库模块是描述不同 [组件](#components) 扩展提供的逻辑（换言之，将在标记运行时库中发出的逻辑）。 每个库模块文件的内容必须跟在 [CommonJS模块标准](https://nodejs.org/api/modules.html#modules-commonjs-modules).

例如，如果您要构建名为“send beacon”的操作类型，则必须有一个包含用于发送信标的逻辑的文件。 如果使用JavaScript，则可以调用文件 `sendBeacon.js`. 此文件的内容将在标记运行时库中发出。

您可以将库模块文件放置在扩展目录中所需的任意位置，前提是您要描述它们在 `extension.json`.

### 视图

视图是能够加载到 [`iframe` 元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe) ，尤其是通过平台UI和数据收集UI。 视图必须包含由扩展提供的脚本，并符合小型API，才能与应用程序通信。

任何扩展最重要的视图文件都是其配置。 请参阅 [扩展配置](#configuration) 以了解更多信息。

对于在视图中使用的库，目前没有任何限制。换言之，您可以使用jQuery、Underscore、React、Angular、Bootstrap或其他变量。 但是，仍建议使扩展具有与UI类似的外观。

建议将所有与视图相关的文件（HTML、CSS、JavaScript）放置在与库模块文件分离的单个子目录中。在 `extension.json`，则可以描述此视图子目录的位置。 然后，平台将从其Web服务器中提供此子目录（仅此子目录）。

## 库组件 {#components}

每个扩展定义一组功能。 这些功能通过在 [库](../ui/publishing/libraries.md) 部署到您的网站或应用程序的。 库是单个组件的集合，包括条件、操作、数据元素等。 每个库组件都是在标记运行时内发出的一段可重用代码（由扩展提供）。

根据您是开发Web扩展还是边缘扩展，可用的组件类型及其用例会有所不同。 有关每种扩展类型都有哪些组件可用的概述，请参阅以下子部分。

### Web扩展组件 {#web}

在 Web 扩展中，规则是通过事件触发的，如果满足给定的条件集，规则即可执行特定的操作。有关更多信息，请参阅有关 [Web 扩展中的模块流](./web/flow.md)的概述。

除 [核心模块](./web/core.md) 由Adobe提供，您可以在web扩展中定义以下库组件：

* [事件](./web/event-types.md)
* [条件](./web/condition-types.md)
* [操作](./web/action-types.md)
* [数据元素](./web/data-element-types.md)
* [共享模块](./web/shared.md)

>[!NOTE]
>
>有关在Web扩展中实施库组件所需的格式的详细信息，请参阅 [模块格式概述](./web/format.md).

### 边缘扩展的组件 {#edge}

在 Edge 扩展中，规则是通过条件检查触发的，如果这些检查通过，规则将执行特定的操作。请参阅 [边缘扩展流](./edge/flow.md) 以了解更多信息。

您可以在边缘扩展中定义以下库组件：

* [条件](./edge/condition-types.md)
* [操作](./edge/action-types.md)
* [数据元素](./edge/data-element-types.md)

>[!NOTE]
>
>有关在 Edge 扩展中实施库模块所需格式的详细信息，请参阅[模块格式概述](./edge/format.md)。

## 扩展配置 {#configuration}

扩展配置是指收集来自用户的全局设置的方式。该配置由一个视图组件组成，该组件将标记运行时库中的设置导出并作为纯对象发出。

例如，假定某个扩展允许用户使用“发送信标”操作发送信标，并且该信标必须始终包含帐户ID。 扩展不应在用户每次配置“发送信标”操作时都要求其提供帐户ID，而应从扩展配置视图中询问一次帐户ID。 每次发送信标时，“发送信标”操作都可以从扩展配置中提取帐户ID并将其添加到信标。

当用户在UI中将扩展安装到资产时，会向用户显示扩展配置视图，用户必须完成该视图才能完成安装。

要了解更多信息，请参阅 [扩展配置](./configuration.md).

## 提交扩展

构建完扩展后，您可以提交该扩展以将其列在Platform的扩展目录中。 请参阅 [扩展提交流程概述](./submit/overview.md) 以了解更多信息。
