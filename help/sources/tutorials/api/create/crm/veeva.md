---
keywords: Experience Platform；主页；热门主题；Veeva CRM;Veeva CRM;Veeva;
solution: Experience Platform
title: 使用流服务API创建Veeva CRM基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Veeva CRM。
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# 创建 [!DNL Veeva CRM] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Veeva CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Veeva CRM] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Veeva CRM]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 您的 [!DNL Veeva CRM] 实例。 |
| `username` | 您的 [!DNL Veeva CRM] 帐户。 |
| `password` | 密码值 [!DNL Veeva CRM] 帐户。 |
| `securityToken` | 您的安全令牌 [!DNL Veeva CRM] 实例。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Veeva CRM] 为： `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

有关这些值的更多信息，请参阅此 [[!DNL Veeva CRM] 文档](https://developer.veevacrm.com/api/#order-management-rest-api).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Veeva CRM] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 您的 [!DNL Veeva CRM] 基本连接。 您可以使用此名称查找 [!DNL Veeva CRM] 基本连接。 |
| `description` | 您的 [!DNL Veeva CRM] 基本连接。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.environmentUrl` | 您的 [!DNL Veeva CRM] 实例。 |
| `auth.params.username` | 您的 [!DNL Veeva CRM] 帐户。 |
| `auth.params.password` | 密码值 [!DNL Veeva CRM] 帐户。 |
| `auth.params.securityToken` | 您的安全令牌 [!DNL Veeva CRM] 实例。 |
| `connectionSpec.id` | 的连接规范ID [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

## 后续步骤

通过阅读本教程，您已创建 [!DNL Veeva CRM] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/crm.md)
