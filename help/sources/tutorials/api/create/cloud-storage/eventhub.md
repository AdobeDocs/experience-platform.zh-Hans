---
keywords: Experience Platform；主页；热门主题；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流服务API创建Azure事件集线器源连接
topic: 概述
type: 教程
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure事件中心帐户。
translation-type: tm+mt
source-git-commit: 643da0981b3c955a9f66b6542ddaf2bda7398a2e
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API创建[!DNL Azure Event Hubs]源连接

>[!NOTE]
>
> [!DNL Azure Event Hubs]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL Azure Event Hubs]帐户的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

- [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
- [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到[!DNL Azure Event Hubs]帐户所需了解的其他信息。

### 收集所需凭据

要使[!DNL Flow Service]与您的[!DNL Azure Event Hubs]帐户连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 生成的共享访问签名。 |
| `namespace` | 您访问的事件中心的命名空间。 |
| `connectionSpec.id` | [!DNL Azure Event Hubs]连接规范ID:`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

有关这些值的详细信息，请参阅[此事件集线器文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL Azure Event Hubs]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

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
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `auth.params.sasKey` | 生成的共享访问签名。 |
| `namespace` | 您访问的[!DNL Event Hubs]的命名空间。 |
| `connectionSpec.id` | [!DNL Azure Event Hubs]连接规范ID:`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了[!DNL Azure Event Hubs]连接，并获取了作为响应体一部分的唯一ID。 您可以使用此连接ID来使用流服务API](../../collect/streaming.md)收集流数据。[