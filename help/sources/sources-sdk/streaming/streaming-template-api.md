---
title: 流SDK API的文档自助服务模板
description: 了解如何使用流服务API将流数据从源引入Adobe Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: eb317f38499a32b1a6eb072ec74e68cdfebf994f
workflow-type: tm+mt
source-wordcount: '1699'
ht-degree: 1%

---

# 创建要流式处理的源连接和数据流 *YOURSOURCE* 数据使用 [!DNL Flow Service] API

*浏览此模板时，替换或删除所有斜体段落（从此段落开始）。*

*首先，在页面顶部更新元数据（标题和描述）。 请忽略此页面上的所有DNL实例。 此标记可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 我们会在您提交文档后将标记添加到文档中。*

## 概述

*提供贵公司的简短概览，包括贵公司为客户提供的价值。 添加指向产品文档主页的链接以供进一步阅读。*

>[!IMPORTANT]
>
>此文档页面由创建 *YOURSOURCE* 团队。 如有任何查询或更新请求，请直接通过 *插入链接或电子邮件地址，您可以从中获取更新*.

## 先决条件

*在此部分中添加有关客户在Adobe Experience Platform用户界面中开始设置源之前需要了解的任何信息。 这可能与以下内容有关：*

* *需要添加到允许列表*
* *电子邮件哈希处理要求*
* *任何账户详情*
* *如何获取API密钥以连接到您的平台*

### 收集所需的凭据

为了连接 *YOURSOURCE* 要Experience Platform，必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| *凭据1* | *请在此处为源的身份验证凭据添加简短描述* | *请在此处添加源身份验证凭据的示例* |
| *凭据二* | *请在此处为源的身份验证凭据添加简短描述* | *请在此处添加源身份验证凭据的示例* |
| *凭据3* | *请在此处为源的身份验证凭据添加简短描述* | *请在此处添加源身份验证凭据的示例* |

有关这些凭据的更多信息，请参阅 *YOURSOURCE* 身份验证文档。 *请在此处添加指向您平台的身份验证文档的链接*.

### 集成 *YOURSOURCE* 使用您的webhook

*流SDK要求您的源能够支持Webhook，以便与Experience Platform通信。 在本节中，您必须提供用户必须遵循的步骤，才能将YOURSOURCE与webhook集成。*

## Connect *YOURSOURCE* 到平台，使用 [!DNL Flow Service] API

以下教程将指导您完成创建 *YOURSOURCE* 源连接并创建数据流以引入 *YOURSOURCE* 使用将数据发送到平台 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### 创建源连接 {#source-connection}

通过向POST请求创建源连接 [!DNL Flow Service] API，同时提供源的连接规范ID、名称和描述等详细信息以及数据的格式。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求创建源连接 *YOURSOURCE*：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 确保源连接的名称是描述性的，因为您可以使用此名称查找源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 的格式 *YOURSOURCE* 要摄取的数据。 目前，唯一支持的数据格式为 `json`. |

**响应**

成功响应将返回唯一标识符(`id`)。 此ID在后续步骤中是创建数据流所必需的。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 创建目标XDM架构 {#target-schema}

为了在Platform中使用源数据，必须创建一个目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Platform数据集。

可以通过向以下对象执行POST请求来创建目标XDM架构 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅关于的教程 [使用API创建架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 创建目标数据集 {#target-dataset}

可以通过向执行POST请求来创建目标数据集 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅关于的教程 [使用API创建数据集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您拥有目标架构、目标数据集和到数据湖的连接规范ID的唯一标识符。 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含入站源数据的数据集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求创建目标连接 *YOURSOURCE*：


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于数据湖的连接规范ID。 此固定ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 *YOURSOURCE* 要带到Platform的数据。 |
| `params.dataSetId` | 在上一步中检索的目标数据集ID。 |


**响应**

成功响应将返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 创建映射 {#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所遵循的目标架构。 这可以通过向以下对象执行POST请求来实现 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在请求有效负载中定义数据映射。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 的ID [目标XDM架构](#target-schema) 在之前的步骤中生成。 |
| `mappings.destinationXdmPath` | 源属性将映射到的目标XDM路径。 |
| `mappings.sourceAttribute` | 需要映射到目标XDM路径的源属性。 |
| `mappings.identity` | 一个布尔值，指定是否将映射集标记为 [!DNL Identity Service]. |

**响应**

成功响应将返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 创建流 {#flow}

从以下来源获取数据的最后一步 *YOURSOURCE* 到Platform就是创建数据流。 现在，您已准备以下必需值：

* [源连接ID](#source-connection)
* [目标连接ID](#target-connection)
* [映射Id](#mapping)

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
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为 `1.0`. |
| `sourceConnectionIds` | 此 [源连接ID](#source-connection) 在之前的步骤中生成。 |
| `targetConnectionIds` | 此 [目标连接Id](#target-connection) 在之前的步骤中生成。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入到Platform时需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 此 [映射Id](#mapping) 在之前的步骤中生成。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为 `0`. |

**响应**

成功的响应会返回ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### 获取您的流端点URL

创建数据流后，您现在可以检索流端点URL。 您将使用此端点URL将源订阅到webhook，从而允许源与Experience Platform通信。

GET要检索您的流端点URL，请向 `/flows` 端点并提供数据流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回有关您的数据流的信息，包括您的端点URL，这些信息标记为 `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## 附录

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读以下指南： [使用API监控源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新您的数据流

通过向发出PATCH请求，更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 `/flows` 端点 [!DNL Flow Service] API，同时提供数据流的ID。 发出PATCH请求时，必须提供数据流的唯一值 `etag` 在 `If-Match` 标头。 有关完整的API示例，请阅读以下指南： [使用API更新源数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帐户

PATCH通过向 [!DNL Flow Service] API，同时将基本连接ID作为查询参数提供。 在提出PATCH请求时，您必须提供源帐户的唯一 `etag` 在 `If-Match` 标头。 有关完整的API示例，请阅读以下指南： [使用API更新源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 删除数据流

通过向以下对象执行DELETE请求来删除您的数据流： [!DNL Flow Service] API，以便在查询参数中提供要删除的数据流的ID。 有关完整的API示例，请阅读以下指南： [使用API删除数据流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 删除您的帐户

向以下人员发出DELETE请求以删除您的帐户： [!DNL Flow Service] 提供要删除的帐户的基本连接ID时的API。 有关完整的API示例，请阅读以下指南： [使用API删除源帐户](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).