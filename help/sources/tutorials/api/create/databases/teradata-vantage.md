---
keywords: Experience Platform；主页；热门主题；Data Vantage
title: 使用流服务API创建TeradataVantage基连接
description: 了解如何使用Flow Service API将Adobe Experience Platform与VantageTeradata连接。
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# （测试版）创建 [!DNL Teradata Vantage] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Teradata Vantage] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Teradata Vantage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

以下部分提供了成功连接到时需要了解的其他信息 [!DNL Teradata Vantage] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Teradata Vantage]，则必须提供以下连接属性：

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 连接字符串是提供有关数据源以及如何连接到该数据源的信息的字符串。 的连接字符串模式 [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Teradata Vantage] 为： `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

有关入门的更多信息，请参阅此 [[!DNL Teradata Vantage] 文档](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Teradata Vantage] 身份验证凭据作为请求正文的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Teradata Vantage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 用于连接到的连接字符串 [!DNL Teradata Vantage] 实例。 的连接字符串模式 [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | 的 [!DNL Teradata Vantage] 连接规范ID: `2fa8af9c-2d1a-43ea-a253-f00a00c74412`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

通过阅读本教程，您已创建 [!DNL Teradata Vantage] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
