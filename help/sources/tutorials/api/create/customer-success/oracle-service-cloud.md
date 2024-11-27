---
keywords: Experience Platform；主页；热门主题；Oracle服务云；oracle服务云
title: 使用流服务API创建Oracle服务云Source连接
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到OracleService Cloud。
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建Oracle服务云源连接

>[!WARNING]
>
>[!DNL Oracle Service Cloud]源将于2025年6月底弃用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为Oracle服务云创建基本连接的步骤。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到Oracle服务云所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到Oracle服务云，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | oracle服务云实例的主机URL。 |
| `username` | 您的OracleService Cloud用户帐户用户名。 |
| `password` | 您的OracleService Cloud帐户的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 oracle服务云的连接规范ID为： `ba5126ec-c9ac-11eb-b8bc-0242ac130003`。 |

有关对Oracle服务云帐户进行身份验证的更多信息，请参阅[[!DNL Oracle] 身份验证指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供POST服务云身份验证凭据作为请求参数的一部分时，向`/connections`端点发出Oracle请求。

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
| `auth.params.host` | oracle服务云实例的主机URL。 |
| `auth.params.username` | 与您的Oracle服务云帐户关联的用户名。 |
| `auth.params.password` | 与您的OracleService Cloud帐户关联的密码。 |
| `connectionSpec.id` | oracle服务云连接规范ID： `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**响应**

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了Oracle服务云基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将客户成功数据引入Platform](../../collect/customer-success.md)
