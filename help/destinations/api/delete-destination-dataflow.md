---
keywords: Experience Platform；主页；热门主题；流服务；API；API；删除；删除目标数据流
solution: Experience Platform
title: 使用流服务API删除目标数据流
type: Tutorial
description: 了解如何使用流服务API将数据流删除到批处理目标和流式目标。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 使用流服务API删除目标数据流

您可以使用删除包含错误或已过时的数据流 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教程介绍了使用将数据流同时删除到批处理目标和流式目标 [!DNL Flow Service].

## 快速入门 {#get-started}

本教程要求您拥有有效的流ID。 如果您没有有效的流ID，请从 [目标目录](../catalog/overview.md) 并按照概述的步骤操作 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) 在尝试本教程之前。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了使用，成功删除数据流时需要了解的其他信息 [!DNL Flow Service] API。

### 正在读取示例API调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值 {#gather-values-for-required-headers}

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 未指定标头，请求将在 `prod` 沙盒。

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 删除目标数据流 {#delete-destination-dataflow}

对于现有的流ID，您可以通过向以下对象执行DELETE请求来删除目标数据流： [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 要删除的目标数据流的值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态202（无内容）和一个空白正文。 您可以通过尝试向数据流查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，指示数据流已被删除。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) 有关解释错误响应的更多信息，请参阅Platform疑难解答指南。

## 后续步骤 {#next-steps}

按照本教程中的说明，您已成功使用了 [!DNL Flow Service] 用于删除到目标的现有数据流的API。

有关如何使用用户界面执行这些操作的步骤，请参阅关于的教程 [在UI中删除数据流](../ui/delete-destinations.md).

您现在可以继续 [删除目标帐户](/help/destinations/api/delete-destination-account.md) 使用 [!DNL Flow Service] API。
