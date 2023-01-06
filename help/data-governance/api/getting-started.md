---
keywords: Experience Platform；主页；热门主题；DULE;DULE
solution: Experience Platform
title: 策略服务API快速入门
description: 策略服务API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档简要介绍在尝试调用策略服务API之前需要了解的核心概念。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 入门 [!DNL Policy Service] API

的 [!DNL Policy Service] API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档简要介绍在尝试调用 [!DNL Policy Service] API。

## 先决条件

使用开发人员指南需要对 [!DNL Experience Platform] 使用“数据管理”功能时涉及的服务。 开始使用之前 [!DNL Policy Service API]，请查阅以下服务的文档：

* [数据管理](../home.md):框架 [!DNL Experience Platform] 强制实施数据使用合规性。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 读取示例API调用

的 [!DNL Policy Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需标题

API文档还要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将提供 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于“数据管理”的沙箱，则与特定的虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

## 核心资源与自定义资源

在 [!DNL Policy Service] API中，所有策略和营销操作都称为 `core` 或 `custom` 资源。

`core` 资源是指由Adobe定义和维护的资源，而 `custom` 资源是由您的组织创建和维护的资源，因此仅对您的IMS组织是唯一可见的。 因此，列出和查找操作(`GET`)是 `core` 资源，而则列出、查找和更新操作(`POST`, `PUT`, `PATCH`和 `DELETE`)可用于 `custom` 资源。

## 后续步骤

要开始使用策略服务API进行调用，请选择一个可用的端点指南。
