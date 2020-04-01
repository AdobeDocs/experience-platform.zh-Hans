---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 元数据命令
topic: metadata
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# 元数据命令

对于数据集上的元数据，当前支持以下PSQL命令进行查询：

>[!NOTE] 下面列出的命令区分大小写。

| 命令 | 描述 |
|------- | ------------|
| `\conninfo` | 输出有关当前数据库连接的信息。 |
| `\d` | 显示所有可见表、视图、实体化视图、序列和外表的列表。 |
| `\dE` | 显示一列表外表。 |
| `\df or \df+` | 显示一列表函数。 |
| `\di` | 显示索引列表。 |
| `\dm` | 显示实体化列表的视图。 |
| `\dn` | 显示列表模式(命名空间)。 |
| `\ds` | 显示序列列表。 |
| `\dS` | 显示PostgreSQL定义的表的列表。 |
| `\dt` | 显示表列表。 |
| `\dT` | 显示一列表数据类型。 |
| `\dv` | 显示一列表视图。 |
| `\encoding` | 列表当前客户端字符集编码。 |
| `\errverbose` | 以最大程度重复最近的服务器错误消息。 |
| `\l or \list` | 显示服务器中数据库的列表。 |
| `\set` | 显示所有当前psql变量的名称和值。 |
| `\showtables` | 显示以下信息： <br>名称：引用表的名称。<br>datasetId:存储的数据集的ID。<br>数据集：存储的数据集的名称。<br>说明：数据集的描述。<br>已解决：一个布尔值，它表示当前会话中是否已解析数据集。 |
| `\timing` | 在打开和关闭之间切换显示。 显示以毫秒为单位。 超过一秒的间隔以分钟：秒格式显示，并根据需要添加小时和天字段。 |

可以组合所有与开始 `\d` 的命令。 例如，您可以发出 `\dtsn` 问题，显示所有表、序列和模式的列表。 `\d` 仅显示所有可见表、视图、实体化视图和序列。

有关上述命令的其他信息，请参阅 [postgresql.org上的文档](https://www.postgresql.org/docs/10/app-psql.html)。 但是，请注意，并非PostgreSQL文档中显示的所有选项都受Experience Platform支持。

