---
title: 从Jupyter笔记本连接到Data Distiller
description: 了解如何从Jupyter Notebook连接到Data Distiller。
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 1%

---

# 从Jupyter笔记本连接到DD

要使用高价值客户体验数据丰富您的机器学习管道，您必须首先从Jupyter Notebooks连接到Data Distiller。 本文档介绍在机器学习环境中从Python笔记本连接到Data Distiller的步骤。

## 快速入门

本指南假定您熟悉交互式Python笔记本，并且有权访问笔记本环境。 笔记本可以在基于云的机器学习环境中托管，也可以在本地使用 [Jupyter Notebook](https://jupyter.org/).

### 获取连接凭据

要连接到Data Distiller和其他Adobe Experience Platform服务，您需要Experience PlatformAPI凭据。 API凭据可在中创建  [Adobe Developer控制台](https://developer.adobe.com/console/home) 由具有Experience Platform开发人员访问权限的用户访问。 建议您创建专门用于数据科学工作流的Oauth2 API凭据，并让贵组织的Adobe系统管理员将该凭据分配给具有适当权限的“角色”。

请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关创建API凭据和获取所需权限的详细说明。

数据科学的推荐权限包括：

- 将用于数据科学的沙盒（通常为prod）
- 数据建模：管理架构
- 数据管理：管理数据集
- 数据摄取：查看源
- 目标：管理和激活数据集目标
- 查询服务：管理查询

默认情况下，角色（以及分配给该角色的API凭据）被阻止访问任何标记的数据。 根据组织的数据治理策略，系统管理员可以授予角色对某些被视为适合数据科学使用的已标记数据的访问权限。 Platform客户有责任适当地管理标签访问和政策，以遵守相关法规和组织政策。

### 将凭据存储在单独的配置文件中

为了确保凭据的安全，建议您避免将凭据信息直接写入代码。 相反，应将凭据信息保存在单独的配置文件中，并读取连接到Experience Platform和Data Distiller所需的值。

例如，您可以创建一个名为 `config.ini` 并包括以下信息（以及任何其他有助于在会话之间保存的信息，例如数据集ID）：

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

在笔记本中，您随后可以使用将凭据信息读入内存 `configParser` 来自标准Python库的包：

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

然后，您可以在代码中引用凭据值，如下所示：

```python
org_id = config.get('Credential', 'ims_org_id')
```

## 此 `aepp` Python库

[aepp](https://github.com/adobe/aepp/tree/main) 是一个Adobe管理的开源Python库，提供连接到Data Distiller和提交查询以及向其他Experience Platform服务发出请求的功能。 此 `aepp` 库又依赖于PostgreSQL数据库适配器包  `psycopg2` 用于交互式数据Distiller查询。 可以使用连接到数据Distiller并查询Experience Platform数据集 `psycopg2` 独自，但是 `aepp` 提供了更大的便利性和附加功能，可用于向所有Experience PlatformAPI服务发出请求。

安装或升级 `aepp` 和 `psycopg2` 在您的环境中，您可以使用 `%pip` 笔记本中的magic命令：

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

然后，您可以配置 `aepp` 库中包含您的凭据，代码如下：

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## 创建与Data Distiller的连接

一次 `aepp` 配置了凭据，您可以使用以下代码创建与Data Distiller的连接并启动交互式会话，如下所示：

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

然后，您可以在Experience Platform沙盒中查询数据集。 给定您要查询的数据集的ID，您可以从目录服务检索相应的表名称，并对表运行查询：

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### 连接到单个数据集以提高查询性能

默认情况下，数据Distiller连接会连接到沙盒中的所有数据集。 为了加快查询速度并减少资源使用，您可以改为连接到感兴趣的特定数据集。 您可以通过更改 `dbname` 在Data Distiller连接对象中 `{sandbox}:{table_name}`：

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## 后续步骤

通过阅读本文档，您已了解如何在机器学习环境中从Python笔记本连接到Data Distiller。 在机器学习环境中创建从Experience Platform到馈送自定义模型的功能管道的下一步是 [浏览和分析数据集](./exploratory-analysis.md).
