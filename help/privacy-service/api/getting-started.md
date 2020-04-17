---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隐私服务开发人员指南
description: 使用RESTful API跨Adobe Experience Cloud应用程序管理数据主体的个人数据
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# 隐私服务开发人员指南

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理（访问和删除）数据主体（客户）的个人数据。 隐私服务还提供了一个中央审核和记录机制，允许您访问涉及Experience Cloud应用程序的作业的状态和结果。

本指南介绍如何使用Privacy Service API。 有关如何使用UI的详细信息，请参阅隐 [私服务UI概述](../ui/overview.md)。 有关隐私服务API中所有可用端点的全面列表，请参阅 [API参考](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)。

## 入门指南

本指南需要了解以下Experience Platform功能：

* [隐私服务](../home.md):提供RESTful API和用户界面，使您能够跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

以下各节提供了成功调用隐私服务API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## 后续步骤

现在，您已经了解要使用哪些标头，可以开始调用隐私服务API了。 隐私工作 [文档](privacy-jobs.md) ，将逐步介绍您可以使用隐私服务API进行的各种API调用。 每个示例调用包括常规API格式、显示所需标题的示例请求和示例响应。
