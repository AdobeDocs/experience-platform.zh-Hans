---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: 分段服务API快速入门
topic-legacy: developer guide
description: 以下文档提供了要成功使用分段API需要了解的其他信息。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 分段服务API快速入门 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 允许您在Adobe Experience Platform中通过 [!DNL Real-time Customer Profile] 数据。

开发人员指南需要对 [!DNL Experience Platform] 使用涉及的服务 [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Allows you to build audience segments from [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Provides a unified, real-time consumer profile based on aggregated data from multiple sources.
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Reading sample API calls

的 [!DNL Segmentation Service] API文档提供了示例API调用，以演示如何设置请求的格式。 These include paths, required headers, and properly formatted request payloads. 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 必需标题

API文档还要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] 端点。 完成身份验证教程将提供 [!DNL Experience Platform] API调用，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## 后续步骤

要使用 [!DNL Segmentation Service] API中，使用左侧导航或在 [开发人员指南概述](./overview.md)
