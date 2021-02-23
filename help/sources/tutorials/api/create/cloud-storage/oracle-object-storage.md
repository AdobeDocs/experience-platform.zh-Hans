---
keywords: Experience Platform；主页；热门主题；Oracle对象存储;oracle对象存储
solution: Experience Platform
title: 使用流服务API创建Oracle对象存储源连接
topic: 概述
type: 教程
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Oracle对象存储。
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API创建[!DNL Oracle Object Storage]源连接

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)指导您完成将Adobe Experience Platform连接到[!DNL Oracle Object Storage]的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到[!DNL Oracle Object Storage]所需的其他信息。

### 收集所需凭据

要使[!DNL Flow Service]连接到[!DNL Oracle Object Storage]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]端点。 端点格式为：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的存储段名称。 存储段名称必须长度在3到63个字符之间，必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不能与IP地址相同。 |
| `folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |

有关如何获取这些值的详细信息，请参阅[Oracle对象存储身份验证指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用平台API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL Oracle Object Storage]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Oracle Object Storage]连接，必须在POST请求中提供其唯一连接规范ID。 [!DNL Oracle Object Storage]的连接规范ID为`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]端点。 |
| `auth.params.accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `auth.params.secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `auth.params.bucketName` | 如果用户具有受限访问权限，则需要允许的存储段名称。 |
| `auth.params.folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |
| `connectionSpec.id` | [!DNL Oracle Object Storage]连接规范ID:`c85f9425-fb21-426c-ad0b-405e9bd8a46c`。 |

**响应**

成功的响应返回新创建的连接的连接ID。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了[!DNL Oracle Object Storage]连接，并获得了其唯一连接ID。 您可以使用此连接ID来使用流服务API](../../explore/cloud-storage.md)浏览云存储。[