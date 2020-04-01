---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: DULE Policy Service API开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# DULE Policy Service API开发人员指南

数据使用标签和强制执行(DULE)是Adobe Experience Platform数据管理的核心机制。 DULE策略服务提供了一个RESTful API，它允许您创建和管理数据使用策略，以确定可以针对已标记有某些数据使用标签的数据采取哪些营销操作。

本文档提供了有关执行策略服务API中可用的关键操作的说明。 如果您尚未这样做，请首先查看“数据管理”概 [述](../home.md) ，以熟悉DULE框架。 有关创建和实施DULE策略的分步说明，请参阅 [DULE策略教程](../policies/create.md)。

本文档介绍了在尝试调用策略服务API之前需要了解的核心概念。

## DULE Policy Service快速入门

在开始使用策略服务之前，Experience Platform上的数据必须应用相应的DULE标签。 有关将数据使用标签应用到数据集和字段的完整分步说明，请参阅 [DULE标签用户指南](../labels/user-guide.md)。

## 先决条件

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [数据管理](../home.md):Experience Platform强制遵循数据使用的框架。
   * [DULE标签](../labels/overview.md):数据使用标签将应用于体验数据模型(XDM)数据字段，为访问该数据的方式指定限制。
* [体验数据模型(XDM)系统](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

## 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于数据管理的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## 核心与自定义资源

在策略服务API中，所有策略和营销操作都称为或 `core` 资 `custom` 源。

资 `core``custom` 源由Adobe定义和维护，而资源由个人客户创建和维护，因此，资源是唯一的，仅对创建资源的IMS组织可见。 因此，列表和查找操作(`GET`)是对资源允许的唯一操作，而列表、查找和更新操作( `core` 、`POST`、 `PUT`和 `PATCH`)可用于资 `DELETE``custom` 源。

## 策略状态

数据使用策略可以具有以下三种可能的状态之一： `DRAFT`、 `ENABLED`或 `DISABLED`。

默认情况下，只有“ENABLED”策略参与策略评估。

&quot;草案&quot;政策也可在政策评估中考虑，但只能通过设置查询参数来考虑 `?includeDraft=true`。 有关政策评估的更多信息，请参阅本文档 [末尾的](../enforcement/overview.md) “政策执行文档”一节。

## 营销操作名称 {#marketing-actions}

营销活动名称是营销活动的唯一标识符。 每个 `core` 营销操作都有一个唯一的名称，该名称适用于所有IMS组织。 这些名称由Adobe定义和维护。 同时，所有客户定义的营销操作(`custom` 资源)在您的单个组织内都是独一无二的，不可见或与其他IMS组织共享。

本文档后面的“营销操作”部分概述了在策略服务API中使 [用营销操作的步骤](#marketing-actions) 。

## 后续步骤

既然您已具备入门知识和凭据，您可以继续阅读本开发人员指南中提供的示例API调用：

* [营销操作](marketing-actions.md)
* [策略](policies.md)