---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API；
solution: Experience Platform
title: 分段服务API快速入门
description: 以下文档提供了成功使用分段API所需了解的其他信息。
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# 分段服务API快速入门 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service]允许您通过Adobe Experience Platform中的区段定义或其他源，从[!DNL Real-Time Customer Profile]数据创建受众。

开发人员指南要求实际了解与使用[!DNL Segmentation Service]有关的各种[!DNL Experience Platform]服务。

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从[!DNL Real-Time Customer Profile]数据构建受众。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。 为了更好地利用分段，请确保根据用于数据建模的[最佳实践](../../xdm/schema/best-practices.md)，将您的数据作为配置文件和事件摄取。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供成功使用[!DNL Segmentation] API所需了解的其他信息。

## 正在读取示例 API 调用

[!DNL Segmentation Service] API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform]端点。 完成身份验证教程将提供[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 后续步骤

要使用[!DNL Segmentation Service] API进行调用，请使用左侧导航或[开发人员指南概述](./overview.md)中选择可用的端点指南之一
