---
keywords: Experience Platform；主页；热门主题；oracle；雄辩；oracle雄辩
solution: Experience Platform
title: 使用流服务API创建OracleEloqua基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到OracleEloqua。
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 创建 [!DNL Oracle Eloqua] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Oracle Eloqua] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对平台的以下组件有充分的了解：

* [源](../../../../home.md):平台允许从各种源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md):平台提供可对单个 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Oracle Eloqua] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Oracle Eloqua]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | 您的 [!DNL Oracle Eloqua]. |
| `username` | 您的用户名 [!DNL Oracle Eloqua] 帐户。 用户名的格式必须为 `siteName + \\ + username`，其中 `siteName` 是您用来登录的公司名称 [!DNL Oracle Eloqua] 和 `username` 是您的用户名。 例如，您的登录用户名可以是： `adobe\\emily`. |
| `password` | 与您的 [!DNL Oracle Eloqua] 用户名。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID的值 [!DNL Oracle Eloqua] 源的固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

有关的身份验证凭据的详细信息 [!DNL Oracle Eloqua]，请参阅 [[!DNL Oracle Eloqua] 认证指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Oracle Eloqua] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Oracle Eloqua]:

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
| `name` | 您的 [!DNL Oracle Eloqua] 基本连接。 建议提供一个描述性名称，因为您可以使用此值查找基本连接。 |
| `description` | （可选）可包含以提供有关基本连接的补充信息的属性。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | 您的 [!DNL Oracle Eloqua] 服务器。 |
| `auth.params.username` | 包含与您的 [!DNL Oracle Eloqua] 帐户。 |
| `auth.params.password` | 与您的 [!DNL Oracle Eloqua] 帐户。 |
| `connectionSpec.id` | 的连接规范ID的值 [!DNL Oracle Eloqua] 源的固定为： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Oracle Eloqua] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
