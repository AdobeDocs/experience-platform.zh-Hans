---
keywords: Experience Platform；主页；热门主题；数据集连接流服务；流服务；流服务连接
solution: Experience Platform
title: 使用Flow Service API创建Adobe Experience Platform数据集基础连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API创建到Adobe Experience Platform的数据集基础连接。
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Experience Platform]数据集基础连接

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

要将数据从第三方源连接到[!DNL Platform]，必须先建立数据集基础连接。

本教程使用[!DNL Flow Service] API指导您完成创建数据集基础连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成的基础](../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式 Registry开发人员指南](../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用所需了解的重要信息。这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（特别要注意“接受”标头及其可能的值）。
* [目录服务](../../../catalog/home.md):目录是数据位置和谱系的记录系 [!DNL Experience Platform]统。
* [批量摄取](../../../ingestion/batch-ingestion/overview.md):批处理摄取API允许您将数据作为批处理文件摄取到Experience Platform中。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到数据湖所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 查找连接规范

创建数据集基础连接的第一步是从[!DNL Flow Service]中检索一组连接规范。

**API格式**

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求和使用查询参数来查找数据集基础连接的连接规范。

发送不带GET参数的查询请求将返回所有可用源的连接规范。 您可以包含查询`property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"`以获取数据集基础连接的信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**请求**

以下请求检索数据集基础连接的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回创建基本连接所需的连接规范和唯一标识符(`id`)。

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 创建数据集基础连接

基本连接指定源并包含该源的凭据。 只需要一个数据集基础连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `connectionSpec.id` | 在上一步中检索到的连接规范`id`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 需要此ID才能创建目标连接并从第三方源连接器收集数据。

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了一个数据集基础连接，并获得了该连接的唯一ID值。 您可以使用此基本连接创建目标连接。 以下教程将逐步介绍创建目标连接的步骤，具体取决于您所使用的源连接器的类别:

* [云存储](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [客户成功](./collect/customer-success.md)
* [数据库](./collect/database-nosql.md)
