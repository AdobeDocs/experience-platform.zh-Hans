---
title: MySQL Source Connector概述
description: 了解如何使用API或用户界面将MySQL连接到Adobe Experience Platform。
last-substantial-update: 2025-05-17T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: 7a5dae76c5b58b302b4f3295efc17f40dbb9b18b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL]是用于存储和管理结构化数据的开源关系数据库管理系统。 它将数据组织成表，并使用SQL（结构化查询语言）来查询和更新信息。 [!DNL MySQL]广泛用于Web应用程序，支持多种平台，以其速度、可靠性和易用性而闻名。 它非常适合于从小型网站到大型企业系统的各种情况。

您可以使用[!DNL MySQL]源连接帐户并将数据从[!DNL MySQL]数据库摄取到Adobe Experience Platform。

## 先决条件 {#prerequisites}

在将[!DNL MySQl]帐户连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在Azure或Amazon Web Services (AWS)上将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到您的允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Azure和AWS上的Experience Platform](../../ip-address-allow-list.md)的指南。

### 在Azure上对Experience Platform进行身份验证 {#azure}

您可以使用帐户密钥身份验证或基本身份验证将[!DNL MySQL]数据库连接到Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

为以下凭据提供值，以使用帐户密钥身份验证将您的[!DNL MySQL]数据库连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 与您的帐户关联的[!DNL MySQL]连接字符串。 [!DNL MySQL]连接字符串模式为： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL MySQL]的连接规范ID为`26d738e0-8963-47ea-aadf-c60de735468a`。 |

有关详细信息，请阅读有关连接字符串[&#128279;](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)的[!DNL MySQL] 文档。

>[!TAB 基本身份验证]

为以下凭据提供值，以使用基本身份验证将[!DNL MySQL]数据库连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `server` | [!DNL MySQL]数据库的名称或IP地址。 |
| `database` | 要连接的[!DNL MySQL]数据库的名称。 |
| `username` | 与您的[!DNL MySQL]数据库身份验证关联的用户名。 |
| `password` | 与您的[!DNL MySQL]数据库身份验证关联的密码。 |
| `sslMode` | 要应用于您的连接的[!DNL Secure Sockets Layer] (SSL)方法。 可用的值包括： <ul><li>`DISABLED`：使用此选项禁用SSL。 如果您的服务器需要SSL配置，则连接将失败</li><li>`PREFERRED`：使用此选项可优先使用SSL连接，因为服务器支持它们。 此选项还允许非SSL连接。</li><li>`REQUIRED`：使用此选项将SSL连接设为必需。 如果服务器不支持SSL，则连接将失败。</li><li>`Verify-Ca`：如果服务器不支持SSL，则使用此选项在连接失败时验证服务器证书。</li><li>`Verify Identity`：如果服务器不支持SSL，则在连接失败时，使用此选项验证具有主机名的服务器证书。</li></ul> |

>[!ENDTABS]

## 使用API将[!DNL MySQL]连接到Experience Platform

- [使用流服务API连接 [!DNL MySQL] 数据库](../../tutorials/api/create/databases/mysql.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将MySQL连接到Experience Platform

- [使用UI将 [!DNL MySQL] 数据库连接到Experience Platform](../../tutorials/ui/create/databases/mysql.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
