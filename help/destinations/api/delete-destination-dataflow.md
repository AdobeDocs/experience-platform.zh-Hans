---
keywords: Experience Platform；主页；热门主题；流服务；API；API；删除；删除目标数据流
solution: Experience Platform
title: 使用流服务API删除目标数据流
type: Tutorial
description: 了解如何使用流服务API将数据流删除到批处理目标和流式目标。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 14%

---

# 使用流服务API删除目标数据流

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)删除包含错误或已过时的数据流。

本教程介绍使用[!DNL Flow Service]将数据流同时删除到批处理目标和流式目标的步骤。

## 快速入门 {#get-started}

本教程要求您拥有有效的流ID。 如果您没有有效的流ID，请从[目标目录](../catalog/overview.md)中选择您选择的目标，然后按照列出的步骤[连接到目标](../ui/connect-destination.md)和[激活数据](../ui/activation-overview.md)，然后再尝试本教程。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations]是预先构建的与目标平台的集成，可无缝激活Adobe Experience Platform中的数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功删除数据流时需要了解的其他信息。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值 {#gather-values-for-required-headers}

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`标头，则在`prod`沙盒下解析请求。

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

* `Content-Type: application/json`

## 删除目标数据流 {#delete-destination-dataflow}

使用现有的流ID，您可以通过对[!DNL Flow Service] API执行DELETE请求来删除目标数据流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要删除的目标数据流的唯一`id`值。 |

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

成功的响应返回HTTP状态202（无内容）和一个空白正文。 您可以通过尝试向数据流发送查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，指示数据流已被删除。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience Platform API错误消息原则。 有关解释错误响应的详细信息，请参阅Experience Platform疑难解答指南中的[API状态代码](/help/landing/troubleshooting.md#api-status-codes)和[请求标头错误](/help/landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

通过完成本教程，您已成功使用[!DNL Flow Service] API删除到目标的现有数据流。

有关如何使用用户界面执行这些操作的步骤，请参阅有关[在UI中删除数据流](../ui/delete-destinations.md)的教程。

您现在可以使用[!DNL Flow Service] API继续并[删除目标帐户](/help/destinations/api/delete-destination-account.md)。
