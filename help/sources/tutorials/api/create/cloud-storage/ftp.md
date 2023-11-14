---
keywords: Experience Platform；主页；热门主题；文件传输协议；文件传输协议
solution: Experience Platform
title: 使用流服务API创建FTP基本连接
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到FTP（文件传输协议）服务器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 4%

---

# 使用创建基于FTP的连接 [!DNL Flow Service] API

>[!NOTE]
>
>FTP连接器处于测试阶段。 功能和文档可能会发生更改。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL FTP] （文件传输协议）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接到 [!DNL FTP] 服务器使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接到 [!DNL FTP]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的关联的名称或IP地址 [!DNL FTP] 服务器。 |
| `username` | 对您的具有访问权限的用户名 [!DNL FTP] 服务器。 |
| `password` | 您的密码 [!DNL FTP] 服务器。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL FTP] 为： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL FTP] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL FTP]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.password` | 与您的FTP服务器关联的密码。 |
| `connectionSpec.id` | FTP服务器连接规范ID： `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**响应**

成功的响应将返回唯一标识符(`id`)。 请在下一教程中探究您的FTP服务器时需要使用此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

在本教程之后，您已使用创建了一个FTP连接 [!DNL Flow Service] API中，并获取了连接的唯一ID值。 您可以使用此连接ID来 [使用流服务API浏览云存储](../../explore/cloud-storage.md).
