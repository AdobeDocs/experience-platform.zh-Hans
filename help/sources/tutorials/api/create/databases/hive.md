---
keywords: Experience Platform；主页；热门主题；Apache Hive;Hive
solution: Experience Platform
title: 在Azure HDInsights Base连接上使用流服务API创建Apache配置单元
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Azure HDInsights上的Apache Hive连接到Adobe Experience Platform。
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API在[!DNL Azure HDInsights]基本连接上创建[!DNL Apache Hive]

>[!NOTE]
>
>[!DNL Azure HDInsights]连接器上的[!DNL Apache Hive]处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)在[!DNL Azure HDInsights]（以下称为“[!DNL Hive]”）上为[!DNL Apache Hive]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Hive]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Hive]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Hive]服务器的IP地址或主机名。 |
| `username` | 用于访问[!DNL Hive]服务器的用户名。 |
| `password` | 与用户对应的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Hive]的连接规范ID是：`aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

有关入门的详细信息，请参见[此Hive文档](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Hive]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Hive]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的[!DNL Hive]帐户关联的连接字符串。 |
| `connectionSpec.id` | [!DNL Hive]连接规范ID:`aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Hive]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/database-nosql.md)浏览数据库。
