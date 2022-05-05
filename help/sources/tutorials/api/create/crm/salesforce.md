---
keywords: Experience Platform；主页；热门主题；Salesforce;Salesforce
solution: Experience Platform
title: 使用流服务API创建Salesforce基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Salesforce帐户。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# 创建 [!DNL Salesforce] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Salesforce] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接所需了解的其他信息 [!DNL Platform] 至 [!DNL Salesforce] 帐户 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接到 [!DNL Salesforce]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Salesforce] 源实例。 |
| `username` | 的用户名 [!DNL Salesforce] 用户帐户。 |
| `password` | 的密码 [!DNL Salesforce] 用户帐户。 |
| `securityToken` | 的安全令牌 [!DNL Salesforce] 用户帐户。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL AdWords] 为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

有关入门的更多信息，请访问 [此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Salesforce] 身份验证凭据作为请求参数的一部分。


**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Salesforce]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.username` | 与您的 [!DNL Salesforce] 帐户。 |
| `auth.params.password` | 与 [!DNL Salesforce] 帐户。 |
| `auth.params.securityToken` | 与 [!DNL Salesforce] 帐户。 |
| `connectionSpec.id` | 的 [!DNL Salesforce] 连接规范ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Salesforce] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/crm.md)
