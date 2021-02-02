---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；api;
solution: Experience Platform
title: 分段服务开发人员指南
topic: developer guide
description: 以下文档提供了成功使用分段API所需了解的其他信息。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# [!DNL Segmentation Service] {#getting-started}入门

Adobe Experience Platform[!DNL Segmentation Service]允许您在Adobe Experience Platform建立细分，并根据[!DNL Real-time Customer Profile]数据生成受众。

开发人员指南要求对使用[!DNL Segmentation Service]时涉及的各种[!DNL Experience Platform]服务进行有效的了解。

- [[!DNL Segmentation]](../home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 细分。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功使用[!DNL Segmentation] API所需了解的其他信息。

## 读取示例API调用

[!DNL Segmentation Service] API文档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

## 所需的标题

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用[!DNL Platform]端点。 完成身份验证教程后，将为[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：`Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定将在其中执行操作的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

## 后续步骤

要使用[!DNL Segmentation Service] API进行调用，请使用左侧导航或在[开发人员指南概述](./overview.md)中选择可用的端点指南之一