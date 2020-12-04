---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: 策略服务API快速入门
topic: developer guide
description: 策略服务API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用策略服务API之前需要了解的核心概念。
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Getting started with the [!DNL Policy Service] API

API [!DNL Policy Service] 允许您创建和管理与Adobe Experience Platform相关的各种资源 [!DNL Data Governance]。 此文档介绍了在尝试调用API之前需要了解的核心概 [!DNL Policy Service] 念。

## 先决条件

使用开发人员指南需要对使用数据管理功能时 [!DNL Experience Platform] 涉及的各种服务进行有效的了解。 在开始使用之前，请 [!DNL Policy Service API]查阅以下服务的文档：

* [[!DNL Data Governance]](../home.md):强制执行数据使 [!DNL Experience Platform] 用合规性的框架。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 读取示例API调用

API文 [!DNL Policy Service] 档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

## 所需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用端点 [!DNL Platform] 。 完成身份验证教程可为API调用中每个所需标头 [!DNL Experience Platform] 提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Data Governance]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

* `Content-Type: application/json`

## 核心与自定义资源

在API [!DNL Policy Service] 中，所有策略和营销操作称为 `core` 或资 `custom` 源。

`core` 资源是Adobe定义和维护的资源，而 `custom` 资源是您的组织创建和维护的资源，因此，资源是唯一的，仅对您的IMS组织可见。 因此，列表和查找操作(`GET`)是允许对资源执行的唯一 `core` 操作，而列表、查找和更新操作(`POST`、 `PUT`、 `PATCH`和 `DELETE`)可用于资 `custom` 源。

## 后续步骤

要开始使用策略服务API进行调用，请选择可用的端点指南之一。