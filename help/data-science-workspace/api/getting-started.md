---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Sensei Machine Learning API开发人员指南
topic: Developer guide
translation-type: tm+mt
source-git-commit: 9e12c8087524f692a123b3389df4fdc324c4238d

---


# Sensei Machine Learning API开发人员指南

Sensei机器学习API为数据科学家提供了组织和管理机器学习服务的机制，从算法入门到实验，再到服务部署。

此开发人员指南提供了帮助您使用 [Sensei机器学习API进行开始的步骤](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，并演示了对各种数据科学工作区资源执行CRUD操作的API调用。

## 入门指南

您必须已完成身份验证教 [程](../../tutorials/authentication.md) ，才能访问以下请求标头以调用Adobe Experience Platform API:

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## 后续步骤

收集所需的身份验证凭据后，您可以继续阅读本开发人员指南的后续部分，获取对以下端点组的示例API调用：

* [引擎](engines.md)
* [实验](experiments.md)
* [洞察](insights.md)
* [MLInstances（方法）](mlinstances.md)
* [MLServices](mlservices.md)
* [模型](models.md)
* [附录](appendix.md)