---
keywords: Experience Platform；主页；热门主题；PSQL;psql;查询服务；查询服务；元数据；命令；元数据命令；
solution: Experience Platform
title: 元数据PostgreSQL命令在查询服务中
topic-legacy: metadata
description: 一列表PostgreSQL命令，当前支持在Adobe Experience Platform 查询服务中查询元数据。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 元数据PostgreSQL命令在查询服务中

对于数据集上的元数据，当前支持以下PostgreSQL命令进行查询：

>[!NOTE]
>
>下面列出的命令区分大小写。

| 命令 | 描述 |
|------- | ------------|
| `\conninfo` | 输出有关当前数据库连接的信息。 |
| `\d` | 显示所有可见表、视图、实体化视图、序列和外来表的列表。 |
| `\dE` | 显示外来表的列表。 |
| `\df or \df+` | 显示列表函数。 |
| `\di` | 显示索引的列表。 |
| `\dm` | 显示实体化视图的列表。 |
| `\dn` | 显示列表模式(命名空间)。 |
| `\ds` | 显示序列列表。 |
| `\dS` | 显示PostgreSQL定义的表的列表。 |
| `\dt` | 显示表列表。 |
| `\dT` | 显示列表数据类型。 |
| `\dv` | 显示列表视图。 |
| `\encoding` | 列表当前客户端字符集编码。 |
| `\errverbose` | 以最大详细度重复最近的服务器错误消息。 |
| `\l or \list` | 显示服务器中数据库的列表。 |
| `\set` | 显示所有当前psql变量的名称和值。 |
| `\showtables` | 显示以下信息：<br>名称：表的引用名称。<br>datasetId:存储的数据集的ID。<br>数据集：存储的数据集的名称。<br>描述：数据集的描述。<br>已解决：一个布尔值，用于指示当前会话中是否解析数据集。 |
| `\timing` | 在打开和关闭之间切换显示。 显示以毫秒为单位。 超过一秒的时间间隔以分钟：秒格式显示，并根据需要添加小时和天字段。 |

所有与`\d`开始的命令都可以组合。 例如，可以发布`\dtsn`来显示所有表、序列和模式的列表。 `\d` 它本身显示所有可见表、视图、实体化视图和序列。

有关上述命令的其他信息，请参阅[postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)的文档。 但是，请注意，并非PostgreSQL文档中显示的所有选项都受[!DNL Experience Platform]支持。
