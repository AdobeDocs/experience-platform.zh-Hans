---
title: 使用流服务API为Pendo创建源连接和数据流
description: 了解如何使用流服务API将Adobe Experience Platform连接到Pendo。
badge: Beta 版
exl-id: 12b0295d-4b26-4eb7-a02a-a01d825d2a1e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 2%

---

# 为以下对象创建源连接和数据流 [!DNL Pendo] 使用流服务API

>[!NOTE]
>
>此 [!DNL Pendo] 源为测试版。 请阅读 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

以下教程将指导您完成创建源连接和要引入的数据流的步骤 [[!DNL Pendo]](https://Pendo.com/) 使用将事件数据发送到Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门 {#getting-started}

本指南要求您对 Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 连接 [!DNL Pendo] 到平台，使用 [!DNL Flow Service] API {#connect-platform-to-flow-api}

下面概述了创建源连接和数据流以引入 [!DNL Pendo] 要Experience Platform的事件数据。

### 创建源连接 {#source-connection}

通过向发出POST请求来创建源连接 [!DNL Flow Service] API，同时提供源的连接规范ID、名称和描述等详细信息以及数据的格式。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求为创建源连接 [!DNL Pendo]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Pendo",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Pendo",
      "connectionSpec": {
          "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 的格式 [!DNL Pendo] 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |

**响应**

成功的响应将返回唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### 创建目标XDM架构 {#target-schema}

为了在Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Platform数据集。

可以通过向以下对象执行POST请求来创建目标XDM架构 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅关于的教程 [使用API创建架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### 创建目标数据集 {#target-dataset}

可以通过向执行POST请求来创建目标数据集 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅关于的教程 [使用API创建数据集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含入站源数据的数据集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求创建目标连接 [!DNL Pendo]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Pendo",
      "description": "Streaming Target Connection for Pendo",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/b48de0b204046e65a4c50232e7946401946b4c519fd7c172",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63dca52231a6031c07280614"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于数据湖的连接规范ID。 此固定ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 [!DNL Pendo] 要摄取的数据。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |

**响应**

成功的响应将返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。 这可以通过向以下对象执行POST请求来实现 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 请求有效负载中定义的数据映射。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.accountid",
            "sourceAttribute": "accountId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.uniqueid",
            "sourceAttribute": "uniqueId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.name1",
            "sourceAttribute": "properties.guideProperties.name",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestamp1",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.visitorid",
            "sourceAttribute": "visitorId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目标XDM架构](#target-schema) 在之前的步骤中生成。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

**响应**

成功响应将返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "a126ae1a1d134c4b82bd00c2d01a039e",
    "version": 0,
    "createdDate": 1676881164541,
    "modifiedDate": 1676881164541,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 创建流 {#flow}

从以下来源获取数据的最后一步 [!DNL Pendo] 到Platform就是创建数据流。 现在，您已准备以下必需值：

* [源连接ID](#source-connection)
* [目标连接ID](#target-connection)
* [映射 ID](#mapping)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供上述值时执行POST请求来创建数据流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Pendo",
      "description": "Streaming Dataflow for Pendo",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
      ],
      "targetConnectionIds": [
          "df7c660e-3484-463b-b01a-1835e9b04ac9"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bae11501021646e58cecc1182451af22",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为 `1.0`. |
| `sourceConnectionIds` | 此 [源连接ID](#source-connection) 在之前的步骤中生成。 |
| `targetConnectionIds` | 此 [目标连接Id](#target-connection) 在之前的步骤中生成。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入到Platform时需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 此 [映射ID](#mapping) 在之前的步骤中生成。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为 `0`. |

**响应**

成功的响应会返回ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### 获取您的流端点URL {#get-streaming-url}

创建数据流后，您现在可以检索流端点URL。 您将使用此端点URL将源订阅到webhook，从而允许源与Experience Platform通信。

GET要检索您的流端点URL，请向 `/flows` 端点并提供数据流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有关数据流的信息，包括标记为的端点URL `inletUrl`. 请参阅 [设置Webhook](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) 页面以获取所需的值。

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Pendo",
            "description": "Streaming Dataflow for Pendo",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "etag": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "sourceConnectionIds": [
                "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
            ],
            "targetConnectionIds": [
                "df7c660e-3484-463b-b01a-1835e9b04ac9"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "339d60a5-9ff6-4eba-8197-e8887eeb3c08",
                        "connectionSpec": {
                            "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "df7c660e-3484-463b-b01a-1835e9b04ac9",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e389c18dbc7f5de8b95df07b1b89d76ddd9b1e88d5423abc71b6ac9161491373"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "bae11501021646e58cecc1182451af22",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4d90b316-1c9b-469d-935f-5a27d5deefdf",
            "providerRefId": "19d9fb14-9cb9-42a5-bb8b-23dc545e766a",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            },
            "lastRunDetails": {
                "id": "d6972216-2332-41f6-8ed3-2ac82e6550b7",
                "state": "partialSuccess",
                "startedAtUTC": 1676862000000,
                "completedAtUTC": 1676867880000
            }
        }
    ]
}
```

## 附录 {#appendix}

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流 {#monitor-dataflow}

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读以下指南： [使用API监控源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新您的数据流 {#update-dataflow}

通过向发出PATCH请求，更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 `/flows` 端点 [!DNL Flow Service] API，同时提供数据流的ID。 发出PATCH请求时，必须提供数据流的唯一值 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读以下指南： [使用API更新源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帐户 {#update-account}

PATCH通过向 [!DNL Flow Service] API，同时将您的基本连接ID作为查询参数提供。 发出PATCH请求时，必须提供源帐户的唯一帐户 `etag` 在 `If-Match` 标题。 有关完整的API示例，请阅读以下指南： [使用API更新源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 删除您的数据流 {#delete-dataflow}

通过向以下对象执行DELETE请求来删除您的数据流： [!DNL Flow Service] API，同时提供您要作为查询参数的一部分删除的数据流的ID。 有关完整的API示例，请阅读以下指南： [使用API删除数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 删除您的帐户 {#delete-account}

向以下网站发出DELETE请求，删除您的帐户： [!DNL Flow Service] API，同时提供要删除帐户的基本连接ID。 有关完整的API示例，请阅读以下指南： [使用API删除源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
