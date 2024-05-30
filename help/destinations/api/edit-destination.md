---
solution: Experience Platform
title: 使用流服务API编辑目标连接
type: Tutorial
description: 了解如何使用流服务API编辑目标连接的各种组件。
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 4%

---

# 使用流服务API编辑目标连接

本教程涵盖了编辑目标连接的各种组件的步骤。 了解如何使用更新身份验证凭据、导出位置等 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 本教程中描述的编辑操作当前仅通过流服务API受支持。

## 快速入门 {#get-started}

本教程要求您拥有有效的数据流ID。 如果您没有有效的数据流ID，请从 [目标目录](../catalog/overview.md) 并遵循概述的步骤 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) ，然后再尝试本教程。

>[!NOTE]
>
> 术语 *流量* 和 *数据流* 在本教程中可互换使用。 在本教程的上下文中，它们具有相同的含义。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations] 是预先构建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。
* [沙盒](../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供在使用成功更新数据流时需要了解的其他信息 [!DNL Flow Service] API。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

### 收集所需标头的值 {#gather-values-for-required-headers}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源，包括属于 [!DNL Flow Service]隔离到特定的虚拟沙盒。 所有对Platform API的请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 未指定标头，请求解析在 `prod` 沙盒。

包含有效负载的所有请求(`POST`， `PUT`， `PATCH`)需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

编辑目标连接的第一步是使用流ID检索数据流详细信息。 您可以通过对以下对象发出GET请求，查看现有数据流的当前详细信息： `/flows` 端点。

>[!TIP]
>
>您可以使用Experience PlatformUI获取目标所需的数据流ID。 转到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]**，选择所需的目标数据流并在右边栏中找到目标ID。 目标ID是您将在下一步中用作流ID的值。
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

成功响应将返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)，以及其他相关信息。 与本教程最相关的内容是下面的响应中高亮显示的目标连接ID和基本连接ID。 您将在下一节中使用这些ID来更新目标连接的各种组件。

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

要更新目标连接的组件，请执行 `PATCH` 请求 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，同时提供目标连接ID、版本以及要使用的新值。 请记住，在上一步中，当您检查到所需目标的现有数据流时，您获得了目标连接ID。

>[!IMPORTANT]
>
>此 `If-Match` 进行以下操作时需要标题： `PATCH` 请求。 此标头的值是要更新的目标连接的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> GET要获取最新版本的etag值，请对 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，其中 `{TARGET_CONNECTION_ID}` 是要更新的目标连接ID。
>
> 确保将 `If-Match` 标题加双引号，如下面的示例所示 `PATCH` 请求。

以下是一些示例，说明如何更新不同类型目标的目标连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取目标连接ID > `PATCH` 具有所需参数的更新值的目标连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求将更新 `bucketName` 和 `path` 的参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的Etag。 您可以通过向以下网站发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google广告管理器和Google广告管理器360]

**请求**

以下请求更新参数 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目标](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 连接以添加新的 [**[!UICONTROL 将受众ID附加到受众名称]**](/help/release-notes/2023/april-2023.md#destinations) 字段。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的电子标记。 您可以通过向以下网站发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB pinterest]

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的电子标记。 您可以通过向以下网站发出GET请求来验证更新： [!DNL Flow Service] API，同时提供您的目标连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 编辑基本连接组件（身份验证参数和其他组件） {#patch-base-connection}

在要更新目标的凭据时编辑基本连接。 基本连接的组件因目标而异。 例如，对于 [!DNL Amazon S3] 目标，您可以将访问密钥和密钥更新为 [!DNL Amazon S3] 位置。

要更新基本连接的组件，请执行 `PATCH` 请求 `/connections` 端点，同时提供基本连接ID、版本以及要使用的新值。

请记住，您的基本连接ID位于 [上一步](#look-up-dataflow-details)，在您检查到参数所需目标的现有数据流时 `baseConnection`.

>[!IMPORTANT]
>
>此 `If-Match` 进行以下操作时需要标题： `PATCH` 请求。 此标头的值是您要更新的基础连接的唯一版本。 每次成功更新流实体（例如数据流、基本连接等）时，etag值都会更新。
>
> GET要获取最新版本的Etag值，请对 `/connections/{BASE_CONNECTION_ID}` 端点，其中 `{BASE_CONNECTION_ID}` 是您要更新的基本连接ID。
>
> 确保将 `If-Match` 标题加双引号，如下面的示例所示 `PATCH` 请求。

下面是一些示例，用于为不同类型的目标更新基本连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取基本连接ID > `PATCH` 具有所需参数的更新值的基连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求将更新 `accessId` 和 `secretKey` 的参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的电子标记。 您可以通过向以下网站发出GET请求来验证更新： [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**请求**

以下请求更新的 [[!DNL Azure Blob] 目标](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 连接，用于更新连接到Azure Blob实例所需的连接字符串。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的电子标记。 您可以通过向以下网站发出GET请求来验证更新： [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) 有关解释错误响应的更多信息，请参阅平台故障排除指南。

## 后续步骤 {#next-steps}

通过学习本教程，您已了解如何使用更新目标连接的各种组件。 [!DNL Flow Service] API。 欲知目标的更多信息，请参见 [目标概述](../home.md).
