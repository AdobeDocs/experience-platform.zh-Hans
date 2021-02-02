---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: 可观性洞察API入门
topic: developer guide
description: 可观性洞察API允许您针对各种Adobe Experience Platform功能检索度量数据。 本文档介绍了在尝试调用可观性洞察API之前需要了解的核心概念。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# [!DNL Observability Insights] API入门

[!DNL Observability Insights] API允许您检索各种Adobe Experience Platform功能的度量数据。 本文档介绍了在尝试调用[!DNL Observability Insights] API之前需要了解的核心概念。

## 读取示例API调用

[!DNL Observability Insights] API文档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参见[Experience Platform疑难解答指南](../../landing/troubleshooting.md)中有关如何读取示例API调用的章节。

## 所需的标题

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在其中进行的沙箱的名称。 有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用[!DNL Observability Insights] API进行调用，请继续执行[ metrics端点指南](./metrics.md)。