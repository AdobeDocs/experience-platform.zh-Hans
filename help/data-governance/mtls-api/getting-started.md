---
title: MTLS服务API快速入门
description: 本文档提供了成功使用MTLS API所需了解的其他信息。
role: Developer
exl-id: db5978cf-fe47-4b76-86ba-c8ea1ee6b12f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 6%

---

# MTLS服务API快速入门 {#getting-started}

MTLS服务API允许您安全检索和验证Adobe颁发的公共证书。

以下部分提供成功使用MTLS服务API所需了解的其他信息。

## 正在读取示例 API 调用

MTLS服务API文档提供了一个示例API调用，用于演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求有效负载。 还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 必需的标头

API文档还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用Experience Platform端点。 完成身份验证教程将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

## 后续步骤

要使用MTLS服务API进行调用，请使用左侧导航或[开发人员指南概述](./overview.md)中选择端点指南
