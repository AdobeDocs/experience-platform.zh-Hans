---
title: 使用Python和SQLAlchemy管理平台数据
description: 了解如何使用SQLAlchemy来使用Python而不是SQL管理平台数据。
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 使用管理Platform数据 [!DNL Python] 和 [!DNL SQLAlchemy]

了解如何使用SQLAlchemy以更灵活地管理Adobe Experience Platform数据。 对于不熟悉SQL的人来说，SQLAlchemy可以在使用关系数据库时大大缩短开发时间。 本文档提供了连接的说明和示例 [!DNL SQLAlchemy] 查询服务并开始使用Python与数据库交互。

[!DNL SQLAlchemy] 是一个对象关系映射器(ORM)和 [!DNL Python] 代码库，可以将存储在SQL数据库中的数据传输到 [!DNL Python] 对象。 然后，您可以使用对Platform数据湖中所保存的数据执行CRUD操作 [!DNL Python] 代码。 这消除了仅使用PSQL管理数据的需要。

## 快速入门

获取进行连接所需的凭据 [!DNL SQLAlchemy] 要Experience Platform，您必须有权访问Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## [!DNL Query Service] 凭据 {#credentials}

要查找凭据，请登录Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航中，后面是 **[!UICONTROL 凭据]**. 有关如何查找登录凭据的完整说明，请阅读 [凭据指南](../ui/credentials.md).

![突出显示“凭据”选项卡，其中显示了“查询服务”的过期凭据。](../images/use-cases/credentials.png)

虽然端口80是连接查询服务的推荐端口，但您也可以使用端口5432。

>[!IMPORTANT]
>
>如果您使用过期凭据（如上图所示）连接到查询服务，则您连接的会话生命周期将在贵组织的设置中定义的设置时间段后过期。 默认情况下，此时间段为24小时。 请参阅文档以了解如何 [使用未过期的凭据连接客户端](../ui/credentials.md#non-expiring-credentials)，或如何 [更改即将过期的凭据的会话生命周期](../ui/credentials.md#expiring-credentials).

一旦您有权访问QS凭据，请打开 [!DNL Python] 所选编辑器。

### 将凭据存储在 [!DNL Python] {#store-credentials}

在您的 [!DNL Python] 编辑者，导入 `urllib.parse.quote` 库并将每个凭据变量另存为参数。 此 `urllib.parse` 模块提供了一个标准界面，用于将URL字符串分解为组件。 quote函数可替换URL字符串中的特殊字符，以便安全地将数据用作URL组件。 以下是所需代码的示例：

>[!TIP]
>
>使用 [!DNL Python]的三引号输入多行密码字符串。

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>您为连接提供的密码 [!DNL SQLAlchemy] 的Experience Platform将在您使用过期凭据时过期。 请参阅 [“凭据”部分](#credentials) 了解更多信息。

### 创建引擎实例 [#create-engine]

创建变量后，导入 `create_engine` 函数并创建一个字符串，以在SQLAlchemy中编译和格式化查询服务凭据。 此 `create_engine` 然后使用函数来构建引擎实例。

>[!NOTE]
>
>`create_engine`返回引擎实例。 但是，在调用需要连接的查询之前，它不会打开与查询服务的连接。

使用第三方客户端访问Platform时必须启用SSL。 作为引擎的一部分，请使用 `connect_args` 输入其他关键字参数。 建议将SSL模式设置为 `require`. 请参阅 [SSL模式文档](../clients/ssl-modes.md) 以了解有关接受值的更多信息。

以下示例显示 [!DNL Python] 初始化引擎和连接字符串所需的代码。

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>您为连接提供的密码 [!DNL SQLAlchemy] 的Experience Platform将在您使用过期凭据时过期。 请参阅 [“凭据”部分](#credentials) 了解更多信息。

您现在可以使用来查询Platform数据 [!DNL Python]. 以下示例返回一个查询服务表名数组。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
