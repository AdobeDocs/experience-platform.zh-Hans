---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: Observability Insights API入门
description: 通过可观察性洞察API，可检索各种Adobe Experience Platform功能的指标数据。 本文档介绍了在尝试调用Observability Insights API之前需要了解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---

# [!DNL Observability Insights] API快速入门

[!DNL Observability Insights] API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用[!DNL Observability Insights] API之前需要了解的核心概念。

## 正在读取示例 API 调用

[!DNL Observability Insights] API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[Experience Platform疑难解答指南](../../landing/troubleshooting.md)中有关如何读取示例API调用的部分。

## 必需的标头

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称。 有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用[!DNL Observability Insights] API进行调用，请转到[量度终结点指南](./metrics.md)。
