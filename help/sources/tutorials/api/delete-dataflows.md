---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: 使用Flow Service API删除数据流
topic: overview
type: Tutorial
description: 本教程介绍使用流服务API删除数据流的步骤。
translation-type: tm+mt
source-git-commit: ae3e64a5f9a82c0efe3cffeb6d4d425ae2e72bda
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# 使用Flow Service API删除数据流

本教程介绍使用删除批处理源和流式源创建的数据流的步骤 [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。

## 入门指南

本教程要求您具有有效的流ID。 如果您没有有效的流ID，请从源概述中选择您选择的连接 [器](../../home.md) ，并按照概述的步骤操作，然后尝试本教程。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用API成功删除数据流时需要了解的其他 [!DNL Flow Service] 信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 删除数据流

使用现有流ID，您可以通过对API执行DELETE请求来删除数据 [!DNL Flow Service] 流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要删 `id` 除的数据流的唯一值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。 您可以通过尝试对GET流进行查找（数据）请求来确认删除。 API将返回HTTP 404（未找到）错误，表示已删除数据流。

## 后续步骤

通过遵循本教程，您已成功使 [!DNL Flow Service] 用API删除现有数据流。

有关如何使用用户界面执行这些操作的步骤，请参阅有关在UI中删 [除数据流的教程](../../tutorials/ui/delete.md)
