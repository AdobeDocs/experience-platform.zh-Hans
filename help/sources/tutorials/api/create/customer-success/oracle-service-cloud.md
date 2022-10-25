---
keywords: Experience Platform；主页；热门主题；Oracle服务云；oracle服务云
title: 使用流服务API创建Oracle服务云源连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Oracle服务云。
source-git-commit: 078a266967cd7b0818f958283a58a8af4c886a21
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# （测试版）使用创建Oracle服务云源连接 [!DNL Flow Service] API

>[!NOTE]
>
>oracle服务云源处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用创建Oracle服务云基本连接的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 要与Oracle服务云连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 您的Oracle服务云实例的主机URL。 |
| `username` | 您的Oracle服务云用户帐户的用户名。 |
| `password` | 您的Oracle服务云帐户的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 oracle服务云的连接规范ID是： `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

有关对Oracle服务云帐户进行身份验证的更多信息，请参阅 [[!DNL Oracle] 认证指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 端点。

**API格式**

```http
POST /connections
```

**请求**

以下请求为Oracle服务云创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 您的Oracle服务云实例的主机URL。 |
| `auth.params.username` | 与您的Oracle服务云帐户关联的用户名。 |
| `auth.params.password` | 与您的Oracle服务云帐户关联的密码。 |
| `connectionSpec.id` | oracle服务云连接规范ID: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过阅读本教程，您已使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/customer-success.md)
