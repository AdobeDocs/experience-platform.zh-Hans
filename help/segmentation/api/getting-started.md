---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；api;
solution: Experience Platform
title: 分段服务API快速入门
topic-legacy: developer guide
description: 以下文档提供了您需要了解的其他信息，以便成功使用分段API。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 分段服务API {#getting-started}快速入门

Adobe Experience Platform [!DNL Segmentation Service]允许您在Adobe Experience Platform中根据[!DNL Real-time Customer Profile]数据生成区段和受众。

开发人员指南要求对与使用[!DNL Segmentation Service]相关的各种[!DNL Experience Platform]服务有良好的了解。

- [[!DNL Segmentation]](../home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 区段。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功使用[!DNL Segmentation] API所需了解的其他信息。

## 读取示例API调用

[!DNL Segmentation Service] API文档提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

## 所需的标题

API文档还要求您已完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以便成功调用[!DNL Platform]端点。 完成身份验证教程后，将为[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定将在其中执行操作的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

## 后续步骤

要使用[!DNL Segmentation Service] API进行调用，请使用左侧导航或在[开发人员指南概述](./overview.md)中选择可用的端点指南之一
