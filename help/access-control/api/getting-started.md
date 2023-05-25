---
keywords: Experience Platform；主页；热门主题；访问控制；API；入门
solution: Experience Platform
title: Access Control API指南
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种平台功能的角色和权限。 以下部分提供了开发人员成功调用Schema Registry API时需要了解的其他信息。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control] 对象 [!DNL Experience Platform] 是透过下列方式管理： [Adobe Admin Console](https://adminconsole.adobe.com). 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒相关联。 请参阅 [访问控制概述](../home.md) 了解更多信息。

本开发人员指南提供了有关如何将请求格式化的信息， [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)，并涵盖以下操作：

- [权限和资源类型的列表名称](./permissions-and-resource-types.md)
- [查看当前用户的有效访问策略](./effective-policies.md)

## 快速入门

以下部分提供了成功调用 [!DNL Access Control] API。

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

## 后续步骤

现在您已经收集了所需的凭据，接下来可以继续阅读开发人员指南的其余部分。 每个部分都提供了有关其端点的重要信息，并演示了用于执行CRUD操作的示例API调用。 每个调用都包含常规API格式、一个示例请求（显示所需的标头和格式正确的负载），以及一个成功调用的示例响应。
