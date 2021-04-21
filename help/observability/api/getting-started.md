---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: 可观察性洞察API入门
topic-legacy: developer guide
description: 可观察性洞察API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用可观性分析API之前需要了解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!DNL Observability Insights] API入门

[!DNL Observability Insights] API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用[!DNL Observability Insights] API之前需要了解的核心概念。

## 读取示例API调用

[!DNL Observability Insights] API文档提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅[Experience Platform疑难解答指南](../../landing/troubleshooting.md)中有关如何读取示例API调用的部分。

## 所需的标题

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作所在沙箱的名称。 有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用[!DNL Observability Insights] API进行调用，请继续访问[ metrics endpoint guide](./metrics.md)。
