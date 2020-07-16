---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: DULE Policy Service API开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# DULE [!DNL Policy Service] API开发人员指南

数据使用标签与强制(DULE)是Adobe Experience Platform的核心机制 [!DNL Data Governance]。 DULE提 [!DNL Policy Service] 供一个RESTful API，它允许您创建和管理数据使用策略，以确定可以对带有特定数据使用标签的数据进行哪些营销操作。

此文档提供了有关执行API中可用的关键操作的 [!DNL Policy Service] 说明。 如果您尚未这样做，请首先查看“数据管 [理”概述](../home.md) ，以熟悉DULE框架。 有关创建和实施DULE策略的分步说明，请参阅 [DULE策略教程](../policies/create.md)。

此文档介绍了在尝试调用API之前需要了解的核心概 [!DNL Policy Service] 念。

## DULE快速入门 [!DNL Policy Service]

在开始使用之前， [!DNL Policy Service]上的数据必 [!DNL Experience Platform] 须应用相应的DULE标签。 有关将数据使用标签应用到数据集和字段的完整分步说明，请参阅DULE标 [签用户指南](../labels/user-guide.md)。

## 先决条件

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [!DNL Data Governance](../home.md): 强制执行数据使 [!DNL Experience Platform] 用合规性的框架。
   * [DULE标签](../labels/overview.md): 数据使用标签应用 [!DNL Experience Data Model] 于(XDM)数据字段，指定如何访问该数据的限制。
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): 组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [!DNL Real-time Customer Profile](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

## 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Data Governance]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型： application/json

## 核心与自定义资源

在API [!DNL Policy Service] 中，所有策略和营销操作称为 `core` 或资 `custom` 源。

资 `core` 源由Adobe定义和维护，而资源由 `custom` 个别客户创建和维护，因此，资源是唯一的，仅对创建资源的IMS组织可见。 因此，列表和查找操作(`GET`)是允许对资源执行的唯一 `core` 操作，而列表、查找和更新操作(`POST`、 `PUT`、 `PATCH`和 `DELETE`)可用于资 `custom` 源。

## 策略状态

数据使用策略可以具有以下三种可能的状态之一： `DRAFT`、 `ENABLED`或 `DISABLED`。

默认情况下，只有“ENABLED”策略参与策略评估。

&quot;DRAFT&quot;策略也可在策略评估中考虑，但只能通过设置查询参数来考虑 `?includeDraft=true`。 有关策略评估的更多信息，请参阅本文档 [末尾的](../enforcement/overview.md) “策略执行文档”一节。

## 营销操作名称 {#marketing-actions}

营销活动名称是营销活动的唯一标识符。 每个 `core` 营销操作都有一个在所有IMS组织中应用的唯一名称。 这些名称由Adobe定义和维护。 同时，所有客户定义的营销行动(`custom` 资源)在您的单个组织中是独一无二的，不可见或与其他IMS组织共享。

在此文档后面的“营销操作 [!DNL Policy Service] ”部分中概述了 [在API中使用](#marketing-actions) 营销操作的步骤。

## 后续步骤

现在您已具备入门知识和凭据，您可以继续阅读本开发人员指南中提供的示例API调用：

* [营销操作](marketing-actions.md)
* [策略](policies.md)