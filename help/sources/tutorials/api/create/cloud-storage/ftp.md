---
keywords: Experience Platform；主页；热门主题；文件传输协议；文件传输协议
solution: Experience Platform
title: 使用流服务API创建FTP连接器
topic: overview
type: Tutorial
description: 本教程使用流服务API指导您完成将Experience Platform连接到FTP（文件传输协议）服务器的步骤。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API创建FTP连接器

>[!NOTE]
>
>FTP连接器处于测试状态。 功能和文档可能会发生更改。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到FTP（文件传输协议）服务器的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到FTP服务器时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]连接到FTP，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的FTP服务器关联的名称或IP地址。 |
| `username` | 有权访问FTP服务器的用户名。 |
| `password` | FTP服务器的密码。 |

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个FTP帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

### 使用基本身份验证创建FTP连接

要使用基本身份验证创建FTP连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`host`、`userName`和`password`提供值。

**API格式**

```http
POST /connections
```

**请求**

要创建FTP连接，其唯一连接规范ID必须作为POST请求的一部分提供。 FTP的连接规范ID为`fb2e94c9-c031-467d-8103-6bd6e0a432f2`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | FTP服务器的主机名。 |
| `auth.params.username` | 与您的FTP服务器关联的用户名。 |
| `auth.params.password` | 与FTP服务器关联的密码。 |
| `connectionSpec.id` | FTP服务器连接规范ID:`fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**响应**

成功的响应会返回新创建的连接的唯一标识符(`id`)。 在下一个教程中浏览您的FTP服务器需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了FTP连接，并获得了该连接的唯一ID值。 您可以使用此连接ID来[使用流服务API](../../explore/cloud-storage.md)或[使用流服务API](../../cloud-storage-parquet.md)采集拼花存储。
