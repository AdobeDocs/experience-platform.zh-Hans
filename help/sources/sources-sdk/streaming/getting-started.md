---
title: 自助式源快速入门(Streaming SDK)
description: 本文档介绍了在尝试使用自助源(Streaming SDK)创建新源之前需要了解的先决条件信息。
hide: true
hidefromtoc: true
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 自助式源快速入门(Streaming SDK)

自助式源（流SDK）允许您集成自己的源，以将流数据引入到Adobe Experience Platform。 本文档介绍了在尝试调用 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 高级流程

下面概述了在Experience Platform中配置源的分步流程：

### 集成

* [为流SDK创建新的连接规范](create.md).
* [使用新的连接规范ID更新流规范](update-flow-specs.md).
* [测试和提交您的流源](submit.md).

### 文档

* 要开始记录您的源，请阅读 [关于创建自助式源文档的概述](../documentation/doc-overview.md).
* 阅读以下内容中的指南： [使用GitHub Web界面](../documentation/github.md) 有关如何使用GitHub创建文档的步骤。
* 阅读以下内容中的指南： [使用文本编辑器](../documentation/text-editor.md) 有关如何使用本地计算机创建文档的步骤。
* [使用流SDK API文档模板在API中记录您的源](streaming-template-api.md).
* [使用流SDK UI文档模板在UI中记录源](streaming-template-ui.md).

您还可以下载以下文档模板：

* [API文档模板](../assets/streaming/streaming-template-api.zip)
* [UI文档模板](../assets/streaming/streaming-template-ui.zip)

## 先决条件

>[!IMPORTANT]
>
>要发送更新，您与Experience Platform集成的源必须能够支持端点可以订阅的webhook。

要使用自助源（流SDK），您必须确保您有权访问配置了Adobe Experience Platform源的沙盒组织。

本指南还需要深入了解Adobe Experience Platform的以下组件：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 正在读取示例API调用

自助服务源(Streaming SDK)和 [!DNL Flow Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

## 收集所需标题的值

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Platform中的所有资源，包括属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 对Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙盒的更多信息，请参阅 [沙盒文档](../../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 后续步骤

要开始使用自助源（流SDK）创建新源，请参阅关于的教程 [创建新源](./create.md).
