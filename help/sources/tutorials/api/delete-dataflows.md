---
keywords: Experience Platform；主页；热门主题；流程服务；API;API；删除；删除数据流
solution: Experience Platform
title: 使用流服务API删除数据流
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API删除批处理数据流和流数据流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用流服务API删除数据流

您可以使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)删除包含错误或已过时的批处理数据流和流数据流。

本教程介绍了使用[!DNL Flow Service]删除使用批处理源和流源生成的数据流的步骤。

## 快速入门

本教程要求您拥有有效的流程ID。 如果您没有有效的流ID，请从[源概述](../../home.md)中选择您选择的连接器，然后按照列出的步骤操作，然后再尝试本教程。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功删除数据流所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 删除数据流

使用现有的流ID，可以通过向[!DNL Flow Service] API执行DELETE请求来删除数据流。

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

成功响应会返回HTTP状态204（无内容）和空白正文。 您可以通过尝试对数据流进行查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，表示数据流已被删除。

## 后续步骤

在本教程中，您已成功使用[!DNL Flow Service] API删除现有数据流。

有关如何使用用户界面执行这些操作的步骤，请参阅关于[删除UI](../../tutorials/ui/delete.md)中数据流的教程
