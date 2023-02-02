---
title: 自助源（流SDK）入门
description: 本文档简要介绍在尝试使用自助源（流SDK）创建新源之前您需要了解的先决条件信息。
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 自助源（流SDK）入门

自助源（流SDK）允许您集成自己的源以将流数据引入Adobe Experience Platform。 本文档简要介绍在尝试调用 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 高级流程

在Experience Platform中配置源的分步流程如下所示：

### 集成

* [为流SDK创建新的连接规范](create.md).
* [使用新的连接规范ID更新流流规范](update-flow-specs.md).
* [测试并提交流源](submit.md).

### 文档

* 要开始记录源，请阅读 [自助源创建文档概述](../documentation/doc-overview.md).
* 阅读 [使用GitHub Web界面](../documentation/github.md) 有关如何使用GitHub创建文档的步骤。
* 阅读 [使用文本编辑器](../documentation/text-editor.md) 有关如何使用本地计算机创建文档的步骤。
* [使用流SDK API文档模板在API中记录您的源](streaming-template-api.md).
* [使用流SDK UI文档模板在UI中记录您的源](streaming-template-ui.md).

您还可以下载以下文档模板：

* [API文档模板](../assets/streaming/streaming-template-api.zip)
* [UI文档模板](../assets/streaming/streaming-template-ui.zip)

## 先决条件

>[!IMPORTANT]
>
>要与Experience Platform集成的源必须能够支持端点可订阅的WebHook以发送更新。

要使用自助源（流SDK），您必须确保有权访问已配置Adobe Experience Platform源的沙盒组织。

本指南还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 读取示例API调用

自助源（流SDK）和 [!DNL Flow Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

## 收集所需标题的值

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

平台中的所有资源，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙箱的更多信息，请参阅 [沙盒文档](../../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

要开始使用自助源（流SDK）创建新源，请参阅 [创建新源](./create.md).
