---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 自助源入门（批量SDK）
topic-legacy: developer guide
description: 本文档简要介绍在尝试使用自助源（批处理SDK）创建新源之前您需要了解的先决条件信息。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 自助源入门（批量SDK）

自助源（批量SDK）允许您集成自己的基于REST的源，以将批量数据导入Adobe Experience Platform。 本文档简要介绍在尝试调用 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 先决条件

要使用自助源（批量SDK），您必须确保有权访问已使用Adobe Experience Platform源进行设置的IMS组织沙盒。

本指南还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 读取示例API调用

自助源（批处理SDK）和 [!DNL Flow Service] API文档提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

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

要开始使用自助源（批处理SDK）创建新源，请参阅 [创建新源](./create.md).
