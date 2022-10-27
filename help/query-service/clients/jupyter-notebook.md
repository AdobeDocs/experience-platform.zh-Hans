---
title: 将Jupyter Notebook连接到查询服务
description: 了解如何将Jupyter Notebook与Adobe Experience Platform查询服务连接。
source-git-commit: af37fe3be6b9645965b7477b9b85c5e11fe6fbae
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 连接 [!DNL Jupyter Notebook] 查询服务

本文档介绍连接所需的步骤 [!DNL Jupyter Notebook] 和Adobe Experience Platform查询服务。

## 快速入门

本指南要求您已拥有 [!DNL Jupyter Notebook] 熟悉其界面。 下载 [!DNL Jupyter Notebook] 或有关更多信息，请参阅 [官方 [!DNL Jupyter Notebook] 文档](https://jupyter.org/).

获取连接所需的凭据 [!DNL Jupyter Notebook] 要Experience Platform，您必须拥有 [!UICONTROL 查询] 工作区。 如果您当前无权访问 [!UICONTROL 查询] 工作区。

>[!TIP]
>
>[!DNL Anaconda Navigator] 是一种桌面图形用户界面(GUI)，它为安装和启动通用界面提供了一种更轻松的方法 [!DNL Python] 诸如 [!DNL Jupyter Notebook]. 它还有助于管理包、环境和通道，而无需使用命令行命令。
>您可以 [安装首选版本的应用程序](https://docs.anaconda.com/anaconda/install/) 从他们的网站上。
>按照引导式安装过程操作。 从Anaconda Navigator主屏幕中，选择 **[!DNL Jupyter Notebook]** 从支持的应用程序列表启动程序。
>![的 [!DNL Anaconda Navigator] 主屏幕 [!DNL Jupyter Notebook] 突出显示。](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>有关详细信息，请参阅 [官方文档](https://docs.anaconda.com/anaconda/navigator/).

## Launch [!DNL Jupyter Notebook]

在您打开了 [!DNL Jupyter Notebook] Web应用程序，选择 **[!DNL New]** 下拉列表后跟 **[!DNL Python 3]** 创建新笔记本。 的 [!DNL Notebook] 出现编辑器。

![的 [!DNL Jupiter Notebook] 使用 [!DNL New] 下拉列表和 [!DNL Python] 3突出显示。](../images/clients/jupyter-notebook/new-notebook.png)

在 [!DNL Notebook] 编辑器中，输入以下值： `pip install psycopg2-binary` 选择 **[!DNL Run]** 中。 输入行下方会显示成功消息。

>[!IMPORTANT]
>
>在此过程中，您必须选择 **[!DNL Run]** 执行每行代码。

![的 [!DNL Notebook] 突出显示安装库命令的UI。](../images/clients/jupyter-notebook/install-library.png)

接下来，导入 [!DNL PostgreSQL] 数据库适配器 [!DNL Python]. 输入值： `import psycopg2`选择 **[!DNL Run]**. 此过程没有成功消息。 如果没有错误消息，请继续执行下一步。

![的 [!DNL Notebook] 突出显示导入数据库驱动程序代码的UI。](../images/clients/jupyter-notebook/import-dbdriver.png)

您现在必须通过输入以下值来提供Adobe Experience Platform凭据： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 可以在 [!UICONTROL 查询] 部分 [!UICONTROL 凭据] 选项卡。 请参阅有关如何 [查找组织凭据](../ui/credentials.md) 以了解详细说明。

使用第三方客户端时，建议使用未过期的凭据，以免反复输入详细信息。 有关 [如何生成和使用未过期的凭据](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>从Platform UI复制凭据时，请确保凭据没有其他格式。 它们应全部位于一行中，属性和值之间应有一个空格。 凭据用引号括起来， **not** 逗号分隔。

![的 [!DNL Notebook] 突出显示连接凭据的UI。](../images/clients/jupyter-notebook/provide-credentials.png)

您的 [!DNL Jupyter Notebook] 实例现在已连接到查询服务。

## 查询执行示例

现在，您已连接 [!DNL Jupyter Notebook] 要查询服务，您可以使用 [!DNL Notebook] 输入。 以下示例使用简单的查询来演示该过程。

输入以下值：

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

接下来，调用参数(`data` 在上例中)以在无格式响应中显示查询结果。

![的 [!DNL Notebook] UI中包含命令，用于在笔记本中返回和显示SQL结果。](../images/clients/jupyter-notebook/example-query.png)

要以更易读的方式格式化结果，请使用以下命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

这些命令不会生成成功消息。 如果没有错误消息，则可以使用函数以表格式输出SQL查询的结果。

![设置SQL结果格式所需的命令。](../images/clients/jupyter-notebook/format-results-commands.png)

输入并运行 `df.head()` 函数查看表格化查询结果。

![SQL查询在 [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## 后续步骤

现在，您已连接查询服务，因此可以使用 [!DNL Jupyter Notebook] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
