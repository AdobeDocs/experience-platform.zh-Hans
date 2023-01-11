---
keywords: Experience Platform；主页；热门主题；文件传输协议；文件传输协议
solution: Experience Platform
title: 使用流服务API创建FTP基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到FTP（文件传输协议）服务器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用创建FTP基本连接 [!DNL Flow Service] API

>[!NOTE]
>
>FTP连接器处于测试阶段。 功能和文档可能会发生更改。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL FTP] （文件传输协议）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到 [!DNL FTP] 服务器使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接到 [!DNL FTP]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的 [!DNL FTP] 服务器。 |
| `username` | 有权访问您的 [!DNL FTP] 服务器。 |
| `password` | 您的密码 [!DNL FTP] 服务器。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL FTP] 为： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL FTP] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL FTP]:

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
| `auth.params.username` | 与FTP服务器关联的用户名。 |
| `auth.params.password` | 与FTP服务器关联的密码。 |
| `connectionSpec.id` | FTP服务器连接规范ID: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**响应**

成功的响应会返回唯一标识符(`id`)。 在下一个教程中浏览FTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过阅读本教程，您已使用 [!DNL Flow Service] API，并且已获取连接的唯一ID值。 您可以将此连接ID用于 [使用流量服务API浏览云存储](../../explore/cloud-storage.md).
