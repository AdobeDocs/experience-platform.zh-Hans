---
title: 使用Python和SQLAlchemy管理Experience Platform数据
description: 了解如何使用SQLAlchemy代替SQL使用Python管理Experience Platform数据。
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 使用[!DNL Python]和[!DNL SQLAlchemy]管理Experience Platform数据

了解如何使用SQLAlchemy以更灵活地管理Adobe Experience Platform数据。 对于不熟悉SQL的人来说，SQLAlchemy可以在使用关系数据库时大大缩短开发时间。 本文档提供了将[!DNL SQLAlchemy]连接到查询服务并开始使用Python与数据库交互的说明和示例。

[!DNL SQLAlchemy]是对象关系映射器(ORM)和[!DNL Python]代码库，可以将存储在SQL数据库中的数据转换为[!DNL Python]对象。 然后，您可以使用[!DNL Python]代码对Experience Platform数据湖中保留的数据执行CRUD操作。 这消除了仅使用PSQL管理数据的需要。

## 快速入门

要获取将[!DNL SQLAlchemy]连接到Experience Platform所需的凭据，您必须有权访问Experience Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## [!DNL Query Service]凭据 {#credentials}

若要查找凭据，请登录到Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。 有关如何查找登录凭据的完整说明，请参阅[凭据指南](../ui/credentials.md)。

![已高亮显示“凭据”选项卡，其中的“查询服务”的凭据已过期。](../images/use-cases/credentials.png)

虽然端口80是连接查询服务的推荐端口，但您也可以使用端口5432。

>[!IMPORTANT]
>
>如果您使用过期凭据（如上图所示）连接到查询服务，则您连接的会话生命周期将在您组织的设置中定义的设置时间段后过期。 默认情况下，此时段为24小时。 请参阅文档，了解如何[连接具有非过期凭据](../ui/credentials.md#non-expiring-credentials)的客户端，或如何[更改过期凭据的会话生命周期](../ui/credentials.md#expiring-credentials)。

访问QS凭据后，打开您选择的[!DNL Python]编辑器。

### 在[!DNL Python]中存储凭据 {#store-credentials}

在[!DNL Python]编辑器中，导入`urllib.parse.quote`库并将每个凭据变量另存为参数。 `urllib.parse`模块提供了一个标准接口，用于将URL字符串分解为组件。 quote函数可替换URL字符串中的特殊字符，以便安全地将数据用作URL组件。 下面显示了所需代码的示例：

>[!TIP]
>
>使用[!DNL Python]的三引号输入多行密码字符串。

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
>您提供的用于将[!DNL SQLAlchemy]连接到Experience Platform的密码将在您使用过期凭据时过期。 有关详细信息，请参阅[凭据部分](#credentials)。

### 创建引擎实例[#create-engine]

创建变量后，导入`create_engine`函数并创建一个字符串，以在SQLAlchemy中编译和格式化查询服务凭据。 然后使用`create_engine`函数来构造引擎实例。

>[!NOTE]
>
>`create_engine`返回引擎的实例。 但是，在调用需要连接的查询之前，它不会打开与查询服务的连接。

使用第三方客户端访问Experience Platform时必须启用SSL。 作为引擎的一部分，使用`connect_args`输入其他关键词参数。 建议将SSL模式设置为`require`。 有关接受值的详细信息，请参阅[SSL模式文档](../clients/ssl-modes.md)。

以下示例显示了初始化引擎和连接字符串所需的[!DNL Python]代码。

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
>您提供的用于将[!DNL SQLAlchemy]连接到Experience Platform的密码将在您使用过期凭据时过期。 有关详细信息，请参阅[凭据部分](#credentials)。

您现在可以使用[!DNL Python]查询Experience Platform数据。 以下示例返回了一个查询服务表名数组。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
