---
keywords: Experience Platform；主页；热门主题；Oracle对象存储；oracle对象存储
solution: Experience Platform
title: 使用流服务API创建Oracle对象存储库连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Oracle对象存储。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 创建 [!DNL Oracle Object Storage] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Oracle Object Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Oracle Object Storage] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接到 [!DNL Oracle Object Storage]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 此 [!DNL Oracle Object Storage] 身份验证所需的端点。 终结点格式为： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 此 [!DNL Oracle Object Storage] 身份验证所需的访问密钥ID。 |
| `secretKey` | 此 [!DNL Oracle Object Storage] 身份验证所需的密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的分段名称。 存储段名称的长度必须介于3到63个字符之间，必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不能类似于IP地址。 |
| `folderPath` | 如果用户访问受限，则需要允许的文件夹路径。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Oracle Object Storage] 为： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

有关如何获取这些值的详细信息，请参阅 [《Oracle对象存储验证指南》](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Oracle Object Storage] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Oracle Object Storage]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUrl` | 此 [!DNL Oracle Object Storage] 身份验证所需的端点。 |
| `auth.params.accessKey` | 此 [!DNL Oracle Object Storage] 身份验证所需的访问密钥ID。 |
| `auth.params.secretKey` | 此 [!DNL Oracle Object Storage] 身份验证所需的密码。 |
| `auth.params.bucketName` | 如果用户具有受限访问权限，则需要允许的分段名称。 |
| `auth.params.folderPath` | 如果用户访问受限，则需要允许的文件夹路径。 |
| `connectionSpec.id` | 此 [!DNL Oracle Object Storage] 连接规范ID： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**响应**

成功响应将返回新创建的连接的连接ID。 在下一个教程中，需要此ID来浏览您的云存储数据。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Oracle Object Storage] 连接使用 [!DNL Flow Service] API中，并且已获得其唯一连接ID。 您可以使用此连接ID来 [使用流服务API浏览云存储](../../explore/cloud-storage.md).
