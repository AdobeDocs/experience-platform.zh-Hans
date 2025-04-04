---
solution: Experience Platform
title: 统一标记API快速入门
description: 以下文档提供了成功使用统一标记API所需了解的其他信息。
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 9%

---

# 统一标记API快速入门 {#getting-started}

统一标记API允许您在Adobe Experience Platform中对业务对象进行分类和管理。

以下部分提供了成功使用统一标记API需要了解的其他信息。

## 正在读取示例 API 调用

统一标记API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用Experience Platform端点。 完成身份验证教程将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 后续步骤

要使用统一标记API进行调用，请使用左侧导航或[开发人员指南概述](./overview.md)中选择可用的端点指南之一
