---
title: 使用流服务API创建OracleEloqua基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到OracleEloqua。
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 创建 [!DNL Oracle Eloqua] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Oracle Eloqua] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要深入了解Platform的以下组件：

* [源](../../../../home.md)：Platform允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)：Platform提供对单个进行分区的虚拟沙箱 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Oracle Eloqua] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Oracle Eloqua]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | 的端点 [!DNL Oracle Eloqua]. |
| `username` | 您的用户名 [!DNL Oracle Eloqua] 帐户。 用户名格式必须是 `siteName + \\ + username`，其中 `siteName` 是您用来登录的公司名称 [!DNL Oracle Eloqua] 和 `username` 是您的用户名。 例如，您的登录用户名可以是： `adobe\\emily`. |
| `password` | 与您的对应的密码 [!DNL Oracle Eloqua] 用户名。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID的值 [!DNL Oracle Eloqua] 源固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

有关以下项的身份验证凭据的详细信息： [!DNL Oracle Eloqua]，请参见 [[!DNL Oracle Eloqua] 身份验证指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Oracle Eloqua] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Oracle Eloqua]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 您的名称 [!DNL Oracle Eloqua] 基本连接。 建议您提供描述性名称，因为可以使用此值查找基础连接。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的补充信息。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | 的端点 [!DNL Oracle Eloqua] 服务器。 |
| `auth.params.username` | 包含与您的网站对应的网站名称和用户名的拼接凭据 [!DNL Oracle Eloqua] 帐户。 |
| `auth.params.password` | 与您的密码对应的密码 [!DNL Oracle Eloqua] 帐户。 |
| `connectionSpec.id` | 的连接规范ID的值 [!DNL Oracle Eloqua] 源固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**响应**

成功响应将返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Oracle Eloqua] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将营销自动化数据引入Platform [!DNL Flow Service] API](../../collect/marketing-automation.md)
