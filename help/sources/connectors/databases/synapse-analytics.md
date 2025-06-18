---
title: Azure Synapse Analytics Source Connector概述
description: 了解如何使用API或用户界面将Azure Synapse Analytics连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 3%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

[!DNL Azure Synapse Analytics]是一个基于云的分析服务，可统一大数据和数据仓库。 您可以使用SQL、[!DNL Spark]或实时工具摄取、浏览、准备和分析数据 — 所有这些操作都无需移动数据。

您可以使用[!DNL Azure Synapse Analytics]源连接帐户并将数据导入Adobe Experience Platform。

## 先决条件 {#prerequisites}

在将[!DNL Azure Synapse Analytics]帐户连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

### 配置权限

要将源帐户连接到Experience Platform，您的帐户必须启用以下两项权限：

* **查看源**
* **管理源**

如果您没有这些权限，请联系产品管理员以请求获取访问权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

### 对Experience Platform进行身份验证

您可以使用帐户密钥身份验证或服务主体密钥身份验证将您的[!DNL Azure Synapse Analytics]连接到Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

为以下凭据提供值，以使用帐户密钥身份验证将您的[!DNL Azure Synapse Analytics]数据库连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| 连接字符串 | 这是用于[!DNL Azure Synapse Analytics]身份验证的&#x200B;**连接字符串**。 标准格式为： `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 必须将占位符替换为实际连接详细信息。 |
| 连接规范ID | **连接规范**&#x200B;提供数据源的连接器属性。 这包含身份验证规范和创建&#x200B;**Base**&#x200B;和&#x200B;**Source**&#x200B;连接的要求等详细信息。 对于[!DNL Azure Synapse Analytics]，连接规范ID为： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 **注意：**&#x200B;只有在通过API连接时才需要此凭据。 |

>[!TAB 服务主体密钥身份验证]

要检索服务主体密钥身份验证的凭据，请导航到[[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home)并检索以下值：

* 应用程序 ID
* 显示名称
* 机密
* 租户 ID

接下来，导航到您的[[!DNL Azure Synapse Analytics] 实例](https://azure.microsoft.com/en-ca/products/synapse-analytics)，然后选择从外部提供程序创建用户的选项。 在此处，为架构上的服务主体提供相应的权限。 **注意：**：必须包含“SELECT”，因为它与架构预览所需的“COPY”类似。 例如，示例命令可以是：

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

为以下凭据提供值，以使用服务主体密钥身份验证将您的[!DNL Azure Synapse Analytics]数据库连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| Server | [!DNL Azure Synapse Analytics] SQL端点的完全限定域名。 |
| 数据库 | [!DNL Azure Synapse Analytics]工作区中特定数据库的名称。 |
| 租户 | 与您的[!DNL Azure]订阅关联的[!DNL Azure Active Directory]租户ID。 |
| 服务主体 ID | [!DNL Azure Active Directory]应用程序的客户端ID。 |
| 服务主体密钥 | 与服务主体关联的客户端密钥或密码。 |
| 连接规范ID | **连接规范**&#x200B;提供数据源的连接器属性。 这包含身份验证规范和创建&#x200B;**Base**&#x200B;和&#x200B;**Source**&#x200B;连接的要求等详细信息。 对于[!DNL Azure Synapse Analytics]，连接规范ID为： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 **注意：**&#x200B;只有在通过API连接时才需要此凭据。 |

有关详细信息，请阅读有关管理 [!DNL Azure Synapse Analytics][&#128279;](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity)的标识的[!DNL Azure] 文档。

>[!ENDTABS]

## 使用API将[!DNL Azure Synapse Analytics]连接到Experience Platform

* [使用流服务API连接 [!DNL Azure Synapse Analytics] 到Experience Platform](../../tutorials/api/create/databases/synapse-analytics.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Azure Synapse Analytics]连接到Experience Platform

* [在UI中将 [!DNL Azure Synapse Analytics] 连接到Experience Platform](../../tutorials/ui/create/databases/synapse-analytics.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)

