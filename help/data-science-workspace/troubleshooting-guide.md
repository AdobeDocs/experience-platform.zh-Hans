---
keywords: Experience Platform；故障排除；数据科学Workspace；热门主题
solution: Experience Platform
title: 数据科学Workspace疑难解答指南
description: 本文档提供有关Adobe Experience Platform数据科学Workspace的常见问题解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# [!DNL Data Science Workspace]疑难解答指南

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本文档提供有关Adobe Experience Platform [!DNL Data Science Workspace]的常见问题解答。 有关[!DNL Experience Platform] API的一般问题和疑难解答，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

## JupyterLab Notebook查询状态停滞在执行状态

JupyterLab Notebook可能指示单元格在某些内存不足的情况下无限期地处于执行状态。 例如，在查询大型数据集或执行多个后续查询时，JupyterLab Notebook可能会用尽可用内存来存储生成的数据流对象。 在此情况下可以看到一些指标。 首先，即使单元格旁边的[`*`]图标显示正在执行，内核仍进入空闲状态。 此外，底部栏显示已使用/可用的RAM数量。

![可用RAM](./images/jupyterlab/user-guide/allocate-ram.png)

在数据读取期间，内存可能会增加，直到达到您分配的最大内存量。 一旦达到最大内存并且内核重新启动，就会释放内存。 这意味着，由于内核重新启动，在此情况下使用的内存可能显示为非常低，而在重新启动之前，内存将非常接近分配的最大RAM。

要解决此问题，请选择JupyterLab右上角的齿轮图标，然后将滑块向右滑动，然后选择&#x200B;**[!UICONTROL 更新配置]**&#x200B;以分配更多RAM。 此外，如果您正在运行多个查询并且RAM值接近分配的最大量，除非您需要从以前的查询获得结果，请重新启动内核以重置可用的RAM量。 这可确保您拥有可用于当前查询的最大RAM量。

![分配更多ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

如果分配了最大内存量(RAM)但仍遇到此问题，您可以通过减少列或数据范围来修改查询，以便对较小的数据集大小进行操作。 要使用全部数据，建议您使用Spark笔记本。

## [!DNL Google Chrome]中未加载[!DNL JupyterLab]环境

>[!IMPORTANT]
>
>此问题已得到解决，但仍可能存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器处于最新状态。

使用[!DNL Google Chrome]浏览器版本80.x时，默认情况下会阻止所有第三方Cookie。 此策略可以阻止[!DNL JupyterLab]在Adobe Experience Platform中加载。

要解决此问题，请执行以下步骤：

在您的[!DNL Chrome]浏览器中，导航到右上角并选择&#x200B;**设置**(或者，您可以在地址栏中复制并粘贴“chrome://settings/”)。 接下来，滚动到页面底部，然后单击&#x200B;**高级**&#x200B;下拉列表。

![chrome高级](./images/faq/chrome-advanced.png)

将显示&#x200B;**隐私和安全性**&#x200B;部分。 接下来，单击&#x200B;**网站设置**，然后单击&#x200B;**Cookie和网站数据**。

![chrome高级](./images/faq/privacy-security.png)

![chrome高级](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关闭”。

![chrome高级](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您可以禁用第三方Cookie并添加[*。]ds.adobe.net到允许列表。

在地址栏中导航到“chrome://flags/”。 使用右侧的下拉菜单搜索并禁用标题为&#x200B;*“默认为Cookie设置SameSite”*&#x200B;的标记。

![禁用samesite标志](./images/faq/samesite-flag.png)

在步骤2之后，系统会提示您重新启动浏览器。 重新启动后，[!DNL Jupyterlab]应该可以访问。

## 为什么在Safari中无法访问[!DNL JupyterLab]？

Safari在Safari &lt; 12中默认禁用第三方Cookie。 由于您的[!DNL Jupyter]虚拟机实例与其父框架驻留在不同的域上，因此Adobe Experience Platform当前要求启用第三方Cookie。 请启用第三方Cookie或切换到其他浏览器，如[!DNL Google Chrome]。

对于Safari 12，您需要将用户代理切换到“[!DNL Chrome]”或“[!DNL Firefox]”。 若要切换用户代理，请打开&#x200B;*Safari*&#x200B;菜单并选择&#x200B;**首选项**。 将出现首选项窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择&#x200B;**高级**。 然后选中&#x200B;*在菜单栏*&#x200B;中显示“开发”菜单。 完成此步骤后，可以关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

接下来，从顶部导航栏中选择&#x200B;**开发**&#x200B;菜单。 从&#x200B;**开发**&#x200B;下拉列表中，将鼠标悬停在&#x200B;**用户代理**&#x200B;上。 您可以选择要使用的&#x200B;**[!DNL Chrome]**&#x200B;或&#x200B;**[!DNL Firefox]**&#x200B;用户代理字符串。

![开发菜单](./images/faq/user-agent.png)

## 为什么我在尝试上载或删除[!DNL JupyterLab]中的文件时看到“403禁止访问”消息？

如果您的浏览器启用了广告阻止软件，例如[!DNL Ghostery]或[!DNL AdBlock] Plus，则每个广告阻止软件中必须允许域“\*.adobe.net”才能使[!DNL JupyterLab]正常工作。 这是因为[!DNL JupyterLab]虚拟机运行在不同于[!DNL Experience Platform]域的域上。

## 为什么我的[!DNL Jupyter Notebook]的某些部分看起来很混乱或者没有呈现为代码？

如果意外地将相关单元格从“代码”更改为“Markdown”，则可能会发生这种情况。 在集中代码单元格时，按组合键&#x200B;**ESC+M**&#x200B;会将单元格的类型更改为Markdown。 可以通过笔记本顶部的下拉指示器来更改选定单元格的类型。 要将单元格类型更改为代码，请先选择要更改的给定单元格。 接下来，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义[!DNL Python]库？

[!DNL Python]内核预安装了许多流行的机器学习库。 但是，通过在代码单元格中执行以下命令，可以安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的[!DNL Python]库的完整列表，请参阅《JupyterLab用户指南》[&#128279;](./jupyterlab/overview.md#supported-libraries)的附录部分。

## 我可以安装自定义PySpark库吗？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参阅《JupyterLab用户指南》[&#128279;](./jupyterlab/overview.md#supported-libraries)的附录部分。

## 是否可以为[!DNL JupyterLab] [!DNL Spark]或PySpark内核配置[!DNL Spark]群集资源？

您可以通过将以下块添加到笔记本的第一个单元格来配置资源：

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

有关[!DNL Spark]群集资源配置的更多信息，包括可配置属性的完整列表，请参阅[JupyterLab用户指南](./jupyterlab/overview.md#kernels)。

## 为什么在尝试为较大的数据集执行某些任务时会收到错误？

如果您收到错误，原因如`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`。这通常意味着驱动程序或执行器的内存不足。 有关数据限制以及如何对大型数据集执行任务的更多信息，请参阅JupyterLab Notebooks [数据访问](./jupyterlab/access-notebook-data.md)文档。 通常，通过将`mode`从`interactive`更改为`batch`可以解决此错误。

此外，在写入大型Spark/PySpark数据集时，在执行写入代码之前缓存数据(`df.cache()`)可以显着改善性能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果在读取数据时遇到问题并将转换应用于数据，请尝试在转换之前缓存数据。 缓存数据可防止通过网络进行多次读取。 从读取数据开始。 接下来，缓存(`df.cache()`)数据。 最后，执行转换。

## 为什么我的Spark/PySpark笔记本要花这么长时间来读写数据？

如果对数据执行转换（如使用`fit()`），则转换可能会执行多次。 为了提高性能，请在执行`fit()`之前使用`df.cache()`缓存您的数据。 这样可以确保仅执行一次转换，并防止通过网络进行多次读取。

**建议的顺序：**&#x200B;从读取数据开始。 接下来，执行转换，然后缓存(`df.cache()`)数据。 最后，执行`fit()`。

## 为什么我的Spark/PySpark笔记本无法运行？

如果收到以下任何错误：

- 由于暂存失败，作业已中止……只能压缩每个分区中具有相同元素数的RDD。
- 远程RPC客户端已取消关联和其他内存错误。
- 读取和写入数据集时性能不佳。

在写入数据之前，请检查以确保您正在缓存数据(`df.cache()`)。 在笔记本中执行代码时，在操作（如`fit()`）之前使用`df.cache()`可以极大地提高笔记本性能。 在写入数据集之前使用`df.cache()`可确保仅执行一次转换，而不是执行多次。

## 数据科学Workspace中的[!DNL Docker Hub]限制限制

自2020年11月20日起，对匿名和自由身份验证使用Docker Hub的费率限制已生效。 匿名和免费[!DNL Docker Hub]用户限制为每六小时100个容器图像提取请求。 如果您受这些更改影响，您将收到此错误消息：`ERROR: toomanyrequests: Too Many Requests.`或`You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`。

目前，仅当您尝试在六小时内构建100个按配方生产的笔记本，或者如果您在数据科学Workspace中使用频繁进行放大和缩小的基于Spark的笔记本，此限制才会影响您的组织。 但是，这不太可能，因为运行这些服务器的群集在空闲之前保持活动状态两个小时。 这减少了群集处于活动状态时所需的Pull数。 如果收到上述任何错误，则需要等待重置[!DNL Docker]限制。

有关[!DNL Docker Hub]速率限制的详细信息，请访问[DockerHub文档](https://www.docker.com/increase-rate-limits)。 我们正在研究此问题的解决方案，并期待在后续版本中推出此解决方案。
