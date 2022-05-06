---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: 可观察性分析API快速入门
topic-legacy: developer guide
description: 可观察性分析API允许您为各种Adobe Experience Platform功能检索量度数据。 本文档简要介绍在尝试调用可观察性分析API之前您需要了解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 入门 [!DNL Observability Insights] API

的 [!DNL Observability Insights] API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档简要介绍在尝试调用 [!DNL Observability Insights] API。

## 读取示例API调用

的 [!DNL Observability Insights] API文档提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅 [Experience Platform疑难解答指南](../../landing/troubleshooting.md).

## 必需标题

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中进行的沙盒的名称。 有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用 [!DNL Observability Insights] API，继续 [metrics endpoint指南](./metrics.md).
