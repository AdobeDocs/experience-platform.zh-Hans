---
title: MariaDB Source Connector概述
description: 了解如何使用API或用户界面将MariaDB连接到Adobe Experience Platform。
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform允许从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方数据库引入数据。 [!DNL Experience Platform]可以连接到不同类型的数据库，如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括[!DNL MariaDB]。

## 先决条件 {#prerequisites}

在将[!DNL MariaDB]帐户连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在Azure或Amazon Web Services (AWS)上将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到您的允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Azure和AWS上的Experience Platform](../../ip-address-allow-list.md)的指南。

### 在Azure上对Experience Platform进行身份验证 {#azure}

必须提供以下凭据的值，才能将[!DNL MariaDB]连接到Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

要使用帐户密钥身份验证，请为以下凭据提供适当的值。

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 与您的[!DNL MariaDB]身份验证关联的连接字符串。 [!DNL MariaDB]连接字符串模式为： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL MariaDB]的连接规范ID为`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL MariaDB] 文档](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

>[!TAB 基本身份验证]

要使用基本身份验证，请为以下凭据提供相应的值。

| 凭据 | 描述 |
| --- | --- |
| `server` | [!DNL MariaDB]数据库的名称或IP。 |
| `username` | 数据库的名称。 |
| `port` | 要连接的通信端点的端口号。 |
| `password` | 与数据库对应的用户名。 |
| `database` | 与数据库对应的密码。 |
| `sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL MariaDB]的连接规范ID为`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL MariaDB] 文档](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

>[!ENDTABS]

### 在Amazon Web Services (AWS)上对Experience Platform进行身份验证 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

必须提供以下凭据的值，才能将[!DNL MariaDB]连接到AWS上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `server` | [!DNL MariaDB]数据库的名称或IP。 |
| `username` | 数据库的名称。 |
| `port` | 要连接的通信端点的端口号。 |
| `password` | 与数据库对应的用户名。 |
| `database` | 与数据库对应的密码。 |
| `sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL MariaDB]的连接规范ID为`3000eb99-cd47-43f3-827c-43caf170f015`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL MariaDB] 文档](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)。

## 使用API将[!DNL MariaDB]连接到Experience Platform

- [使用流服务API创建MariaDB基本连接](../../tutorials/api/create/databases/mariadb.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL MariaDB]连接到Experience Platform

- [在UI中创建MariaDB源连接](../../tutorials/ui/create/databases/mariadb.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
