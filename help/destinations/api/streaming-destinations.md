---
keywords: Experience Platform；主页；热门主题；API教程；流目标API;平台
solution: Experience Platform
title: 使用Adobe Experience Platform中的Flow Service API连接到流目标并激活数据
description: 本文档包括通过使用Adobe Experience Platform API创建流目标
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 1%

---


# 使用Flow Service API连接到流目标并激活数据

>[!NOTE]
>
>平台中的[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目标当前处于测试阶段。 文档和功能可能会发生变化。

本教程演示了如何使用API调用连接到Adobe Experience Platform存储，创建到流云事件目标([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md)或[Azure集线器](../catalog/cloud-storage/azure-event-hubs.md))的连接，创建到新创建目标的数据流，以及将数据激活到新创建的目标。

本教程在所有示例中使用[!DNL Amazon Kinesis]目标，但对于[!DNL Azure Event Hubs]，这些步骤是相同的。

![概述 — 创建流目标和激活区段的步骤](../assets/api/streaming-destination/overview.png)

如果您希望使用平台中的用户界面连接到目标并激活数据，请参阅[连接目标](../ui/connect-destination.md)和[将用户档案和区段激活到目标](../ui/activate-destinations.md)教程。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是Experience Platform中数据位置和谱系的记录系统。
* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了在平台中将数据激活到流目标所需的其他信息。

### 收集所需凭据

要完成本教程中的步骤，您应准备好以下凭据，具体取决于要连接和激活区段的目标类型。

* 对于[!DNL Amazon Kinesis]连接：`accessKeyId`、`secretKey`、`region`或`connectionUrl`
* 对于[!DNL Azure Event Hubs]连接：`sasKeyName`、`sasKey`、`namespace`

### 读取示例API调用{#reading-sample-api-calls}

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集必需和可选标头{#gather-values}的值

要调用平台API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：承载`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的资源可以隔离到特定的虚拟沙箱。 在向平台API发出的请求中，您可以指定操作将在中进行的沙箱的名称和ID。 这些是可选参数。

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

### Swagger文档{#swagger-docs}

您可以在Swagger的本教程中找到所有API调用的随附参考文档。 请参阅Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)上的[ Flow Service API文档。 我们建议您同时使用本教程和Swagger文档页。

## 获取可用流目标{#get-the-list-of-available-streaming-destinations}的列表

![目标步骤概述步骤1](../assets/api/streaming-destination/step1.png)

作为第一步，您应确定要激活数据的流目标。 首先，请发出呼叫，请求列表可连接和激活区段的可用目标。 对`connectionSpecs`端点执行以下GET请求，以返回可用目标的列表:

**API格式**

```http
GET /connectionSpecs
```

**请求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**响应**

成功的响应包含可用目标及其唯一标识符的列表(`id`)。 存储您计划使用的目标的值，因为在后续步骤中需要它。 例如，如果要将区段连接到[!DNL Amazon Kinesis]或[!DNL Azure Event Hubs]并将其传送，请在响应中查找以下代码片段：

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## 连接到您的Experience Platform数据{#connect-to-your-experience-platform-data}

![目标步骤概述步骤2](../assets/api/streaming-destination/step2.png)

接下来，您必须连接到Experience Platform数据，以便导出用户档案数据并在首选目标中激活它。 这包括两个子步骤，如下所述。

1. 首先，您必须通过设置基本连接来执行呼叫，以授权访问Experience Platform中的数据。
2. 然后，使用基本连接ID，您将再进行一次调用，在其中创建源连接，从而建立与Experience Platform数据的连接。


### 授权访问您的Experience Platform

**API格式**

```http
POST /connections
```

**请求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`:使用统一用户档案服务的连接规范ID -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一步创建源连接时，按需要存储此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 连接到您的Experience Platform数据{#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上一步中获得的ID。
* `{CONNECTION_SPEC_ID}`:使用统一用户档案服务的连接规范ID -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**响应**

成功的响应返回新创建的源连接到统一用户档案服务的唯一标识符(`id`)。 这将确认您已成功连接到Experience Platform数据。 在后续步骤中存储所需的值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 连接到流目标{#connect-to-streaming-destination}

![目标步骤概述步骤3](../assets/api/streaming-destination/step3.png)

在此步骤中，您将设置到所需流目标的连接。 这包括两个子步骤，如下所述。

1. 首先，必须通过设置基本连接来执行对流目标的访问授权调用。
2. 然后，使用基本连接ID，您将进行另一次调用，在其中创建目标连接，该连接指定存储帐户中要传送导出数据的位置，以及将导出的数据的格式。

### 授权访问流目标

**API格式**

```http
POST /connections
```

**请求**

>[!IMPORTANT]
>
>以下示例包含前缀为`//`的代码注释。 这些注释突出显示了必须对不同的流目标使用不同值的位置。 请在使用代码片断之前删除注释。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`:使用您在获取可用目标的列表步骤 [中获得的连接规范ID](#get-the-list-of-available-destinations)。
* `{AUTHENTICATION_CREDENTIALS}`:填写流目标的名称： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`者
* `{ACCESS_ID}`: *用于 [!DNL Amazon Kinesis] 连接。* 您的Amazon Kinesis存储位置访问ID。
* `{SECRET_KEY}`: *用于 [!DNL Amazon Kinesis] 连接。* 您Amazon Kinesis存储位置的密钥。
* `{REGION}`: *用于 [!DNL Amazon Kinesis] 连接。* 您帐户中平台 [!DNL Amazon Kinesis] 将流式传输您数据的区域。
* `{SAS_KEY_NAME}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写您的SAS密钥名称。了解在[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS键对[!DNL Azure Event Hubs]进行身份验证。
* `{SAS_KEY}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写您的SAS密钥。了解在[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS键对[!DNL Azure Event Hubs]进行身份验证。
* `{EVENT_HUB_NAMESPACE}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写平台 [!DNL Azure Event Hubs] 将在何处传输您的数据。有关详细信息，请参阅[!DNL Microsoft]文档中的[创建事件集线器命名空间](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一步创建目标连接时，按需要存储此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 指定存储位置和数据格式

**API格式**

```http
POST /targetConnections
```

**请求**

>[!IMPORTANT]
>
>以下示例包含前缀为`//`的代码注释。 这些注释突出显示了必须对不同的流目标使用不同值的位置。 请在使用代码片断之前删除注释。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上述步骤中获得的基本连接ID。
* `{CONNECTION_SPEC_ID}`:使用您在步骤获取可用目标 [的列表中获得的连接规范](#get-the-list-of-available-destinations)。
* `{NAME_OF_DATA_STREAM}`: *用于 [!DNL Amazon Kinesis] 连接。* 在帐户中提供现有数据流的 [!DNL Amazon Kinesis] 名称。平台会将数据导出到此流。
* `{REGION}`: *用于 [!DNL Amazon Kinesis] 连接。* 您的Amazon Kinesis帐户中的平台将在此传输您的数据的区域。
* `{EVENT_HUB_NAME}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写平台 [!DNL Azure Event Hub] 将在其中流式传输您的数据的名称。有关详细信息，请参阅[!DNL Microsoft]文档中的[创建事件集线器](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)。

**响应**

成功的响应返回新创建的目标到流目标的连接的唯一标识符(`id`)。 按照后续步骤中的要求存储此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 创建数据流

![目标步骤概述步骤4](../assets/api/streaming-destination/step4.png)

使用您在前面的步骤中获得的ID，您现在可以在Experience Platform数据与要激活数据的目标之间创建数据流。 将此步骤视为构建Experience Platform和目标之间的管道，数据随后将通过管道流动。

要创建POST流，请执行如下所示的数据请求，同时在负载中提供以下所述的值。

执行以下POST请求以创建数据流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`:基于用户档案的目标的流规范ID为 `71471eba-b620-49e4-90fd-23f1fa0174d8`。在调用中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用在步骤连接到Experience Platform中获 [得的源连接ID](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在步骤连接到流目标时获 [得的目标连接ID](#connect-to-streaming-destination)。

**响应**

成功的响应返回新创建的数据流的ID(`id`)和`etag`。 记下这两个值。 正如您在下一步中所做的那样，激活区段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 将数据激活到新目标{#activate-data}

![目标步骤概述步骤5](../assets/api/streaming-destination/step5.png)

创建了所有连接和数据流后，现在您可以将用户档案数据激活到流平台。 在此步骤中，您可以选择要发送到目标的区段和用户档案属性，并可以计划和将数据发送到目标。

要将区段激活到新目标，必须执行JSONPATCH操作，如下例所示。 您可以在一次调用中激活多个区段和用户档案属性。 要进一步了解JSONPATCH，请参阅[RFC规范](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**请求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

* `{DATAFLOW_ID}`:使用您在上一步中获得的数据流。
* `{ETAG}`:使用您在上一步中获得的标签。
* `{SEGMENT_ID}`:提供要导出到此目标的区段ID。要检索要激活的区段的区段ID，请转到&#x200B;**https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**，在左侧导航菜单中选择&#x200B;**[!UICONTROL 分段服务API]**，然后在&#x200B;**[!UICONTROL 区段定义]**&#x200B;中查找`GET /segment/definitions`操作。
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或  `person.lastName`

**响应**

查找202 OK响应。 不返回响应正文。 要验证请求是否正确，请参阅下一步验证数据流。

## 验证数据流

![目标步骤概述步骤6](../assets/api/streaming-destination/step6.png)

作为教程的最后一步，您应验证区段和用户档案属性确实已正确映射到数据流。

要验证此项，请执行以下GET请求：

**API格式**

```http
GET /flows
```

**请求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:使用上一步中的数据流。
* `{ETAG}`:使用上一步中的etag。

**响应**

返回的响应应包含在`transformations`参数中您在上一步中提交的区段和用户档案属性。 响应中的示例`transformations`参数可能如下所示：

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**导出的数据**

>[!IMPORTANT]
>
> 除了步骤[将用户档案激活到新目标](#activate-data)中的属性和区段之外，[!DNL AWS Kinesis]和[!DNL Azure Event Hubs]中导出的数据还将包含有关标识映射的信息。 这表示导出的用户档案的身份（例如[ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html)、移动ID、Google ID、电子邮件地址等）。 请参阅以下示例。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 使用Postman集合连接到流目标{#collections}

要以更简化的方式连接到本教程中介绍的流目标，您可以使用[[!DNL Postman]](https://www.postman.com/)。

[!DNL Postman] 是一种工具，可用于进行API调用和管理预定义调用和环境库。

对于此特定教程，已附加以下[!DNL Postman]集合：

* [!DNL AWS Kinesis] [!DNL Postman] collection
* [!DNL Azure Event Hubs] [!DNL Postman] collection

单击[此处](../assets/api/streaming-destination/DestinationPostmanCollection.zip)下载集合存档。

每个集合分别包含[!DNL AWS Kinesis]和[!DNL Azure Event Hub]所需的请求和环境变量。

### 如何使用Postman集合

要使用附加的[!DNL Postman]集合成功连接到目标，请执行以下步骤：

* 下载并安装[!DNL Postman];
* [下](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 载并解压缩附加的集合；
* 将收藏集从相应的文件夹导入邮递员；
* 按照本文的说明填写环境变量；
* 根据本文中的说明，运行来自Postman的[!DNL API]请求。

## 后续步骤

通过本教程，您已成功将平台连接到您的首选流目标之一，并设置到相应目标的数据流。 传出数据现在可用于目标位置，以便进行客户分析或您希望执行的任何其他数据操作。 有关更多详细信息，请参阅以下页面：

* [目标概述](../home.md)
* [目标目录概述](../catalog/overview.md)
