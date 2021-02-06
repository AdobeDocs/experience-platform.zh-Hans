---
keywords: Experience Platform；开发人员指南；端点；数据科学工作区；热门主题；数据科学工作区；数据科学
solution: Experience Platform
title: Sensei机器学习API指南
topic: Developer guide
description: Sensei机器学习API允许开发人员对各种数据科学工作区资源执行CRUD操作。 请按照本指南学习如何使用API执行关键操作。
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] API指南

[!DNL Sensei Machine Learning] API为数据科学家提供了组织和管理机器学习服务的机制，从算法入门到实验再到服务部署。

此开发人员指南提供了帮助您使用[Sensei机器学习API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)进行开始的步骤，并演示了对各种数据科学工作区资源执行CRUD操作的API调用。

## 入门指南

您必须已完成[authentication](https://www.adobe.com/go/platform-api-authentication-en)教程，才能访问以下请求标头以调用[!DNL Adobe Experience Platform] API:

* 授权：载体`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name:`{SANDBOX_NAME}`

有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

* 内容类型：application/json

## 后续步骤

收集所需的身份验证凭据后，您可以继续阅读本开发人员指南的后续部分，获取对以下端点组的示例API调用：

* [引擎](./engines.md)
* [实验](./experiments.md)
* [洞察](./insights.md)
* [MLInstances（菜谱）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附录](./appendix.md)