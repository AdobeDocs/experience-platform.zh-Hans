---
keywords: Experience Platform；主页；热门主题；DULE；dule
solution: Experience Platform
title: 策略服务API快速入门
description: 策略服务API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用策略服务API之前需要了解的核心概念。
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# [!DNL Policy Service] API快速入门

[!DNL Policy Service] API允许您创建和管理与Adobe Experience Platform数据管理相关的各种资源。 本文档介绍了在尝试调用[!DNL Policy Service] API之前需要了解的核心概念。

## 先决条件

使用开发人员指南需要对使用数据管理功能所涉及的各种[!DNL Experience Platform]服务有一定的了解。 在开始使用[!DNL Policy Service API]之前，请查看以下服务的文档：

* [数据管理](../home.md)： [!DNL Experience Platform]强制数据使用合规性的框架。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 正在读取示例 API 调用

[!DNL Policy Service] API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform]端点。 完成身份验证教程将提供[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于数据管理的所有资源）均与特定的虚拟沙盒隔离。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 核心资源与自定义资源

在[!DNL Policy Service] API中，所有策略和营销操作都称为`core`或`custom`资源。

`core`资源是由Adobe定义和维护的资源，而`custom`资源是由您的组织创建和维护的资源，因此是唯一的并且仅对您的组织可见。 因此，列表和查找操作(`GET`)是唯一允许对`core`资源执行的操作，而列表、查找和更新操作（`POST`、`PUT`、`PATCH`和`DELETE`）可用于`custom`资源。

## 后续步骤

要开始使用策略服务API进行调用，请选择一个可用的端点指南。
