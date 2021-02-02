---
keywords: Experience Platform；主页；热门主题；模块；
solution: Experience Platform
title: 策略服务API快速入门
topic: developer guide
description: 策略服务API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用策略服务API之前需要了解的核心概念。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# [!DNL Policy Service] API入门

[!DNL Policy Service] API允许您创建和管理与Adobe Experience Platform[!DNL Data Governance]相关的各种资源。 本文档介绍了在尝试调用[!DNL Policy Service] API之前需要了解的核心概念。

## 先决条件

使用开发人员指南需要对使用数据管理功能时涉及的各种[!DNL Experience Platform]服务进行有效的了解。 在开始使用[!DNL Policy Service API]之前，请查看以下服务的文档：

* [[!DNL Data Governance]](../home.md):强制执行数据使 [!DNL Experience Platform] 用合规性的框架。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 读取示例API调用

[!DNL Policy Service] API文档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

## 所需的标题

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用[!DNL Platform]端点。 完成身份验证教程后，将为[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Data Governance]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

* `Content-Type: application/json`

## 核心与自定义资源

在[!DNL Policy Service] API中，所有策略和营销操作称为`core`或`custom`资源。

`core` 资源是Adobe定义和维护的资源，而 `custom` 资源是您的组织创建和维护的资源，因此，资源是唯一的，仅对您的IMS组织可见。因此，列表和查找操作(`GET`)是允许对`core`资源执行的唯一操作，而列表、查找和更新操作（`POST`、`PUT`、`PATCH`和`DELETE`）可用于`custom`资源。

## 后续步骤

要开始使用策略服务API进行调用，请选择可用的端点指南之一。