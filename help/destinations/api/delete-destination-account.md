---
keywords: Experience Platform；主页；热门主题；流服务；删除目标帐户；删除；API
solution: Experience Platform
title: 使用流服务API删除目标帐户
type: Tutorial
description: 了解如何使用流服务API删除目标帐户。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 21%

---

# 使用流服务API删除目标帐户

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

在激活数据之前，您需要先设置目标帐户，以连接到目标。 本教程介绍使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)删除不再需要的目标帐户的步骤。

>[!NOTE]
>
>当前仅在流服务API中支持删除目标帐户。 无法使用Experience Platform UI删除目标帐户。

## 快速入门 {#get-started}

本教程要求您具有有效的连接ID。 连接ID表示与目标的帐户连接。 如果您没有有效的连接ID，请从[目标目录](../catalog/overview.md)中选择您选择的目标，并按照[连接到目标](../ui/connect-destination.md)中列出的步骤操作，然后再尝试本教程。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations]是预先构建的与目标平台的集成，可无缝激活Adobe Experience Platform中的数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功删除目标帐户所需了解的其他信息。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform]。

### 收集所需标头的值 {#gather-values-for-required-headers}

为调用 [!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

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

## 查找要删除的目标帐户的连接ID {#find-connection-id}

>[!NOTE]
>本教程以[飞艇目标](../catalog/mobile-engagement/airship-attributes.md)为例，但列出的步骤适用于任何[可用目标](../catalog/overview.md)。

删除目标帐户的第一步是查找与要删除的目标帐户对应的连接ID。

在Experience Platform UI中，浏览到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**，并通过选择&#x200B;**[!UICONTROL Destinations]**&#x200B;列中的数字来选择要删除的帐户。

![选择要删除的目标帐户](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

接下来，您可以从浏览器的URL中检索目标帐户的连接ID。

![从URL检索连接ID](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## 删除连接 {#delete-connection}

>[!IMPORTANT]
>
>在删除目标帐户之前，必须删除指向目标帐户的任何现有数据流。
>>要删除现有数据流，请参阅以下页面：
>
>* [使用Experience Platform UI](../ui/delete-destinations.md)删除现有数据流；
>* [使用流服务API](delete-destination-dataflow.md)删除现有数据流。

在拥有连接ID并确保不存在到目标帐户的数据流后，请对[!DNL Flow Service] API执行DELETE请求。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要删除的连接唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。 您可以通过尝试向连接发送查找(GET)请求来确认删除。 API将返回HTTP 404（未找到）错误，指示目标帐户已被删除。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

通过完成本教程，您已成功使用[!DNL Flow Service] API删除现有的目标帐户。 有关使用目标的详细信息，请参阅[目标概述](/help/destinations/home.md)。