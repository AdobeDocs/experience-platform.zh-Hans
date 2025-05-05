---
keywords: Experience Platform；主页；热门主题；Oracle对象存储；oracle对象存储
solution: Experience Platform
title: 使用流服务API创建Oracle对象存储基础连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Oracle对象存储。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Oracle Object Storage]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Oracle Object Storage]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Oracle Object Storage]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL Oracle Object Storage]，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]终结点。 终结点格式为： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的分段名称。 存储段名称的长度必须介于3到63个字符之间，必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不得类似于IP地址。 |
| `folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Oracle Object Storage]的连接规范ID为： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

有关如何获取这些值的详细信息，请参阅[Oracle Object Storage身份验证指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Oracle Object Storage]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Oracle Object Storage]创建基本连接：

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
| `auth.params.serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]终结点。 |
| `auth.params.accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `auth.params.secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `auth.params.bucketName` | 如果用户具有受限访问权限，则需要允许的分段名称。 |
| `auth.params.folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |
| `connectionSpec.id` | [!DNL Oracle Object Storage]连接规范ID： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

**响应**

成功的响应将返回新创建的连接的连接ID。 需要在下一个教程中探究您的云存储数据时使用此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Oracle Object Storage]连接，并获得了其唯一的连接ID。 您可以使用此连接ID以使用流服务API[&#128279;](../../explore/cloud-storage.md)来浏览云存储。
