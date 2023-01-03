---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 实时客户资料API快速入门
topic-legacy: guide
type: Documentation
description: 配置文件API快速入门指南概述了要使用实时客户配置文件API端点对配置文件数据执行基本CRUD操作所需了解的关键概念和基本功能。
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 入门 [!DNL Real-Time Customer Profile] API {#getting-started}

使用实时客户配置文件API端点，您可以对配置文件数据执行基本的CRUD操作，例如配置计算属性、访问实体、导出配置文件数据，以及删除不需要的数据集或批量。

使用开发人员指南需要对与 [!DNL Profile] 数据。 开始使用之前 [!DNL Real-Time Customer Profile] API，请查阅以下服务的文档：

* [[!DNL Real-Time Customer Profile]](../home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地了解客户及其行为。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):允许您根据实时客户资料数据构建受众区段。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用所需了解的其他信息 [!DNL Profile] API端点。

## 读取示例API调用

的 [!DNL Real-Time Customer Profile] API文档提供了示例API调用，以演示如何正确设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需标题

API文档还要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将提供 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 请求 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

请求正文中具有有效负载的所有请求(例如POST、PUT和PATCH调用)都必须包含 `Content-Type` 标题。 调用参数中提供了特定于每个调用的已接受值。

## 后续步骤

要开始使用 [!DNL Real-Time Customer Profile] API，请选择一个可用的端点指南。
