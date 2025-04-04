---
keywords: Experience Platform；开发人员指南；端点；数据科学Workspace；热门主题；数据科学工作区；数据科学
solution: Experience Platform
title: Sensei机器学习API指南
description: Sensei机器学习API允许开发人员对各种数据科学Workspace资源执行CRUD操作。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 13%

---

# [!DNL Sensei Machine Learning] API指南

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

[!DNL Sensei Machine Learning] API为数据科学家提供了一种机制，可用于组织和管理机器学习服务，从算法载入到实验，再到服务部署。

本开发人员指南提供了帮助您开始使用[Sensei机器学习API](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)的步骤，并演示了对各种数据科学Workspace资源执行CRUD操作的API调用。

## 快速入门

您需要完成[身份验证](https://www.adobe.com/go/platform-api-authentication-en)教程才能访问以下请求标头以调用[!DNL Adobe Experience Platform] API：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* Content-Type： application/json

## 后续步骤

收集了所需的身份验证凭据后，您可以继续本开发人员指南的后续部分，以了解对以下端点组的示例API调用：

* [引擎](./engines.md)
* [试验](./experiments.md)
* [洞察](./insights.md)
* [MLInstances（配方）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附录](./appendix.md)
