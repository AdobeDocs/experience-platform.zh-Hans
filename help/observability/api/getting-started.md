---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: 可观性洞察API入门
topic: developer guide
description: 可观性洞察API允许您针对各种Adobe Experience Platform功能检索度量数据。 本文档介绍了在尝试调用可观性洞察API之前需要了解的核心概念。
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

API [!DNL Observability Insights] 允许您检索各种Adobe Experience Platform功能的度量数据。 此文档介绍了在尝试调用API之前需要了解的核心概 [!DNL Observability Insights] 念。

## 读取示例API调用

API文 [!DNL Observability Insights] 档提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南中有关如何阅读示例API调 [用的部分](../../landing/troubleshooting.md)。

## 所需的标题

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作所在沙箱的名称。 有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用API进行调 [!DNL Observability Insights] 用，请继续阅读“度 [量端点指南”](./metrics.md)。