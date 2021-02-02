---
keywords: Experience Platform；主页；热门主题；流服务；API;api；删除；删除数据流
solution: Experience Platform
title: 使用Flow Service API删除数据流
topic: overview
type: Tutorial
description: 本教程介绍使用Flow Service API删除批处理和流数据流的步骤。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# 使用Flow Service API删除数据流

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)删除包含错误或已过时的批处理和流数据流。

本教程介绍使用[!DNL Flow Service]删除使用批处理源和流式源创建的数据流的步骤。

## 入门指南

本教程要求您具有有效的流ID。 如果您没有有效的流ID，请从[源概述](../../home.md)中选择您选择的连接器，然后按照概述的步骤操作，再尝试本教程。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功删除数据流时需要了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 删除数据流

使用现有流ID，可以通过对[!DNL Flow Service] API执行DELETE请求来删除数据流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要删除的数据流的唯一`id`值。 |

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

通过遵循本教程，您已成功使用[!DNL Flow Service] API删除现有数据流。

有关如何使用用户界面执行这些操作的步骤，请参阅有关在UI](../../tutorials/ui/delete.md)中删除数据流的教程。[
