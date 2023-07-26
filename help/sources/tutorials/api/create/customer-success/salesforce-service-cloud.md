---
keywords: Experience Platform；主页；热门主题；Salesforce Service Cloud；Salesforce Service Cloud
solution: Experience Platform
title: 使用流服务API创建Salesforce Service云源连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 创建 [!DNL Salesforce Service Cloud] 源连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Salesforce Service Cloud]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 您的用户名 [!DNL Salesforce Service Cloud] 用户帐户。 |
| `password` | 您的密码 [!DNL Salesforce Service Cloud] 帐户。 |
| `securityToken` | 您的安全令牌 [!DNL Salesforce Service Cloud] 帐户。 |
| `apiVersion` | （可选） REST API版本的 [!DNL Salesforce Service Cloud] 您正在使用的实例。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Service Cloud] 为： `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

有关入门的更多信息，请参阅 [此Salesforce Service Cloud文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Salesforce Service Cloud] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Salesforce Service Cloud]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for salesforce service cloud",
      "description": "Base connection for salesforce service cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.username` | 与您的关联的用户名 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.password` | 与您的关联的密码 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.securityToken` | 与您的关联的安全令牌 [!DNL Salesforce Service Cloud] 帐户。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 连接规范ID： `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**响应**

成功响应将返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Salesforce Service Cloud] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将客户成功数据引入Platform [!DNL Flow Service] API](../../collect/customer-success.md)
