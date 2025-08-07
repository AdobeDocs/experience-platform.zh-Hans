---
title: Oracle DB Source连接器概述
description: 了解如何使用API或用户界面将Oracle连接到Adobe Experience Platform。
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB]是由[!DNL Oracle Corporation]开发的功能强大的关系数据库管理系统。 您可以使用[!DNL Oracle DB]高效安全地存储、管理和检索大量结构化数据。

使用Adobe Experience Platform源目录中的[!DNL Oracle DB]源连接数据库并将数据摄取到Experience Platform中。

## 先决条件 {#prerequisites}

在将[!DNL Oracle DB]帐户连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在Azure或Amazon Web Services (AWS)上将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到您的允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Azure和AWS上的Experience Platform](../../ip-address-allow-list.md)的指南。

### 在Azure上对Experience Platform进行身份验证 {#azure}

提供连接字符串以验证您的[!DNL Oracle DB]帐户并将其连接到Azure上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| 连接字符串 | 连接字符串是应用程序用来连接到数据库的文本字符串。 [!DNL Oracle DB]连接字符串模式为： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| 连接规范ID | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 [!DNL Oracle]的连接规范ID为`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

### 在Amazon Web Services上对Experience Platform进行身份验证 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

为以下凭据提供值以验证你的[!DNL Oracle DB]帐户并将它连接到AWS上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| Server | [!DNL Oracle DB]服务器的IP地址或主机名。 |
| 端口 | 数据库服务器的端口号。 默认端口号为`1521`。 |
| 用户名 | 用于验证和访问数据库的[!DNL Oracle DB]用户帐户。 |
| 密码 | 与您的用户名关联的密钥，用于身份验证。 |
| 数据库 | 要连接的特定[!DNL Oracle]数据库实例。 |
| 架构 | 数据库对象的容器，如表、视图或过程。 |
| SSL模式 | 一个布尔值，用于控制是否强制使用SSL。 此配置取决于您的服务器支持，默认为`false`。 |
| 连接规范ID | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 [!DNL Oracle]的连接规范ID为`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |


## 使用API将[!DNL Oracle]连接到[!DNL Experience Platform]

- [使用流服务API连接Oracle DB](../../tutorials/api/create/databases/oracle.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Oracle]连接到[!DNL Experience Platform]

- [使用Oracle UI工作区连接Experience Platform DB。](../../tutorials/ui/create/databases/oracle.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
