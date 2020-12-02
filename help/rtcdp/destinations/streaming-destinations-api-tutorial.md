---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: 连接到流目标并激活数据
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: f12b400ca95e23d8e6ac282fafa8f4bb141d703a
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 2%

---


# 在Adobe的实时客户数据平台中使用API调用连接到流目标并激活数据

>[!NOTE]
>
>Adobe [!DNL Amazon Kinesis] 实时 [!DNL Azure Event Hubs] CDP中的目标和目标目前处于测试阶段。 文档和功能可能会发生变化。

本教程演示如何使用API调用连接到您的Adobe Experience Platform存储、创建到流云目标([AmazonKinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)[或Azure事件中心](/help/rtcdp/destinations/azure-event-hubs-destination.md))的连接、创建到新创建目标的数据流以及将数据激活到新创建的目标。

本教程在所 [!DNL Amazon Kinesis] 有示例中都使用目标，但步骤相同 [!DNL Azure Event Hubs]。

![概述——创建流目标和激活区段的步骤](/help/rtcdp/destinations/assets/flow-prelim.png)

如果您希望使用Adobe实时CDP中的用户界面连接到目标并激活数据，请参 [阅连接目标](../../rtcdp/destinations/connect-destination.md)[并将用户档案和区段激活到目标教程](../../rtcdp/destinations/activate-destinations.md) 。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是Experience Platform内数据位置和谱系的记录系统。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了在Adobe实时CDP中将数据激活到流目标时需要了解的其他信息。

### 收集所需的凭据

要完成本教程中的步骤，您应准备好以下凭据，具体取决于要连接和激活区段的目标类型。

* 对于 [!DNL Amazon Kinesis] 连接： `accessKeyId`、 `secretKey`、 `region` 或 `connectionUrl`
* 对于 [!DNL Azure Event Hubs] 连接： `sasKeyName`, `sasKey``namespace`

### 读取示例API调用 {#reading-sample-api-calls}

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集必需和可选标题的值 {#gather-values}

要调用平台API，您必须先完成身份验证 [教程](/help/tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的资源可以隔离到特定虚拟沙箱。 在对平台API的请求中，您可以指定操作将在其中进行的沙箱的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

### Swagger文档 {#swagger-docs}

您可以在Swagger的本教程中找到所有API调用的随附参考文档。 请参阅 [Adobe.io上的Flow Service API文档](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)。 我们建议您同时使用本教程和Swagger文档页面。

## 获得可用流目标的列表 {#get-the-list-of-available-streaming-destinations}

![目标步骤概述步骤1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

作为第一步，您应确定要激活数据的流目标。 首先，请执行呼叫以请求可连接和激活区段的可用目标列表。 对端点执行以下GET请 `connectionSpecs` 求，以返回可用目标的列表:

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

成功的响应包含可用目标及其唯一标识符的列表(`id`)。 存储您计划使用的目标的值，这是后续步骤中需要的。 例如，如果要连接区段并将其传送到或， [!DNL Amazon Kinesis] 请 [!DNL Azure Event Hubs]在响应中查找以下代码片断：

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

## 连接到Experience Platform数据 {#connect-to-your-experience-platform-data}

![目标步骤概述步骤2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

接下来，您必须连接到Experience Platform数据，以便导出用户档案数据并在首选目标中激活它。 这包括两个子步骤，如下所述。

1. 首先，必须通过设置基本连接，在Experience Platform中执行授权访问数据的调用。
2. 然后，使用基本连接ID，您将再次进行调用，在其中创建源连接，从而建立与Experience Platform数据的连接。


### 授权访问Experience Platform中的数据

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


* `{CONNECTION_SPEC_ID}`:使用统一用户档案服务的连接规范ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一步创建源连接时，按需要存储此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 连接到Experience Platform数据 {#connect-to-platform-data}

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
* `{CONNECTION_SPEC_ID}`:使用统一用户档案服务的连接规范ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**响应**

成功的响应会返回新创建的源`id`连接到统一用户档案服务的唯一标识符()。 这将确认您已成功连接到Experience Platform数据。 在以后的步骤中存储此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 连接到流目标 {#connect-to-streaming-destination}

![目标步骤概述步骤3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

在此步骤中，您将设置到所需流目标的连接。 这包括两个子步骤，如下所述。

1. 首先，必须通过设置基本连接来执行授权访问流目标的调用。
2. 然后，使用基本连接ID，您将再次进行调用，在其中创建目标连接，该连接指定存储帐户中要传送导出数据的位置以及要导出的数据的格式。

### 授权访问流目标

**API格式**

```http
POST /connections
```

**请求**

>[!IMPORTANT]
>
>以下示例包含前缀为的代码注释 `//`。 这些注释突出显示不同流目标必须使用不同值的位置。 请在使用代码片断之前删除注释。

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

* `{CONNECTION_SPEC_ID}`:使用您在获取可用目标的列表 [步骤中获得的连接规范ID](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md#get-the-list-of-available-destinations)。
* `{AUTHENTICATION_CREDENTIALS}`:填写流目标的名称： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`者
* `{ACCESS_ID}`: *用于 [!DNL Amazon Kinesis] 连接。* 您的AmazonKinesis存储位置的访问ID。
* `{SECRET_KEY}`: *用于 [!DNL Amazon Kinesis] 连接。* 你AmazonKinesis存储所的秘钥。
* `{REGION}`: *用于 [!DNL Amazon Kinesis] 连接。* Adobe实时 [!DNL Amazon Kinesis] CDP将流化您的数据所在的区域。
* `{SAS_KEY_NAME}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写您的SAS密钥名称。 了解Microsoft文档 [!DNL Azure Event Hubs] 中有关使用SAS密钥进 [行身份验证](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{SAS_KEY}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写您的SAS密钥。 了解Microsoft文档 [!DNL Azure Event Hubs] 中有关使用SAS密钥进 [行身份验证](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* `{EVENT_HUB_NAMESPACE}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写命名空间 [!DNL Azure Event Hubs] ,Adobe实时CDP将流化您的数据。 有关详细信息，请参 [阅文档中的创建事件中](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) 心 [!DNL Microsoft] 命名空间。

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
>以下示例包含前缀为的代码注释 `//`。 这些注释突出显示不同流目标必须使用不同值的位置。 请在使用代码片断之前删除注释。

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
* `{CONNECTION_SPEC_ID}`:使用您在获取可用目标列表 [步骤中获得的连接规范](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md#get-the-list-of-available-destinations)。
* `{NAME_OF_DATA_STREAM}`: *用于 [!DNL Amazon Kinesis] 连接。* 在帐户中提供现有数据流的 [!DNL Amazon Kinesis] 名称。 Adobe实时CDP会将数据导出到此流。
* `{REGION}`: *用于 [!DNL Amazon Kinesis] 连接。* 您的AmazonKinesis客户所在的Adobe实时CDP将流化您的数据的地区。
* `{EVENT_HUB_NAME}`: *用于 [!DNL Azure Event Hubs] 连接。* 填写Adobe [!DNL Azure Event Hub] 实时CDP将流化您的数据的名称。 有关详细信息，请 [参阅文档中的](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) “创建事件 [!DNL Microsoft] 中心”。

**响应**

成功的响应会返回新创建的目标`id`连接到流目标的唯一标识符()。 按照后续步骤中的要求存储此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 创建数据流

![目标步骤概述步骤4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

现在，使用您在前面的步骤中获得的ID，您可以在Experience Platform数据和要激活数据的目标之间创建数据流。 将此步骤想象为构建Experience Platform和目标之间的管道，数据随后将通过管道流动。

要创建POST流，请执行如下所示的数据请求，同时在有效负荷中提供以下所述的值。

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

* `{FLOW_SPEC_ID}`:基于用户档案的目标的流规范ID是 `71471eba-b620-49e4-90fd-23f1fa0174d8`。 在调用中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用在步骤Connect中获得的源连接 [ID连接到Experience Platform](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在步骤Connect中获得的目标连 [接ID到流目标](#connect-to-streaming-destination)。

**响应**

成功的响应会返回新`id`创建的数据流的ID()和 `etag`。 记下这两个值。 正如您在下一步中将其激活区段一样。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 将数据激活到新目标 {#activate-data}

![目标步骤概述步骤5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

创建了所有连接和数据流后，您现在可以将用户档案数据激活到流平台。 在此步骤中，您可以选择要发送到目标的区段和用户档案属性，还可以计划数据并将数据发送到目标。

要将区段激活到新目标，您必须执行JSONPATCH操作，如下例所示。 您可以在一次调用中激活多个段和用户档案属性。 要进一步了解JSONPATCH，请参 [阅RFC规范](https://tools.ietf.org/html/rfc6902)。

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
* `{SEGMENT_ID}`:提供要导出到此目标的区段ID。 要检索要激活的区段的区段ID，请转 **到https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**，在左侧 **[!UICONTROL 导航菜单中选择Segmentation Service]** API，然后在“区段定义” `GET /segment/definitions` 中查找 **[!UICONTROL 操作]**。
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或 `person.lastName`

**响应**

查找202 OK响应。 不返回响应主体。 要验证请求是否正确，请参阅下一步验证数据流。

## 验证数据流

![目标步骤概述第6步](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

作为教程的最后一步，您应验证区段和用户档案属性确实已正确映射到数据流。

要验证此GET，请执行以下验证请求：

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
* `{ETAG}`:使用上一步中的标记。

**响应**

返回的响应应包含在参 `transformations` 数中您在上一步中提交的区段和用户档案属性。 响应中 `transformations` 的示例参数如下所示：

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
> 除了将用户档案激活到新目标中的属 [性和区段外](#activate-data)，以及中导出的数 [!DNL AWS Kinesis] 据还将包 [!DNL Azure Event Hubs] 含有关标识映射的信息。 这表示导出用户档案的标识( [例如](https://docs.adobe.com/content/help/zh-Hans/id-service/using/intro/id-request.html)ECID、移动ID、Google ID、电子邮件地址等)。 请参阅以下示例。

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

## 使用Postman集合连接到流目标  {#collections}

要以更简化的方式连接到本教程中介绍的流目标，您可以使用 [[!DNL Postman]](https://www.postman.com/)。

[!DNL Postman] 是一种工具，可用于进行API调用并管理预定义调用和环境的库。

对于此特定教程，我们包含附 [!DNL Postman] 加到本文的以下集合：

* [!DNL AWS Kinesis] [!DNL Postman] 集合
* [!DNL Azure Event Hubs] [!DNL Postman] 集合

单击 [此处](assets/DestinationPostmanCollection.zip) ，下载集合存档。

每个集合分别包括必需的请求和环境 [!DNL AWS Kinesis]变量， [!DNL Azure Event Hub]以及。

### 如何使用邮递员集合

要使用附加的集合成功连接到目 [!DNL Postman] 标，请执行以下步骤：

* Download and install [!DNL Postman];
* [下载](assets/DestinationPostmanCollection.zip) 、解压附加集合；
* 将收藏集从其相应的文件夹导入邮递员；
* 根据本文的说明填写环境变量；
* 根据本 [!DNL API] 文中的说明，运行来自邮递员的请求。

## 后续步骤

通过本教程，您已成功将实时CDP连接到您的首选流目标之一，并设置到相应目标的数据流。 传出数据现在可用于目标中进行客户分析或您希望执行的任何其他数据操作。 有关更多详细信息，请参阅以下页面：

* [目标概述](../../rtcdp/destinations/destinations-overview.md)
* [目标目录概述](../../rtcdp/destinations/destinations-catalog.md)
