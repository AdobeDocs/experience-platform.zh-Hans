---
solution: Experience Platform
title: 使用流服务API编辑目标连接
type: Tutorial
description: 了解如何使用流服务API编辑目标连接的各种组件。
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 5%

---

# 使用流服务API编辑目标连接

本教程涵盖了编辑目标连接的各种组件的步骤。 了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新身份验证凭据、导出位置等。

>[!NOTE]
>
> 本教程中描述的编辑操作当前仅通过流服务API受支持。

## 快速入门 {#get-started}

本教程要求您拥有有效的数据流ID。 如果您没有有效的数据流ID，请从[目标目录](../catalog/overview.md)中选择您选择的目标，并执行[连接到目标](../ui/connect-destination.md)和[激活数据](../ui/activation-overview.md)中列出的步骤，然后再尝试本教程。

>[!NOTE]
>
> 在本教程中，术语&#x200B;*流*&#x200B;和&#x200B;*数据流*&#x200B;可互换使用。 在本教程的上下文中，它们具有相同的含义。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [目标](../home.md)： [!DNL Destinations]是预先构建的与目标平台的集成，可无缝激活Adobe Experience Platform中的数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。
* [沙盒](../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用[!DNL Flow Service] API成功更新数据流。

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值 {#gather-values-for-required-headers}

要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对Experience Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`标头，则在`prod`沙盒下解析请求。

包含有效负载(`POST`、`PUT`、`PATCH`)的所有请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找数据流详细信息 {#look-up-dataflow-details}

编辑目标连接的第一步是使用流ID检索数据流详细信息。 通过向`/flows`端点发出GET请求，可查看现有数据流的当前详细信息。

>[!TIP]
>
>您可以使用Experience Platform UI获取目标的数据流ID。 转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 浏览]**，选择所需的目标数据流并在右边栏中找到目标ID。 目标ID是您将在下一步中用作流ID的值。
>
> ![使用Experience Platform UI获取目标ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要检索的目标数据流的唯一`id`值。 |

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

成功响应将返回数据流的当前详细信息，包括其版本、唯一标识符(`id`)和其他相关信息。 与本教程最相关的内容是下面的响应中高亮显示的目标连接ID和基本连接ID。 您将在下一节中使用这些ID来更新目标连接的各种组件。

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

目标连接的组件因目标而异。 例如，对于[!DNL Amazon S3]目标，您可以更新导出文件的存储段和路径。 对于[!DNL Pinterest]目标，您可以更新[!DNL Pinterest Advertiser ID]，对于[!DNL Google Customer Match]，您可以更新[!DNL Pinterest Account ID]。

要更新目标连接的组件，请在提供目标连接ID、版本和要使用的新值的同时，对`/targetConnections/{TARGET_CONNECTION_ID}`端点执行`PATCH`请求。 请记住，在上一步中，当您检查到所需目标的现有数据流时，您获得了目标连接ID。

>[!IMPORTANT]
>
>发出`PATCH`请求时需要使用`If-Match`标头。 此标头的值是要更新的目标连接的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> 要获取最新版本的etag值，请对`/targetConnections/{TARGET_CONNECTION_ID}`端点执行GET请求，其中`{TARGET_CONNECTION_ID}`是您要更新的目标连接ID。
>
> 在发出`PATCH`请求时，请确保将`If-Match`标头的值用双引号括起来，如以下示例中所示。

以下是一些示例，说明如何更新不同类型目标的目标连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取目标连接ID > `PATCH`具有所需参数更新值的目标连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求更新[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目标连接的`bucketName`和`path`参数。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的Etag。 您可以向[!DNL Flow Service] API发出GET请求，同时提供目标连接ID来验证更新。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google广告管理器和Google广告管理器360]

**请求**

以下请求更新[[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md)或[[!DNL Google Ad Manager 360] 目标](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details)连接的参数，以将新的[**[!UICONTROL 附加受众ID添加到受众名称]**](/help/release-notes/2023/april-2023.md#destinations)字段。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供目标连接ID来验证更新。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**请求**

以下请求更新[[!DNL Pinterest] 目标连接](/help/destinations/catalog/advertising/pinterest.md#parameters)的`advertiserId`参数。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的目标连接ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求，同时提供目标连接ID来验证更新。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 编辑基本连接组件（身份验证参数和其他组件） {#patch-base-connection}

在要更新目标的凭据时编辑基本连接。 基本连接的组件因目标而异。 例如，对于[!DNL Amazon S3]目标，您可以将访问密钥和密钥更新到您的[!DNL Amazon S3]位置。

要更新基本连接的组件，请在提供基本连接ID、版本和要使用的新值时对`/connections`端点执行`PATCH`请求。

请记住，您在[上一步](#look-up-dataflow-details)中获取了基本连接ID，当时您为参数`baseConnection`检查了到所需目标的现有数据流。

>[!IMPORTANT]
>
>发出`PATCH`请求时需要使用`If-Match`标头。 此标头的值是您要更新的基础连接的唯一版本。 每次成功更新流实体（例如数据流、基本连接等）时，etag值都会更新。
>
> 要获取最新版本的Etag值，请对`/connections/{BASE_CONNECTION_ID}`端点执行GET请求，其中`{BASE_CONNECTION_ID}`是您要更新的基本连接ID。
>
> 在发出`PATCH`请求时，请确保将`If-Match`标头的值用双引号括起来，如以下示例中所示。

下面是一些示例，用于为不同类型的目标更新基本连接规范中的参数。 但更新任何目标的参数的一般规则如下：

获取连接的数据流ID >获取基本连接ID > `PATCH`具有所需参数更新值的基本连接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

以下请求更新[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目标连接的`accessId`和`secretKey`参数。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求来验证更新，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**请求**

以下请求更新[[!DNL Azure Blob] 目标](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate)连接的参数，以更新连接到Azure Blob实例所需的连接字符串。

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
| `op` | 操作调用，用于定义更新数据流所需的操作。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 定义要更新的流部分。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您的基本连接ID和更新的电子标记。 您可以向[!DNL Flow Service] API发出GET请求来验证更新，同时提供基本连接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience Platform API错误消息原则。 有关解释错误响应的详细信息，请参阅Experience Platform疑难解答指南中的[API状态代码](/help/landing/troubleshooting.md#api-status-codes)和[请求标头错误](/help/landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

通过学习本教程，您已了解如何使用[!DNL Flow Service] API更新目标连接的各种组件。 有关目标的详细信息，请参阅[目标概述](../home.md)。
