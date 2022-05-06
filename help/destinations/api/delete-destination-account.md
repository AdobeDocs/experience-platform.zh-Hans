---
keywords: Experience Platform；主页；热门主题；流程服务；删除目标帐户；删除；API
solution: Experience Platform
title: 使用流量服务API删除目标帐户
type: Tutorial
description: 了解如何使用流量服务API删除目标帐户。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 使用流量服务API删除目标帐户

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

在激活数据之前，您需要先设置目标帐户以连接到目标。 本教程介绍了使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>当前仅流程服务API支持删除目标帐户。 无法使用Experience PlatformUI删除目标帐户。

## 快速入门 {#get-started}

本教程要求您具有有效的连接ID。 连接ID表示与目标的帐户连接。 如果您没有有效的连接ID，请从 [目标目录](../catalog/overview.md) 并按照 [连接到目标](../ui/connect-destination.md) 在尝试本教程之前。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [目标](../home.md): [!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

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

## 查找要删除的目标帐户的连接ID {#find-connection-id}

>[!NOTE]
>本教程使用 [飞艇目的地](../catalog/mobile-engagement/airship-attributes.md) 例如，但列出的步骤适用于 [可用目标](../catalog/overview.md).

删除目标帐户的第一步是查找与要删除的目标帐户对应的连接ID。

在Experience PlatformUI中，浏览到 **[!UICONTROL 目标]** > **[!UICONTROL 帐户]** ，然后通过选择 **[!UICONTROL 目标]** 列。

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
>在删除目标帐户之前，必须删除目标帐户的任何现有数据流。
>要删除现有数据流，请参阅以下页面：
>* [使用Experience PlatformUI](../ui/delete-destinations.md) 删除现有数据流；
>* [使用流量服务API](delete-destination-dataflow.md) 删除现有数据流。


在您拥有连接ID并确保目标帐户不存在数据流后，请向执行DELETE请求 [!DNL Flow Service] API。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 独特 `id` 值。 |

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

成功响应会返回HTTP状态204（无内容）和空白正文。 您可以通过尝试对连接进行查询(GET)请求来确认删除。 API将返回HTTP 404（未找到）错误，表示目标帐户已删除。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规的Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

通过阅读本教程，您已成功使用 [!DNL Flow Service] 用于删除现有目标帐户的API。 有关使用目标的更多信息，请参阅 [目标概述](/help/destinations/home.md).