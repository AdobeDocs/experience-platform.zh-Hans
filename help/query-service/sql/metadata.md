---
keywords: Experience Platform；主页；热门主题；PSQL；PSQL；查询服务；查询服务；元数据；命令；元数据命令；
solution: Experience Platform
title: 查询服务中的元数据PostgreSQL命令
description: 当前支持在Adobe Experience Platform查询服务中查询元数据的PostgreSQL命令列表。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 元数据 [!DNL PostgreSQL] 查询服务中的命令

对于数据集上的元数据，请执行以下操作 [!DNL PostgreSQL] 当前支持查询的命令：

>[!NOTE]
>
>下面列出的命令区分大小写。

| 命令 | 描述 |
|------- | ------------|
| `\conninfo` | 输出有关当前数据库连接的信息。 |
| `\d` | 显示所有可见表、视图、实体化视图、序列和外表列表。 |
| `\dE` | 显示外来表的列表。 |
| `\df or \df+` | 显示函数列表。 |
| `\di` | 显示索引列表。 |
| `\dm` | 显示实体化视图的列表。 |
| `\dn` | 显示架构（命名空间）列表。 |
| `\ds` | 显示序列列表。 |
| `\dS` | 显示PostgreSQL定义的表的列表。 |
| `\dt` | 显示表的列表。 |
| `\dT` | 显示数据类型列表。 |
| `\dv` | 显示视图列表。 |
| `\encoding` | 列出当前客户端字符集编码。 |
| `\errverbose` | 以最大详细程度重复最新的服务器错误消息。 |
| `\l or \list` | 显示服务器中的数据库列表。 |
| `\set` | 显示所有当前psql变量的名称和值。 |
| `\showtables` | 显示以下信息： <br>name：引用表时所依据的名称。<br>datasetId：存储的数据集的ID。<br>dataset：存储的数据集的名称。<br>description：数据集的描述。<br>resolved：一个布尔值，表明数据集是否在当前会话中解析。 |
| `\timing` | 将显示在打开和关闭之间切换。 显示以毫秒为单位。 超过一秒的间隔以分钟：秒格式显示，并且根据需要添加小时和天字段。 |

所有以开头的命令 `\d` 可以合并。 例如，您可以发出 `\dtsn` 显示所有表、序列和模式的列表。 `\d` 它本身显示所有可见的表、视图、实例化视图和序列。

有关上面列出的命令的更多信息，请参阅以下文档： [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). 但是，请注意， [!DNL PostgreSQL] 文档受支持 [!DNL Experience Platform].
