---
keywords: Experience Platform；主页；热门主题；Azure;Azure文件存储；Azure文件存储
solution: Experience Platform
title: 使用流服务API创建Azure文件存储库连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将Azure文件存储连接到Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 创建 [!DNL Azure File Storage] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Azure File Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Azure File Storage]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的端点 [!DNL Azure File Storag]您正在访问的实例。 |
| `userId` | 具有足够访问权限的用户 [!DNL Azure File Storage] 端点。 |
| `password` | 您的密码 [!DNL Azure File Storage] 实例 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Azure File Storage] 为： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

有关入门的更多信息，请参阅 [此Azure文件存储文档](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Azure File Storage] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的端点 [!DNL Azure File Storage] 您正在访问的实例…… |
| `auth.params.userId` | 具有足够访问权限的用户 [!DNL Azure File Storage] 端点。 |
| `auth.params.password` | 的 [!DNL Azure File Storage] 访问密钥。 |
| `connectionSpec.id` | 的 [!DNL Azure File Storage] 连接规范ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API，并已获取连接的唯一ID值。 在下一个教程中，您可以使用此ID来了解如何 [使用流量服务API探索第三方云存储](../../explore/cloud-storage.md).
