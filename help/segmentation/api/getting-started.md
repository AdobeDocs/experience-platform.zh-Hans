---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；API；
solution: Experience Platform
title: 分段服务API快速入门
description: 以下文档提供了成功使用分段API所需了解的其他信息。
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# 分段服务API快速入门 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 允许您通过Adobe Experience Platform中的区段定义或其他来源从以下位置创建受众： [!DNL Real-Time Customer Profile] 数据。

开发人员指南需要对各种 [!DNL Experience Platform] 使用涉及的服务 [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从构建受众 [!DNL Real-Time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被作为配置文件和事件摄取，并根据 [数据建模的最佳实践](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功使用 [!DNL Segmentation] API。

## 正在读取示例 API 调用

此 [!DNL Segmentation Service] API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需的标头

此API文档还要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将为中的每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 被隔离到特定的虚拟沙盒中。 所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在中使用沙箱的详细信息 [!DNL Experience Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

## 后续步骤

使用进行调用 [!DNL Segmentation Service] API中，使用左侧导航或在 [开发人员指南概述](./overview.md)
