---
keywords: Experience Platform；主页；热门主题；oracle;
title: （测试版）使用流量服务API创建OracleResponsys基连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到OracleResponsys。
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# （测试版）创建 [!DNL Oracle Responsys] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Oracle Responsys] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Oracle Responsys] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对平台的以下组件有充分的了解：

* [源](../../../../home.md):平台允许从各种源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md):平台提供可对单个 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Oracle Responsys] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Oracle Responsys]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | 的REST身份验证端点URL [!DNL Oracle Responsys] 实例。 |
| `clientId` | 您的客户端ID [!DNL Oracle Responsys] 实例。 |
| `clientSecret` | 您的客户端密钥 [!DNL Oracle Responsys] 实例。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID的值 [!DNL Oracle Responsys] 源的固定为： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

有关的身份验证凭据的详细信息 [!DNL Oracle Responsys]，请参阅 [[!DNL Oracle Responsys] 认证指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Oracle Responsys] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Oracle Responsys]:

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
| `name` | 您的 [!DNL Oracle Responsys] 基本连接。 建议提供一个描述性名称，因为您可以使用此值查找基本连接。 |
| `description` | （可选）可包含以提供有关基本连接的补充信息的属性。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | 的REST身份验证端点URL [!DNL Oracle Responsys] 服务器。 |
| `auth.params.clientId` | 您的客户端ID [!DNL Oracle Responsys] 实例。 |
| `auth.params.clientSecret` | 您的客户端密钥 [!DNL Oracle Responsys] 实例。 |
| `connectionSpec.id` | 的连接规范ID的值 [!DNL Oracle Responsys] 源的固定为： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Oracle Responsys] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
