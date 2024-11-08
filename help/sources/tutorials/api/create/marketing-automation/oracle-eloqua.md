---
title: 使用流服务API创建OracleEloqua基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到OracleEloqua。
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Oracle Eloqua]基本连接

>[!WARNING]
>
>[!DNL Oracle Eloqua]源将于2025年5月底弃用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Oracle Eloqua]创建基本连接的步骤。

## 开始使用

本指南要求您对Platform的以下组件有一定的了解：

* [源](../../../../home.md)：平台允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Platform提供了将单个[!DNL Platform]实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Oracle Eloqua]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Oracle Eloqua]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | [!DNL Oracle Eloqua]的端点。 |
| `username` | [!DNL Oracle Eloqua]帐户的用户名。 用户名必须设置为`siteName + \\ + username`格式，其中`siteName`是您用于登录到[!DNL Oracle Eloqua]的公司名称，`username`是您的用户名。 例如，您的登录用户名可以是： `adobe\\emily`。 |
| `password` | 与您的[!DNL Oracle Eloqua]用户名对应的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Oracle Eloqua]源的连接规范ID的值固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`。 |

有关[!DNL Oracle Eloqua]的身份验证凭据的详细信息，请参阅有关身份验证](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)的[[!DNL Oracle Eloqua] 指南。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Oracle Eloqua]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Oracle Eloqua]创建基本连接：

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
| `name` | [!DNL Oracle Eloqua]基本连接的名称。 建议您提供一个描述性名称，因为您可以使用此值查找基础连接。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的补充信息。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | [!DNL Oracle Eloqua]服务器的端点。 |
| `auth.params.username` | 包含与您的[!DNL Oracle Eloqua]帐户对应的站点名称和用户名的拼接凭据。 |
| `auth.params.password` | 与您的[!DNL Oracle Eloqua]帐户对应的密码。 |
| `connectionSpec.id` | [!DNL Oracle Eloqua]源的连接规范ID的值固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Oracle Eloqua]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将营销自动化数据引入平台](../../collect/marketing-automation.md)
