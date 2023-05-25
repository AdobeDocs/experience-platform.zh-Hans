---
title: 将Jupyter Notebook连接到查询服务
description: 了解如何将Jupyter Notebook与Adobe Experience Platform查询服务连接。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Connect [!DNL Jupyter Notebook] 查询服务

本文档介绍了连接所需的步骤 [!DNL Jupyter Notebook] 使用Adobe Experience Platform查询服务。

## 快速入门

本指南要求您已有权访问 [!DNL Jupyter Notebook] 并熟悉其界面。 要下载 [!DNL Jupyter Notebook] 有关更多信息，请参阅 [正式 [!DNL Jupyter Notebook] 文档](https://jupyter.org/).

获取进行连接所需的凭据 [!DNL Jupyter Notebook] 要Experience Platform，您必须有权访问 [!UICONTROL 查询] Platform UI中的工作区。 如果您当前无权访问 [!UICONTROL 查询] 工作区。

>[!TIP]
>
>[!DNL Anaconda Navigator] 是一个桌面图形用户界面(GUI)，它提供了一种更容易安装和启动通用的方法 [!DNL Python] 程序，例如 [!DNL Jupyter Notebook]. 它还有助于在不使用命令行命令的情况下管理包、环境和通道。
>按照其网站上的引导式安装过程操作，以便 [安装您的首选应用程序版本](https://docs.anaconda.com/anaconda/install/).
>从“Anaconda导航器”主屏幕中，选择 **[!DNL Jupyter Notebook]** 从支持的应用程序列表中启动该程序。
>欲知更多信息，请参见 [Anaconda官方文档](https://docs.anaconda.com/anaconda/navigator/).

Jupyter官方文档提供了以下说明： [从命令行界面运行笔记本](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI)。

## Launch [!DNL Jupyter Notebook]

在您打开新的 [!DNL Jupyter Notebook] Web应用程序，选择 **[!DNL New]** UI中的下拉列表，其后是 **[!DNL Python 3]** 以创建新的笔记本。 此 [!DNL Notebook] 编辑器出现。

在 [!DNL Notebook] 编辑器中，输入以下值： `pip install psycopg2-binary` 并选择 **[!DNL Run]** 命令栏中的。 输入行下方会显示一条成功消息。

>[!IMPORTANT]
>
>在形成连接的过程中，您必须选择 **[!DNL Run]** 执行每行代码。

接下来，导入 [!DNL PostgreSQL] 数据库适配器 [!DNL Python]. 输入值： `import psycopg2`并选择 **[!DNL Run]**. 此进程没有成功消息。 如果没有错误消息，请继续执行下一步。

您现在必须输入值以提供Adobe Experience Platform凭据： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 您的连接凭据可在 [!UICONTROL 查询] 部分，在 [!UICONTROL 凭据] Platform UI的选项卡。 请参阅有关如何执行操作的文档 [查找您的组织凭据](../ui/credentials.md) 以获取详细说明。

在使用第三方客户端时，建议使用不会过期的凭据，以节省重复输入详细信息的工作量。 有关说明，请参阅文档 [如何生成和使用不会过期的凭据](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>从Platform UI复制凭据时，不需要凭据的其他格式。 它们可以在一行中给出，属性和值之间只有一段空格。 凭据用引号括起来，并且 **非** 逗号分隔。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您的 [!DNL Jupyter Notebook] 实例现在已连接到查询服务。

## 示例查询执行

现在您已连接 [!DNL Jupyter Notebook] 要查询服务，您可以使用以下工具对数据集执行查询： [!DNL Notebook] 输入。 以下示例使用一个简单的查询来演示该过程。

输入以下值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接下来，调用参数(`data` （在上例中）以非格式化的响应显示查询结果。

要以更易于用户识别的方式格式化结果，请使用以下命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

这些命令不会生成成功消息。 如果没有错误消息，您可以使用函数以表格式输出SQL查询的结果。

输入并运行 `df.head()` 函数以查看列表化的查询结果。

## 后续步骤

现在，您已连接查询服务，您可以使用 [!DNL Jupyter Notebook] 以编写查询。 有关如何编写和运行查询的更多信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
