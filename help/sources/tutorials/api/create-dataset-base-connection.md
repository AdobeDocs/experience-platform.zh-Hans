---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Experience Platform数据集基础连接
topic: overview
translation-type: tm+mt
source-git-commit: e409b287d6965ede4030829287bd3e405e9d709b

---


# 使用Flow Service API创建Experience Platform数据集基础连接

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

要将数据从第三方源连接到平台，必须先建立数据集基础连接。

本教程使用Flow Service API指导您完成创建数据集基础连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式注册开发人员指南](../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用所需了解的重要信息。 这包括您 `{TENANT_ID}`的“容器”概念以及发出请求所需的标题（特别注意“接受”标题及其可能的值）。
* [目录服务](../../../catalog/home.md):Catalog是Experience Platform中用于数据位置和世系的记录系统。
* [批量摄取](../../../ingestion/batch-ingestion/overview.md):批处理摄取API允许您将数据作为批处理文件摄取到Experience Platform中。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到数据湖。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于Flow Service的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 查找连接规范

创建数据集基础连接的第一步是从Flow Service中检索一组连接规范。

**API格式**

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 您可以通过执行GET请求和使用查询参数来查找数据集基础连接的连接规范。

发送不带查询参数的GET请求将返回所有可用源的连接规范。 您可以包含查询以 `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` 获取数据集基础连接的信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**请求**

以下请求检索数据集基本连接的连接规范。

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

基本连接指定一个源并包含该源的凭据。 只需一个数据集基本连接，因为它可用于创建多个源连接器以导入不同的数据。

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
| `connectionSpec.id` | 在上一步 `id` 中检索的连接规范。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 需要此ID才能创建目标连接并从第三方源连接器获取数据。

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了数据集基连接，并获得了连接的唯一ID值。 您可以使用此基本连接创建目标连接。 以下教程将逐步介绍创建目标连接的步骤，具体取决于您所使用的源连接器的类别:

* [云存储](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [客户成功](./collect/customer-success.md)
* [数据库](./collect/database-nosql.md)