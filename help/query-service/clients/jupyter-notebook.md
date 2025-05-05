---
title: 将Jupyter笔记本连接到查询服务
description: 了解如何将Jupyter Notebook连接到Adobe Experience Platform查询服务。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 将[!DNL Jupyter Notebook]连接到查询服务

本文档介绍将[!DNL Jupyter Notebook]连接到Adobe Experience Platform查询服务所需的步骤。

## 快速入门

本指南要求您已经拥有[!DNL Jupyter Notebook]的访问权限并熟悉其界面。 要下载[!DNL Jupyter Notebook]或了解更多信息，请参阅[官方 [!DNL Jupyter Notebook] 文档](https://jupyter.org/)。

要获取将[!DNL Jupyter Notebook]连接到Experience Platform所需的凭据，您必须有权访问Experience Platform UI中的[!UICONTROL 查询]工作区。 如果您当前无权访问[!UICONTROL 查询]工作区，请联系您的组织管理员。

>[!TIP]
>
>[!DNL Anaconda Navigator]是一个桌面图形用户界面(GUI)，它提供了一种更容易安装和启动常用[!DNL Python]程序（如[!DNL Jupyter Notebook]）的方法。 它还有助于在不使用命令行命令的情况下管理包、环境和通道。
>按照其网站上的引导式安装过程来[安装您的首选应用程序版本](https://docs.anaconda.com/anaconda/install/)。
>从Anaconda Navigator主屏幕中，从支持的应用程序列表中选择&#x200B;**[!DNL Jupyter Notebook]**&#x200B;以启动该程序。
>有关详细信息，请参阅[Anaconda官方文档](https://docs.anaconda.com/anaconda/navigator/)。

Jupyter官方文档提供了从命令行界面[&#128279;](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI) 运行笔记本的说明。

## Launch [!DNL Jupyter Notebook]

打开新的[!DNL Jupyter Notebook] Web应用程序后，从UI中选择&#x200B;**[!DNL New]**&#x200B;下拉列表，然后选择&#x200B;**[!DNL Python 3]**&#x200B;以创建新的笔记本。 出现[!DNL Notebook]编辑器。

在[!DNL Notebook]编辑器的第一行，输入以下值： `pip install psycopg2-binary`并从命令栏中选择&#x200B;**[!DNL Run]**。 输入行下方将显示一条成功消息。

>[!IMPORTANT]
>
>作为建立连接的过程的一部分，您必须选择&#x200B;**[!DNL Run]**&#x200B;以执行每行代码。

接下来，为[!DNL Python]导入[!DNL PostgreSQL]数据库适配器。 输入值： `import psycopg2`并选择&#x200B;**[!DNL Run]**。 此进程没有成功消息。 如果没有错误消息，请继续执行下一步。

您现在必须输入以下值来提供您的Adobe Experience Platform凭据： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`。 可在Experience Platform UI的[!UICONTROL 凭据]选项卡下的[!UICONTROL 查询]部分中找到您的连接凭据。 有关详细说明，请参阅有关如何[查找组织凭据](../ui/credentials.md)的文档。

在使用第三方客户端时，建议使用未过期的凭据，以节省重复输入详细信息的精力。 有关[如何生成和使用未过期的凭据](../ui/credentials.md#non-expiring-credentials)的说明，请参阅文档。

>[!IMPORTANT]
>
>从Experience Platform UI复制凭据时，不需要凭据的其他格式。 它们可以在一行中给出，属性和值之间只有一段空格。 凭据用引号括起来，**不能用逗号分隔**。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您的[!DNL Jupyter Notebook]实例现在已连接到查询服务。

## 示例查询执行

现在您已将[!DNL Jupyter Notebook]连接到查询服务，可以使用[!DNL Notebook]输入对数据集执行查询。 以下示例使用一个简单的查询来演示该过程。

输入以下值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接下来，调用参数（`data`，以上示例中为），以在未格式化的响应中显示查询结果。

要以更易于用户阅读的方式格式化结果，请使用以下命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

这些命令不会生成成功消息。 如果没有错误消息，则可以使用函数以表格式输出SQL查询的结果。

输入并运行`df.head()`函数以查看列表化的查询结果。

## 后续步骤

现在您已连接查询服务，可以使用[!DNL Jupyter Notebook]编写查询。 有关如何编写和运行查询的详细信息，请参阅[运行查询指南](../best-practices/writing-queries.md)。
