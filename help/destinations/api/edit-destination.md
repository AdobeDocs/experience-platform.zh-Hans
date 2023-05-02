---
solution: Experience Platform
title: 使用流量服务API编辑目标连接
type: Tutorial
description: 了解如何使用流量服务API编辑目标连接的各个组件。
source-git-commit: 52fe0ef2ab195756c381b3ef0a5792dffe459b8d
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 2%

---

# 使用流量服务API编辑目标连接

本教程介绍了编辑目标连接各个组件的步骤。 了解如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 本教程中描述的编辑操作当前仅通过流服务API受支持。

## 快速入门 {#get-started}

本教程要求您拥有有效的数据流ID。 如果您没有有效的数据流ID，请从 [目标目录](../catalog/overview.md) 并按照 [连接到目标](../ui/connect-destination.md) 和 [激活数据](../ui/activation-overview.md) 在尝试本教程之前。

>[!NOTE]
>
> 术语 *流量* 和 *数据流* 在本教程中可互换使用。 在本教程的上下文中，它们具有相同的含义。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [目标](../home.md): [!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 读取示例API调用 {#reading-sample-api-calls}

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

### 收集所需标题的值 {#gather-values-for-required-headers}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 标头未指定，请求将在 `prod` 沙盒。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

编辑目标连接的第一步是使用流ID检索数据流详细信息。 通过向发出GET请求，可以查看现有数据流的当前详细信息 `/flows` 端点。

>[!TIP]
>
>您可以使用Experience PlatformUI获取目标的所需数据流ID。 转到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]**，选择所需的目标数据流并在右边栏中查找目标ID。 目标ID是您将在下一步中用作流ID的值。
>
> ![使用Experience PlatformUI获取目标ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 独特 `id` 要检索的目标数据流的值。 |

**请求**

以下请求会检索有关您的流ID的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)及其他相关信息。 与本教程最相关的是在以下响应中突出显示的Target连接和基本连接ID。 您将在后续部分中使用这些ID来更新目标连接的各个组件。

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

目标连接的组件因目标而异。 例如， [!DNL Amazon S3] 目标中，您可以更新导出文件的存储段和路径。 对于 [!DNL Pinterest] 目标，您可以更新 [!DNL Pinterest Advertiser ID] 对于 [!DNL Google Customer Match] 您可以在 [!DNL Pinterest Account ID].

要更新目标连接的组件，请向 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，同时提供您要使用的target连接ID、版本和新值。 请记住，在您检查到所需目标的现有数据流时，您在上一步中获得了目标连接ID。

>[!IMPORTANT]
>
>的 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的目标连接的唯一版本。 每次成功更新流程实体（如数据流、目标连接等）时，etag值都会随之更新。
>
> 要获取etag值的最新版本，请向 `/targetConnections/{TARGET_CONNECTION_ID}` 端点，其中 `{TARGET_CONNECTION_ID}` 是要更新的目标连接ID。

以下是更新目标连接规范中不同类型目标参数的一些示例。 但是，用于更新任何目标参数的一般规则如下：

获取连接的数据流ID >获取目标连接ID >将目标连接PATCH为所需参数的更新值。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!ENDSHADEBOX]


>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求更新了 `bucketName` 和 `path` 参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

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
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的Target连接ID和更新的Etag。 您可以通过向 [!DNL Flow Service] API，同时提供您的Target连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager 360]

**请求**

以下请求更新了 [[!DNL Google Ad Manager 360] 目标](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 连接，以向区段名称字段添加新的附加区段ID。

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
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的Target连接ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供您的Target连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**请求**

以下请求更新了 `advertiserId` 参数 [[!DNL Pinterest] 目标连接](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的Target连接ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供您的Target连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## 编辑基本连接组件（身份验证参数和其他组件） {#patch-base-connection}

基本连接的组件因目标而异。 例如， [!DNL Amazon S3] 目标中，您可以将访问密钥和密钥更新为 [!DNL Amazon S3] 位置。

要更新基本连接的组件，请向 `/connections` 端点，同时提供您要使用的基本连接ID、版本和新值。

请记住，在您检查到所需目标的现有数据流时，您在上一步中获得了基本连接ID。

>[!IMPORTANT]
>
>的 `If-Match` 发出PATCH请求时需要标头。 此标头的值是要更新的基本连接的唯一版本。 每次成功更新流量实体（如数据流、基本连接等）时，etag值都会随之更新。
>
> 要获取etag值的最新版本，请向 `/connections/{BASE_CONNECTION_ID}` 端点，其中 `{BASE_CONNECTION_ID}` 是要更新的基本连接ID。

以下是更新基本连接规范中不同类型目标参数的一些示例。 但是，用于更新任何目标参数的一般规则如下：

获取连接的数据流ID >获取基本连接ID >将基本连接PATCH为所需参数的更新值。

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求更新了 `accessId` 和 `secretKey` 参数 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目标连接。

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
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的基本连接ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**请求**

以下请求会更新 [[!DNL Azure Blob] 目标](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 连接，以更新连接到Azure Blob实例所需的连接字符串。

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
| `op` | 用于定义更新数据流所需的操作的操作调用。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 定义要更新的流程部分。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回您的基本连接ID和更新的标记。 您可以通过向 [!DNL Flow Service] API，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规的Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) ，以了解有关解释错误响应的更多信息。

## 后续步骤 {#next-steps}

通过阅读本教程，您学习了如何使用 [!DNL Flow Service] API。 有关目标的更多信息，请参阅 [目标概述](../home.md).
