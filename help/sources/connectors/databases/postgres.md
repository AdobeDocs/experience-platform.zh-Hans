---
title: PostgreSQL Source连接器概述
description: 了解Adobe Experience Platform上的PostgreSQL源。
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 98d1bec3cd453f3a20b8871b891b5464ddd44a09
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

阅读本文档以了解在将[!DNL PostgreSQL]数据库连接到Adobe Experience Platform之前需要完成的先决步骤。

## 先决条件 {#prerequisites}

在将[!DNL PostgreSQL]数据库连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在Azure或Amazon Web Services (AWS)上将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到您的允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Azure和AWS上的Experience Platform](../../ip-address-allow-list.md)的指南。

### 在Azure上对Experience Platform进行身份验证 {#azure}

必须提供以下身份验证凭据的值，才能将[!DNL PostgreSQL]连接到Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

为以下凭据提供值，以使用帐户密钥身份验证将您的[!DNL PostgreSQL]数据库连接到Azure上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL PostgreSQL]的连接规范ID为`74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

有关详细信息，请阅读[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/)。

>[!TAB 基本身份验证]

提供以下凭据的值，以使用基本身份验证将您的[!DNL PostgreSQL]数据库连接到Azure上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `server` | [!DNL PostgreSQL]数据库的名称或IP地址。 |
| `port` | [!DNL PostgreSQL]服务器的TCP端口。 |
| `username` | 与您的[!DNL PostgreSQL]数据库身份验证关联的用户名。 |
| `password` | 与您的[!DNL PostgreSQL]数据库身份验证关联的密码。 |
| `database` | 要连接的[!DNL PostgreSQL]数据库的名称。 |
| `sslMode` | 要应用于您的连接的[!DNL Secure Sockets Layer] (SSL)方法。 可用的值包括： <ul><li>`Disable`：使用此选项禁用SSL。 如果您的服务器需要SSL配置，则连接将失败。</li><li>`Allow`：使用此选项可允许SSL连接。 如果服务器支持非SSL连接，则仍可以使用这些连接。</li><li>`Prefer`：使用此选项可优先使用SSL连接，因为服务器支持它们。 此选项还允许非SSL连接。</li><li>`Require`：使用此选项将SSL连接设为必需。 如果服务器不支持SSL，则连接将失败。</li><li>`Verify-Ca`：如果服务器不支持SSL，则使用此选项在连接失败时验证服务器证书。</li><li>`Verify-Full`：如果服务器不支持SSL，则在连接失败时，使用此选项验证具有主机名的服务器证书。</li></ul> |

有关详细信息，请阅读[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/)。

>[!ENDTABS]

### 在Amazon Web Services (AWS)上对Experience Platform进行身份验证 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

提供以下凭据的值，以使用基本身份验证将您的[!DNL PostgreSQL]数据库连接到AWS上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `server` | [!DNL PostgreSQL]数据库的名称或IP地址。 |
| `port` | [!DNL PostgreSQL]服务器的TCP端口。 |
| `username` | 与您的[!DNL PostgreSQL]数据库身份验证关联的用户名。 |
| `password` | 与您的[!DNL PostgreSQL]数据库身份验证关联的密码。 |
| `database` | 要连接的[!DNL PostgreSQL]数据库的名称。 |
| `sslMode` | 要应用于您的连接的[!DNL Secure Sockets Layer] (SSL)方法。 可用的值包括： <ul><li>`Disable`：使用此选项禁用SSL。 如果您的服务器需要SSL配置，则连接将失败。</li><li>`Allow`：使用此选项可允许SSL连接。 如果服务器支持非SSL连接，则仍可以使用这些连接。</li><li>`Prefer`：使用此选项可优先使用SSL连接，因为服务器支持它们。 此选项还允许非SSL连接。</li><li>`Require`：使用此选项将SSL连接设为必需。 如果服务器不支持SSL，则连接将失败。</li><li>`Verify-Ca`：如果服务器不支持SSL，则使用此选项在连接失败时验证服务器证书。</li><li>`Verify-Full`：如果服务器不支持SSL，则在连接失败时，使用此选项验证具有主机名的服务器证书。</li></ul> |

有关详细信息，请阅读[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/)。

## 使用API将[!DNL PostgreSQL]连接到Experience Platform

* [使用流服务API创建 [!DNL PostgreSQL] 基本连接](../../tutorials/api/create/databases/postgres.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL PostgreSQL]连接到Experience Platform

* [在UI中创建 [!DNL PostgreSQL] 源连接](../../tutorials/ui/create/databases/postgres.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
