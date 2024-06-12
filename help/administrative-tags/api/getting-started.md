---
solution: Experience Platform
title: 统一标记API快速入门
description: 以下文档提供了成功使用统一标记API所需了解的其他信息。
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# 统一标记API快速入门 {#getting-started}

统一标记API允许您在Adobe Experience Platform中对业务对象进行分类和管理。

以下部分提供了成功使用统一标记API需要了解的其他信息。

## 正在读取示例 API 调用

统一标记API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

## 必需的标头

此API文档还要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功调用Platform端点。 完成身份验证教程将提供Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 被隔离到特定的虚拟沙盒中。 所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在中使用沙箱的详细信息 [!DNL Experience Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

## 后续步骤

要使用统一标记API进行调用，请使用左侧导航或在 [开发人员指南概述](./overview.md)
