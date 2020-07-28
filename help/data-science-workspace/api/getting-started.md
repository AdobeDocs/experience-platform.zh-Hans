---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Sensei Machine Learning API开发人员指南
topic: Developer guide
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] API开发人员指南

API为数 [!DNL Sensei Machine Learning] 据科学家提供了组织和管理机器学习服务的机制，从算法入门到实验再到服务部署。

此开发人员指南提供了帮助您使用Sensei机器 [学习API进行开始的步骤](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，并演示了对各种数据科学工作区资源执行CRUD操作的API调用。

## 入门指南

您必须完成身份验证 [教程](../../tutorials/authentication.md) ，才能访问以下请求标头以调用API [!DNL Adobe Experience Platform] :

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

* 内容类型： application/json

## 后续步骤

收集所需的身份验证凭据后，您可以继续阅读本开发人员指南的后续部分，获取对以下端点组的示例API调用：

* [引擎](./engines.md)
* [实验](./experiments.md)
* [洞察](./insights.md)
* [MLInstances（菜谱）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附录](./appendix.md)