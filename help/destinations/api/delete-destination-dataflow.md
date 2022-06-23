---
keywords: Experience Platform；主页；热门主题；流程服务；API;API；删除；删除目标数据流
solution: Experience Platform
title: 使用流服务API删除目标数据流
type: Tutorial
description: 了解如何使用流服务API将数据流删除到批处理目标和流目标。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 使用流服务API删除目标数据流

您可以删除包含错误或已在使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教程介绍了使用 [!DNL Flow Service].

## 快速入门 {#get-started}

本教程要求您拥有有效的流程ID。 如果您没有有效的流量ID，请从 [目标目录](../catalog/overview.md) 并按照 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) 在尝试本教程之前。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [目标](../home.md): [!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下各节提供了要使用 [!DNL Flow Service] API。

### 读取示例API调用 {#reading-sample-api-calls}

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值 {#gather-values-for-required-headers}

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 标头未指定，请求将在 `prod` 沙盒。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 删除目标数据流 {#delete-destination-dataflow}

使用现有的流ID，您可以通过向执行DELETE请求来删除目标数据流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 独特 `id` 要删除的目标数据流的值。 |

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

成功的响应会返回HTTP状态202（无内容）和空白正文。 您可以通过尝试对数据流进行查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，表示数据流已被删除。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规的Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) ，以了解有关解释错误响应的更多信息。

## 后续步骤 {#next-steps}

通过阅读本教程，您已成功使用 [!DNL Flow Service] 用于将现有数据流删除到目标的API。

有关如何使用用户界面执行这些操作的步骤，请参阅 [删除UI中的数据流](../ui/delete-destinations.md).

你现在可以继续 [删除目标帐户](/help/destinations/api/delete-destination-account.md) 使用 [!DNL Flow Service] API。
