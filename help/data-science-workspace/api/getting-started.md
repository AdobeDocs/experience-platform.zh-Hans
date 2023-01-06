---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；数据科学工作区；数据科学
solution: Experience Platform
title: Sensei机器学习API指南
description: Sensei机器学习API允许开发人员对各种数据科学工作区资源执行CRUD操作。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] API指南

的 [!DNL Sensei Machine Learning] API为数据科学家提供了一种机制来组织和管理机器学习服务，从算法入门到实验，再到服务部署。

本开发人员指南提供了帮助您开始使用 [Sensei机器学习API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，并演示了对各种数据科学工作区资源执行CRUD操作的API调用。

## 快速入门

您需要完成 [身份验证](https://www.adobe.com/go/platform-api-authentication-en) 教程，以便能够访问以下请求标头以调用 [!DNL Adobe Experience Platform] API:

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 后续步骤

收集所需的身份验证凭据后，您可以继续阅读本开发人员指南的后续部分，以了解对以下端点组的API调用示例：

* [引擎](./engines.md)
* [实验](./experiments.md)
* [见解](./insights.md)
* [MLInstances（脚本）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附录](./appendix.md)
