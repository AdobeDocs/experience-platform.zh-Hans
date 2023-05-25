---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: Observability Insights API入门
description: 通过可观察性分析API，可检索各种Adobe Experience Platform功能的指标数据。 本文档介绍了在尝试调用Observability Insights API之前需要了解的核心概念。
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 入门 [!DNL Observability Insights] API

此 [!DNL Observability Insights] API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用 [!DNL Observability Insights] API。

## 正在读取示例API调用

此 [!DNL Observability Insights] API文档提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用的文档中使用的约定的信息，请参阅中有关如何读取示例API调用的章节。 [Experience Platform疑难解答指南](../../landing/troubleshooting.md).

## 必需的标头

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称。 有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 后续步骤

要开始使用 [!DNL Observability Insights] API，转到 [量度端点指南](./metrics.md).
