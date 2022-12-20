---
title: 使用Python和SQLAlchemy管理平台数据
description: 了解如何使用SQLAlchemy来使用Python而不是SQL来管理平台数据。
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 使用管理平台数据 [!DNL Python] 和 [!DNL SQLAlchemy]

了解如何使用SQLAlchemy，以在管理Adobe Experience Platform数据方面获得更大的灵活性。 对于不熟悉SQL的用户，SQLAlchemy在使用关系数据库时可以大大缩短开发时间。 本文档提供了连接的说明和示例 [!DNL SQLAlchemy] 查询服务，并开始使用Python与数据库进行交互。

[!DNL SQLAlchemy] 是对象关系映射器(ORM)和 [!DNL Python] 可将存储在SQL数据库中的数据传输到 [!DNL Python] 对象。 然后，您可以使用对平台数据湖中保留的数据执行CRUD操作 [!DNL Python] 代码。 这样就无需仅使用PSQL管理数据。

## 快速入门

获取连接所需的凭据 [!DNL SQLAlchemy] 要Experience Platform，您必须有权访问平台UI中的“查询”工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## [!DNL Query Service] 凭据 {#credentials}

要查找凭据，请登录到Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航，然后是 **[!UICONTROL 凭据]**. 有关如何查找登录凭据的完整说明，请阅读 [凭据指南](../ui/credentials.md).

![突出显示了查询服务的凭据选项卡，其过期凭据。](../images/use-cases/credentials.png)

虽然建议将端口80作为连接查询服务的端口，但您也可以使用端口5432。

>[!IMPORTANT]
>
>如果您使用过期凭据（如上图所示）连接到查询服务，则连接的会话生命周期将在组织设置中定义的设置时间段后过期。 默认情况下，此时段为24小时。 请参阅相关文档以了解如何 [使用未过期的凭据连接客户端](../ui/credentials.md#non-expiring-credentials)，或如何 [更改即将过期的凭据的会话期限](../ui/credentials.md#expiring-credentials).

访问QS凭据后，打开 [!DNL Python] 编辑。

### 将凭据存储在中 [!DNL Python] {#store-credentials}

在 [!DNL Python] 编辑器，导入 `urllib.parse.quote` 库，并将每个凭据变量另存为参数。 的 `urllib.parse` 模块提供了一个标准界面，用于将URL字符串划分为多个组件。 引号函数可替换URL字符串中的特殊字符，以使数据安全地用作URL组件。 所需代码的示例如下所示：

>[!TIP]
>
>使用 [!DNL Python]&#39;s三引号输入多行密码字符串。

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
>您为连接提供的密码 [!DNL SQLAlchemy] Experience Platform的过期日期。 请参阅 [凭据部分](#credentials) 以了解更多信息。

### 创建引擎实例 [#create-engine]

创建变量后，导入 `create_engine` 函数，并创建一个字符串以在SQLAlchemy中编译和格式化查询服务凭据。 的 `create_engine` 函数来构建引擎实例。

>[!NOTE]
>
>`create_engine`返回引擎的实例。 但是，在调用需要连接的查询之前，不会打开与查询服务的连接。

使用第三方客户端访问平台时必须启用SSL。 作为引擎的一部分，请使用 `connect_args` 以输入其他关键字参数。 建议您将SSL模式设置为 `require`. 请参阅 [SSL模式文档](../clients/ssl-modes.md) 以了解有关已接受值的详细信息。

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
>您为连接提供的密码 [!DNL SQLAlchemy] Experience Platform的过期日期。 请参阅 [凭据部分](#credentials) 以了解更多信息。

现在，您可以使用 [!DNL Python]. 以下示例返回查询服务表名称的数组。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
