---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 实时客户用户档案API入门
topic: guide
type: Documentation
description: 用户档案API入门指南概述了使用实时客户用户档案API端点对用户档案数据执行基本CRUD操作时需要了解的主要概念和基本功能。
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API {#getting-started}快速入门

使用实时用户档案API端点，您可以针对用户档案数据执行基本的CRUD操作，如配置计算属性、访问实体、导出用户档案数据以及删除不需要的数据集或批量。

使用开发人员指南需要对使用[!DNL Profile]数据时涉及的各种Adobe Experience Platform服务进行有效的了解。 在开始使用[!DNL Real-time Customer Profile] API之前，请查阅以下服务的文档：

* [[!DNL Real-time Customer Profile]](../home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地视图客户及其行为。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):允许您根据实时受众数据构建用户档案细分。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功调用[!DNL Profile] API端点所需了解的其他信息。

## 读取示例API调用

[!DNL Real-time Customer Profile] API文档提供示例API调用，以演示如何正确设置请求格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

## 所需的标题

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用[!DNL Platform]端点。 完成身份验证教程后，将为[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的请求需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

请求主体中具有有效负荷的所有请求(如POST、PUT和PATCH调用)都必须包含`Content-Type`头。 在每个呼叫参数中提供特定于每个呼叫的已接受值。

## 后续步骤

要开始使用[!DNL Real-time Customer Profile] API进行调用，请选择可用的端点指南之一。