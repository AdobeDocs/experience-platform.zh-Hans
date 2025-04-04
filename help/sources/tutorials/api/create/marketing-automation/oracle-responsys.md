---
keywords: Experience Platform；主页；热门主题；oracle；
title: (Beta)使用流服务API创建Oracle Responsys基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Oracle Responsys。
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# (Beta)使用[!DNL Flow Service] API创建[!DNL Oracle Responsys]基本连接

>[!NOTE]
>
>[!DNL Oracle Responsys]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Oracle Responsys]创建基本连接的步骤。

## 开始使用

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Oracle Responsys]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Oracle Responsys]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | [!DNL Oracle Responsys]实例的REST身份验证终结点URL。 |
| `clientId` | [!DNL Oracle Responsys]实例的客户端ID。 |
| `clientSecret` | [!DNL Oracle Responsys]实例的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Oracle Responsys]源的连接规范ID的值固定为： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`。 |

有关[!DNL Oracle Responsys]的身份验证凭据的详细信息，请参阅有关身份验证](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm)的[[!DNL Oracle Responsys] 指南。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Oracle Responsys]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Oracle Responsys]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | [!DNL Oracle Responsys]基本连接的名称。 建议您提供一个描述性名称，因为您可以使用此值查找基础连接。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的补充信息。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | [!DNL Oracle Responsys]服务器的REST身份验证终结点URL。 |
| `auth.params.clientId` | [!DNL Oracle Responsys]实例的客户端ID。 |
| `auth.params.clientSecret` | [!DNL Oracle Responsys]实例的客户端密钥。 |
| `connectionSpec.id` | [!DNL Oracle Responsys]源的连接规范ID的值固定为： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Oracle Responsys]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将营销自动化数据引入Experience Platform](../../collect/marketing-automation.md)
