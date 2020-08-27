---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API入门
topic: guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# API入 [!DNL Real-time Customer Profile] 门 {#getting-started}

使用 [!DNL Real-time Customer Profile] API，您可以针对用户档案资源执行基本的CRUD操作，如配置计算属性、访问实体、导出用户档案数据以及删除不需要的数据集或批量。

使用开发人员指南需要对使用数据时涉及的各种Adobe Experience Platform服务进行有效 [!DNL Profile] 了解。 在开始使用API之 [!DNL Real-time Customer Profile] 前，请查阅以下服务的文档：

* [[!DNL实时客户用户档案]](../home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNLAdobe Experience Platform身份服务]](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地视图客户及其行为。
* [[!DNLAdobe Experience Platform分段服务]](../../segmentation/home.md):允许您根据实时受众数据构建用户档案细分。
* [[!DNL体验数据模型(XDM)]](../../xdm/home.md):平台组织客户体验数据的标准化框架。
* [[!DNL沙箱]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功调用API端点所需了解的其 [!DNL Profile] 他信息。

## 读取示例API调用

API文 [!DNL Real-time Customer Profile] 档提供示例API调用，以演示如何正确设置请求格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

## 所需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用端点 [!DNL Platform] 。 完成身份验证教程可为API调用中每个所需标头 [!DNL Experience Platform] 提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API [!DNL Platform] 的请求需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

请求主体中具有有效负荷的所有请求(如POST、PUT和PATCH调用)都必须包含 `Content-Type` 标头。 在每个呼叫参数中提供特定于每个呼叫的已接受值。

## 后续步骤

要开始使用API进行调 [!DNL Real-time Customer Profile] 用，请选择可用的端点指南之一。