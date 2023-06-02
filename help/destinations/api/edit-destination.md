---
solution: Experience Platform
title: 使用流服务API编辑目标连接
type: Tutorial
description: 了解如何使用流服务API编辑目标连接的各种组件。
source-git-commit: 2afe330176c2b7734c38cf47be79960175060824
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 2%

---

# 使用流服务API编辑目标连接

本教程介绍了编辑目标连接的各种组件的步骤。 了解如何使用更新身份验证凭据、导出位置等 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 目前，仅通过流服务API支持本教程中描述的编辑操作。

## 快速入门 {#get-started}

本教程要求您拥有有效的数据流ID。 如果您没有有效的数据流ID，请从 [目标目录](../catalog/overview.md) 并按照概述的步骤操作 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) 在尝试本教程之前。

>[!NOTE]
>
> 条款 *流量* 和 *数据流* 在本教程中可互换使用。 在本教程的上下文中，它们具有相同的含义。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。
* [沙盒](../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 正在读取示例API调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

### 收集所需标题的值 {#gather-values-for-required-headers}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源，包括属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 对Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 未指定标头，请求将在 `prod` 沙盒。

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

编辑目标连接的第一步是使用流ID检索数据流详细信息。 您可以通过对以下地址发出GET请求，查看现有数据流的当前详细信息： `/flows` 端点。

>[!TIP]
>
>您可以使用Experience PlatformUI获取目标所需的数据流ID。 转到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]**，选择所需的目标数据流，然后在右边栏中找到目标ID。 目标ID是您将在下一步中用作流ID的值。
>
> ![使用Experience PlatformUI获取目标ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 要检索的目标数据流的值。 |

**请求**

以下请求可检索有关您的流量ID的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)，以及其他相关信息。 与本教程最相关的是下方的响应中高亮显示的目标连接ID和基本连接ID。 您将在下一节中使用这些ID来更新目标连接的各个组件。

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## 编辑目标连接组件（存储位置和其他组件） {#patch-target-connection}

目标连接的组件因目标而异。 例如，对于 [!DNL Amazon S3] 目标，您可以更新导出文件的存储段和路径。 对象 [!DNL Pinterest] 目标，您可以更新 [!DNL Pinterest Advertiser ID] 和 [!DNL Google Customer Match] 您可以更新 [!DNL Pinterest Account ID].

PATCH要更新目标连接的组件，请对 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，同时提供您的目标连接ID、版本以及要使用的新值。 请记住，在上一步中，当您检查到所需目标的现有数据流时，您获得了目标连接ID。

>[!IMPORTANT]
>
>此 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的目标连接的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> GET要获取最新版本的etag值，请对 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，其中 `{TARGET_CONNECTION_ID}` 是要更新的目标连接ID。

下面是一些示例，用于更新不同类型目标的目标连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取目标连接ID >使用所需参数的更新值PATCH目标连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求将更新 `bucketName` 和 `path` 参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的Etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google广告管理器和Google广告管理器360]

**请求**

以下请求更新参数 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目标](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 连接以添加新的 [**[!UICONTROL 将区段ID附加到区段名称]**](/help/release-notes/2023/april-2023.md#destinations) 字段。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**请求**

以下请求将更新 `advertiserId` 参数 [[!DNL Pinterest] 目标连接](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 编辑基本连接组件（身份验证参数和其他组件） {#patch-base-connection}

要更新目标的凭据时编辑基本连接。 基本连接的组件因目标而异。 例如，对于 [!DNL Amazon S3] 目标，您可以将访问密钥和密钥更新为 [!DNL Amazon S3] 位置。

PATCH要更新基本连接的组件，请对 `/connections` 端点，同时提供基本连接ID、版本以及要使用的新值。

请记住，您的基本连接ID位于 [上一步](#look-up-dataflow-details)，检查到参数所需目标的现有数据流时 `baseConnection`.

>[!IMPORTANT]
>
>此 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的基础连接的唯一版本。 每次成功更新流实体（例如数据流、基本连接等）时，etag值都会更新。
>
> GET要获取最新版本的Etag值，请对 `/connections/{BASE_CONNECTION_ID}` 端点，其中 `{BASE_CONNECTION_ID}` 是要更新的基本连接ID。

下面是一些示例，用于为不同类型的目标更新基本连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取基本连接ID >使用所需参数的更新值PATCH基本连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求将更新 `accessId` 和 `secretKey` 参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**请求**

以下请求更新 [[!DNL Azure Blob] 目标](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 连接，以更新连接到Azure Blob实例所需的连接字符串。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 您希望使用更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的etag。 您可以通过向以下用户发出GET请求来验证更新： [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) 有关解释错误响应的更多信息，请参阅Platform疑难解答指南。

## 后续步骤 {#next-steps}

通过阅读本教程，您已了解如何使用 [!DNL Flow Service] API。 有关目标的更多信息，请参见 [目标概述](../home.md).
