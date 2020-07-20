---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分段服务开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform细分服务允许您根据数据构建细分并在Adobe Experience Platform中生成 [!DNL Real-time Customer Profile] 受众。

开发人员指南要求对与使用相关的各种Experience Platform服务进行有效的了解 [!DNL Segmentation Service]。

- [!DNL Segmentation](../home.md): 允许您根据实时受众数据构建用户档案细分。
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
- [!DNL Real-time Customer Profile](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了成功使用API所需了解的其他信 [!DNL Segmentation] 息。

## 读取示例API调用

API文 [!DNL Segmentation Service] 档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

## 所需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用平台端点。 完成身份验证教程后，将为Experience PlatformAPI调用中每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定要在其中执行操作的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在中使用沙箱的更多信 [!DNL Experience Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 后续步骤

要使用API进行调 [!DNL Segmentation Service] 用，请使用左侧导航或在开发人员指南概述中选择一个可 [用端点指南](./overview.md)