---
keywords: Experience Platform；主页；热门主题；API教程；流目标API;平台
solution: Experience Platform
title: 在Adobe Experience Platform中使用流服务API连接到流目标并激活数据
description: 本文档介绍了如何使用Adobe Experience Platform API创建流目标
topic-legacy: tutorial
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2049'
ht-degree: 1%

---

# 使用流服务API连接到流目标并激活数据

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions).
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
>
>阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

本教程演示了如何使用API调用连接到Adobe Experience Platform数据，创建与云存储流目标([AmazonKinesis](../catalog/cloud-storage/amazon-kinesis.md) 或 [Azure事件中心](../catalog/cloud-storage/azure-event-hubs.md))，创建数据流到新创建的目标，然后将数据激活到新创建的目标。

本教程使用 [!DNL Amazon Kinesis] 目标，但步骤与 [!DNL Azure Event Hubs].

![概述 — 创建流目标和激活区段的步骤](../assets/api/streaming-destination/overview.png)

如果您希望使用平台中的用户界面连接到目标并激活数据，请参阅 [连接目标](../ui/connect-destination.md) 和 [将受众数据激活到流区段导出目标](../ui/activate-segment-streaming-destinations.md) 教程。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是Experience Platform中数据位置和谱系的记录系统。
* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了在平台中激活数据到流目标的需要了解的其他信息。

### 收集所需的凭据

要完成本教程中的步骤，您应准备好以下凭据，具体取决于您连接和激活区段的目标类型。

* 对于 [!DNL Amazon Kinesis] 连接： `accessKeyId`, `secretKey`, `region` 或 `connectionUrl`
* 对于 [!DNL Azure Event Hubs] 连接： `sasKeyName`, `sasKey`, `namespace`

### 读取示例API调用 {#reading-sample-api-calls}

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

### 收集必需和可选标题的值 {#gather-values}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的资源可以与特定虚拟沙箱隔离。 在对Platform API的请求中，您可以指定操作将在其中进行的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

### Swagger文档 {#swagger-docs}

在本教程中，您可以在Swagger中找到所有API调用的随附参考文档。 请参阅 [关于流量服务API的文档Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). 我们建议您同时使用本教程和Swagger文档页面。

## 获取可用流目标列表 {#get-the-list-of-available-streaming-destinations}

![目标步骤概述第1步](../assets/api/streaming-destination/step1.png)

作为第一步，您应该确定要激活数据的流目标。 首先，执行调用以请求可连接和激活区段的可用目标列表。 对执行以下GET请求 `connectionSpecs` 用于返回可用目标列表的端点：

**API格式**

```http
GET /connectionSpecs
```

**请求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**响应**

成功的响应包含可用目标及其唯一标识符的列表(`id`)。 存储您计划使用的目标值，因为在后续步骤中需要该值。 例如，如果您要将区段连接并交付到 [!DNL Amazon Kinesis] 或 [!DNL Azure Event Hubs]，在响应中查找以下代码片段：

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

![目标步骤概述第2步](../assets/api/streaming-destination/step2.png)

接下来，您必须连接到Experience Platform数据，以便导出配置文件数据并在首选目标中激活该数据。 这包括两个子步骤，如下所述。

1. 首先，您必须通过设置基本连接来执行调用，以授权对Experience Platform中的数据的访问。
2. 然后，使用基本连接ID，您将再次进行调用，在该调用中创建源连接，以建立与Experience Platform数据的连接。


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
--header 'x-gw-ims-org-id: {ORG_ID}' \
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


* `{CONNECTION_SPEC_ID}`:使用配置文件服务的连接规范ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**响应**

成功的响应包含基本连接的唯一标识符(`id`)。 在创建源连接的下一步中根据需要存储此值。

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
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上一步中获取的ID。
* `{CONNECTION_SPEC_ID}`:使用配置文件服务的连接规范ID - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**响应**

成功的响应会返回唯一标识符(`id`)用于新创建的与配置文件服务的源连接。 这表示您已成功连接到Experience Platform数据。 在后续步骤中根据需要存储此值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 连接到流目标 {#connect-to-streaming-destination}

![目标步骤概述第3步](../assets/api/streaming-destination/step3.png)

在此步骤中，您将设置到所需流目标的连接。 这包括两个子步骤，如下所述。

1. 首先，您必须通过设置基本连接来执行调用以授权对流目标的访问。
2. 然后，使用基本连接ID，您将再次调用，以在其中创建目标连接，该连接指定将传送导出数据的存储帐户位置以及将导出的数据格式。

### 授权对流目标的访问

**API格式**

```http
POST /connections
```

**请求**

>[!IMPORTANT]
>
>以下示例包含前缀为的代码注释 `//`. 这些注释会突出显示不同流目标必须使用不同值的位置。 请在使用代码片段之前删除注释。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

* `{CONNECTION_SPEC_ID}`:使用您在步骤中获得的连接规范ID [获取可用目标列表](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`:填写流目标的名称： `Aws Kinesis authentication credentials` 或 `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *对于 [!DNL Amazon Kinesis] 连接。* 您的Amazon Kinesis存储位置的访问ID。
* `{SECRET_KEY}`: *对于 [!DNL Amazon Kinesis] 连接。* 您的Amazon Kinesis存储位置的密钥。
* `{REGION}`: *对于 [!DNL Amazon Kinesis] 连接。* 您的 [!DNL Amazon Kinesis] 帐户Platform将在其中传输您的数据。
* `{SAS_KEY_NAME}`: *对于 [!DNL Azure Event Hubs] 连接。* 填写SAS密钥名称。 了解如何验证 [!DNL Azure Event Hubs] 在 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *对于 [!DNL Azure Event Hubs] 连接。* 填写SAS密钥。 了解如何验证 [!DNL Azure Event Hubs] 在 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *对于 [!DNL Azure Event Hubs] 连接。* 填写 [!DNL Azure Event Hubs] Platform将在其中流数据的命名空间。 有关更多信息，请参阅 [创建事件中心命名空间](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) 在 [!DNL Microsoft] 文档。

**响应**

成功的响应包含基本连接的唯一标识符(`id`)。 在创建目标连接的下一步中根据需要存储此值。

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
>以下示例包含前缀为的代码注释 `//`. 这些注释会突出显示不同流目标必须使用不同值的位置。 请在使用代码片段之前删除注释。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
* `{CONNECTION_SPEC_ID}`:使用您在步骤中获得的连接规范 [获取可用目标列表](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *对于 [!DNL Amazon Kinesis] 连接。* 在 [!DNL Amazon Kinesis] 帐户。 平台会将数据导出到此流。
* `{REGION}`: *对于 [!DNL Amazon Kinesis] 连接。* Amazon Kinesis帐户中Platform将在其中传输您数据的区域。
* `{EVENT_HUB_NAME}`: *对于 [!DNL Azure Event Hubs] 连接。* 填写 [!DNL Azure Event Hub] Platform将在其中传输数据的名称。 有关更多信息，请参阅 [创建事件中心](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) 在 [!DNL Microsoft] 文档。

**响应**

成功的响应会返回唯一标识符(`id`)来连接流目标。 按照后续步骤中的要求存储此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 创建数据流

![目标步骤概述第4步](../assets/api/streaming-destination/step4.png)

现在，使用您在上面步骤中获取的ID，您可以在Experience Platform数据与要将数据激活到的目标之间创建数据流。 将此步骤视为构建Experience Platform与所需目标之间的管道，数据稍后将通过管道流动。

要创建数据流，请执行如下所示的POST请求，同时在负载中提供以下所述的值。

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
-H 'x-gw-ims-org-id: {ORG_ID}' \
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

* `{FLOW_SPEC_ID}`:基于用户档案的目标的流量规范ID是 `71471eba-b620-49e4-90fd-23f1fa0174d8`. 在调用中使用此值。
* `{SOURCE_CONNECTION_ID}`:使用您在步骤中获取的源连接ID [连接到Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`:使用您在步骤中获取的目标连接ID [连接到流目标](#connect-to-streaming-destination).

**响应**

成功的响应会返回ID(`id`)和 `etag`. 请记下这两个值。 正如您在下一步中所做的那样，激活区段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 将数据激活到新目标 {#activate-data}

![目标步骤概述步骤5](../assets/api/streaming-destination/step5.png)

创建了所有连接和数据流后，现在您可以将配置文件数据激活到流平台。 在此步骤中，您可以选择要发送到目标的区段和配置文件属性，并可以安排数据发送到目标。

要将区段激活到新目标，您必须执行JSONPATCH操作，如下例所示。 您可以在一次调用中激活多个区段和配置文件属性。 要了解有关JSONPATCH的更多信息，请参阅 [RFC规范](https://tools.ietf.org/html/rfc6902).

**API格式**

```http
PATCH /flows
```

**请求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

* `{DATAFLOW_ID}`:使用在上一步中获取的数据流。
* `{ETAG}`:使用您在上一步中获取的标记。
* `{SEGMENT_ID}`:提供要导出到此目标的区段ID。 要检索要激活的区段的区段ID，请转到 **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**，选择 **[!UICONTROL 分段服务API]** ，然后在左侧导航菜单中查找 `GET /segment/definitions` 操作 **[!UICONTROL 区段定义]**.
* `{PROFILE_ATTRIBUTE}`:例如， `personalEmail.address` 或 `person.lastName`

**响应**

查找202 OK响应。 未返回响应主体。 要验证请求是否正确，请参阅下一步验证数据流。

## 验证数据流

![目标步骤概述步骤6](../assets/api/streaming-destination/step6.png)

在教程的最后一步中，您应该验证区段和配置文件属性是否确实已正确映射到数据流。

要验证此请求，请执行以下GET请求：

**API格式**

```http
GET /flows
```

**请求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`:使用上一步中的数据流。
* `{ETAG}`:使用上一步中的标记。

**响应**

返回的响应应包括在 `transformations` 参数您在上一步中提交的区段和配置文件属性。 示例 `transformations` 响应中的参数可能如下所示：

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
> 除了步骤中的用户档案属性和区段之外， [将数据激活到新目标](#activate-data)，中的导出数据 [!DNL AWS Kinesis] 和 [!DNL Azure Event Hubs] 还将包含有关身份映射的信息。 这表示导出的用户档案的标识(例如 [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html)、移动设备ID、Google ID、电子邮件地址等)。 请参阅下面的示例。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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

要以更简化的方式连接到本教程中描述的流目标，您可以使用 [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] 是一个工具，可用于进行API调用并管理预定义调用和环境的库。

在本特定教程中，请执行以下操作 [!DNL Postman] 收藏集已附加：

* [!DNL AWS Kinesis] [!DNL Postman] 收藏集
* [!DNL Azure Event Hubs] [!DNL Postman] 收藏集

单击 [此处](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 下载收藏集存档。

每个收藏集都包含必需的请求和环境变量， [!DNL AWS Kinesis]和 [!DNL Azure Event Hub]，分别为。

### 如何使用Postman收藏集

使用附加的 [!DNL Postman] 收藏集，请执行以下步骤：

* 下载并安装 [!DNL Postman];
* [下载](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 并解压附带的收藏集；
* 将收藏集从相应的文件夹导入Postman;
* 按照本文中的说明填写环境变量；
* 运行 [!DNL API] 来自Postman的请求（根据本文中的说明）。

## 后续步骤

通过阅读本教程，您已成功将Platform连接到您的其中一个首选流目标，并设置到相应目标的数据流。 传出数据现在可用于客户分析目标或您可能希望执行的任何其他数据操作。 有关更多详细信息，请参阅以下页面：

* [目标概述](../home.md)
* [目标目录概述](../catalog/overview.md)
