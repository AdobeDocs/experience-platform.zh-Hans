---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 连接到电子邮件营销目标，并使用API调用激活数据
description: 本文档包括通过使用Adobe Experience Platform API创建电子邮件营销目标
topic: 教程
type: 教程
translation-type: tm+mt
source-git-commit: 789534c02746ed24dfa01c7b471cdf3be407711e
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 1%

---


# 连接到电子邮件营销目标，并使用API调用激活数据

本教程演示了如何使用API调用连接到Adobe Experience Platform数据、创建[电子邮件营销目标](../catalog/email-marketing/overview.md)、创建到新创建目标的数据流以及将数据激活到新创建的目标。

本教程在所有示例中使用Adobe Campaign目标，但所有电子邮件营销目标的步骤相同。

![概述 — 创建目标和激活区段的步骤](../assets/api/email-marketing/overview.png)

如果您希望使用平台中的用户界面连接目标并激活数据，请参阅[连接目标](../ui/connect-destination.md)和[将用户档案和区段激活到目标](../ui/activate-destinations.md)教程。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 是数据位置和谱系的记录系 [!DNL Experience Platform]统。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的更多信息，以便在平台中将数据激活到电子邮件营销目标。

### 收集所需凭据

要完成本教程中的步骤，您应准备好以下凭据，具体取决于要连接和激活区段的目标类型。

* 对于[!DNL Amazon] S3到电子邮件营销平台的连接：`accessId`, `secretKey`
* 对于与电子邮件营销平台的SFTP连接：`domain`、`port`、`username`、`password`或`ssh key`（取决于到FTP位置的连接方法）

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集必需和可选标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* 授权：承载`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的资源可隔离到特定虚拟沙箱。 在向[!DNL Platform] API发出的请求中，您可以指定操作将在中进行的沙箱的名称和ID。 这些是可选参数。

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

### Swagger文档

您可以在Swagger的本教程中找到所有API调用的随附参考文档。 请参阅Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)上的[流服务API文档。 我们建议您同时使用本教程和Swagger文档页。

## 获取可用目标{#get-the-list-of-available-destinations}的列表

![目标步骤概述步骤1](../assets/api/email-marketing/step1.png)

作为第一步，您应确定要将数据激活到的电子邮件营销目标。 首先，请发出呼叫，请求列表可连接和激活区段的可用目标。 对`connectionSpecs`端点执行以下GET请求，以返回可用目标的列表:

**API格式**

```http
GET /connectionSpecs
```

**请求**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**响应**

成功的响应包含可用目标及其唯一标识符的列表(`id`)。 存储您计划使用的目标的值，因为在后续步骤中需要它。 例如，如果要将区段连接并传送到Adobe Campaign，请在响应中查找以下代码片断：

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## 连接到[!DNL Experience Platform]数据{#connect-to-your-experience-platform-data}

![目标步骤概述步骤2](../assets/api/email-marketing/step2.png)

接下来，您必须连接到[!DNL Experience Platform]数据，以便导出用户档案数据并在首选目标中激活它。 这包括两个子步骤，如下所述。

1. 首先，必须通过设置基本连接来执行对[!DNL Experience Platform]中的数据授权访问的调用。
2. 然后，使用基连接ID，您将进行另一次调用，在其中创建源连接，该连接将建立与[!DNL Experience Platform]数据的连接。


### 授权访问[!DNL Experience Platform]中的数据

**API格式**

```http
POST /connections
```

**请求**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

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

### 连接到[!DNL Experience Platform]数据{#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**请求**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

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
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上一步中获得的ID。
* `{CONNECTION_SPEC_ID}`:使用连接规范ID  [!DNL Unified Profile Service] -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`。

**响应**

成功的响应返回新创建的源连接到[!DNL Unified Profile Service]的唯一标识符(`id`)。 这将确认您已成功连接到[!DNL Experience Platform]数据。 在后续步骤中存储所需的值。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 连接到电子邮件营销目标{#connect-to-email-marketing-destination}

![目标步骤概述步骤3](../assets/api/email-marketing/step3.png)

在此步骤中，您将设置到所需电子邮件营销目标的连接。 这包括两个子步骤，如下所述。

1. 首先，您必须通过设置基本连接来执行呼叫以授权访问电子邮件服务提供商。
2. 然后，使用基本连接ID，您将进行另一次调用，在其中创建目标连接，该连接指定存储帐户中要传送导出数据的位置，以及将导出的数据的格式。

### 授权访问电子邮件营销目标

**API格式**

```http
POST /connections
```

**请求**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`:使用您在获取可用目标的列表步骤 [中获得的连接规范ID](#get-the-list-of-available-destinations)。
* `{S3 or SFTP}`:为此目标填写所需的连接类型。在[目标目录](../catalog/overview.md)中，滚动到首选目标，查看是否支持S3和/或SFTP连接类型。
* `{ACCESS_ID}`:您的S3存储 [!DNL Amazon] 位置的访问ID。
* `{SECRET_KEY}`:您的S3存储 [!DNL Amazon] 位置的密钥。

**响应**

成功的响应包含基连接的唯一标识符(`id`)。 在下一步创建目标连接时，按需要存储此值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 指定存储位置和数据格式

[!DNL Adobe Experience Platform] 以文件形式导出电子邮件营销和云存储目 [!DNL CSV] 标的数据

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 以每个文件500万条记录（行）自动拆分导出文件。每行表示一个用户档案。
>
>拆分文件名后面附加一个数字，指示文件是较大导出的一部分，如下所示：`filename.csv`、`filename_2.csv`、`filename_3.csv`。

**API格式**

```http
POST /targetConnections
```

**请求**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`:使用您在上述步骤中获得的基本连接ID。
* `{CONNECTION_SPEC_ID}`:使用您在步骤获取可用目标 [的列表中获得的连接规范](#get-the-list-of-available-destinations)。
* `{BUCKETNAME}`:您 [!DNL Amazon] 的S3存储段，平台将存放数据导出。
* `{FILEPATH}`:S3存储桶目 [!DNL Amazon] 录中的路径，平台将存放数据导出。

**响应**

成功的响应会返回新创建的目标到电子邮件营销目标的唯一标识符(`id`)。 按照后续步骤中的要求存储此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 创建数据流

![目标步骤概述步骤4](../assets/api/email-marketing/step4.png)

现在，使用您在前面的步骤中获得的ID，您可以在[!DNL Experience Platform]数据与要激活数据的目标之间创建数据流。 将此步骤想象为在[!DNL Experience Platform]和所需目标之间构建数据稍后将通过的管道。

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`:使用要连接到的电子邮件营销目标的流程。要获取流规范，请对`flowspecs`端点执行GET操作。 请参阅此处的Swagger文档：https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs。 在响应中，查找`upsTo`并复制要连接到的电子邮件营销目标的相应ID。 例如，对于Adobe Campaign，请查找`upsToCampaign`并复制`id`参数。
* `{SOURCE_CONNECTION_ID}`:使用在步骤连接到Experience Platform中获 [得的源连接ID](#connect-to-your-experience-platform-data)。
* `{TARGET_CONNECTION_ID}`:使用您在连接到电子邮件营销目标的 [步骤中获得的目标连接ID](#connect-to-email-marketing-destination)。

**响应**

成功的响应返回新创建的数据流的ID(`id`)和`etag`。 记下这两个值。 正如您在下一步中所做的那样，激活区段。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 将数据激活到新目标

![目标步骤概述步骤5](../assets/api/email-marketing/step5.png)

创建了所有连接和数据流后，现在您可以将用户档案数据激活到电子邮件营销平台。 在此步骤中，您可以选择要发送到目标的区段和用户档案属性，并可以计划和将数据发送到目标。

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
* `{PROFILE_ATTRIBUTE}`:例如，  `"person.lastName"`

**响应**

查找202 OK响应。 不返回响应正文。 要验证请求是否正确，请参阅下一步验证数据流。

## 验证数据流

![目标步骤概述步骤6](../assets/api/email-marketing/step6.png)

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
                "selectors": []
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

## 后续步骤

通过本教程，您已成功将平台连接到您的首选电子邮件营销目标之一，并将数据流设置到相应的目标。 传出数据现在可用于电子邮件活动、目标广告和许多其他用例的目标。 有关更多详细信息，请参阅以下页面：

* [目标概述](../home.md)
* [目标目录概述](../catalog/overview.md)