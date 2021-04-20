---
keywords: Experience Platform；主页；热门主题；流服务；删除帐户；删除；api
solution: Experience Platform
title: 使用流服务API删除帐户
topic: overview
type: Tutorial
description: 了解如何使用流服务API删除帐户。
translation-type: tm+mt
source-git-commit: 37be5f5ffa4640d7d4442a24cc257069237f15cb
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---


# 使用流服务API删除帐户

Adobe Experience Platform允许从外部源摄取数据，同时为您提供使用[!DNL Platform]服务构建、标记和增强传入数据的能力。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程介绍了使用[[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)进行删除的步骤。

## 入门指南

本教程要求您具有有效的连接ID。 如果您没有有效的连接ID，请从[源概述](../../home.md)中选择您选择的连接器，然后按照尝试本教程之前概述的步骤操作。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功删除连接时需要了解的其他信息。

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

## 查找连接详细信息

>[!NOTE]
>本教程以[Azure Blob源连接器](../../connectors/cloud-storage/blob.md)为例，但概述的步骤适用于任何[可用源连接器](../../home.md)。

更新连接信息的第一步是使用连接ID检索连接详细信息。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要检索的连接的唯一`id`值。 |

**请求**

以下内容会检索有关您的连接ID的信息。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回连接的当前详细信息，包括其凭据、唯一标识符(`id`)和版本。

```json
{
    "items": [
        {
            "createdAt": 1603514659165,
            "updatedAt": 1603514659165,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "dd3631cd-d0ea-4fea-b631-cdd0ea6fea21",
            "name": "Test Azure Blob Connector",
            "description": "A test connector for Azure Blob",
            "connectionSpec": {
                "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "ConnectionString",
                "params": {
                    "connectionString": "xxxx"
                }
            },
            "version": "\"07001eed-0000-0200-0000-5f93b1250000\"",
            "etag": "\"07001eed-0000-0200-0000-5f93b1250000\""
        }
    ]
}
```

## 删除连接

在您有现有连接ID后，对[!DNL Flow Service] API执行DELETE请求。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要删除的连接的唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对连接进行查找(GET)请求来确认删除。

## 后续步骤

通过本教程，您已成功使用[!DNL Flow Service] API删除现有帐户。

有关如何使用用户界面执行这些操作的步骤，请参阅有关在UI](../../tutorials/ui/delete-accounts.md)中删除帐户的教程[
