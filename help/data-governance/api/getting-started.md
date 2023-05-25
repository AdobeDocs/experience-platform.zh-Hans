---
keywords: Experience Platform；主页；热门主题；DULE；dule
solution: Experience Platform
title: 策略服务API快速入门
description: 策略服务API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用策略服务API之前需要了解的核心概念。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 入门 [!DNL Policy Service] API

此 [!DNL Policy Service] API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用 [!DNL Policy Service] API。

## 先决条件

使用开发人员指南需要对各种 [!DNL Experience Platform] 使用数据管理功能涉及的服务。 开始使用之前 [!DNL Policy Service API]，请查看以下服务的文档：

* [数据管理](../home.md)：用于执行操作的框架 [!DNL Experience Platform] 强制执行数据使用合规性。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 正在读取示例API调用

此 [!DNL Policy Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需的标头

此API文档还要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将为中的每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]包括那些属于数据管理的，均被隔离到特定的虚拟沙盒中。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 核心资源与自定义资源

在 [!DNL Policy Service] API、所有策略和营销操作均称为 `core` 或 `custom` 资源。

`core` 资源是由Adobe定义和维护，而 `custom` 资源是由您的组织创建和维护的资源，因此是唯一的并且仅对您的组织可见。 因此，列出和查找操作(`GET`)是唯一允许对执行的操作 `core` 资源，而列出、查找和更新操作(`POST`， `PUT`， `PATCH`、和 `DELETE`)可用于 `custom` 资源。

## 后续步骤

要开始使用策略服务API进行调用，请选择一个可用的端点指南。
