---
keywords: Experience Platform；故障诊断；Data Science Workspace；热门主题
solution: Experience Platform
title: Data Science Workspace疑难解答指南
topic-legacy: Troubleshooting
description: 本文档提供了有关Adobe Experience Platform Data Science Workspace的常见问题解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑难解答指南

本文档提供了有关Adobe Experience Platform [!DNL Data Science Workspace]的常见问题解答。 有关[!DNL Platform] API的一般问题和疑难解答，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

## [!DNL JupyterLab] 环境未在中加载  [!DNL Google Chrome]

>[!IMPORTANT]
>
>此问题已得到解决，但仍可能存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器是最新的。

使用[!DNL Google Chrome]浏览器版本80.x时，默认情况下会阻止所有第三方Cookie。 此策略可阻止在Adobe Experience Platform中加载[!DNL JupyterLab]。

要解决此问题，请执行以下步骤：

在[!DNL Chrome]浏览器中，导航到右上方，然后选择&#x200B;**Settings**(或者，您也可以在地址栏中复制并粘贴“chrome://settings/”)。 接下来，滚动到页面底部，然后单击&#x200B;**Advanced**&#x200B;下拉列表。

![chrome高级](./images/faq/chrome-advanced.png)

将显示&#x200B;**Privacy and security**&#x200B;部分。 接下来，单击&#x200B;**站点设置**，然后单击&#x200B;**Cookie和站点数据**。

![chrome高级](./images/faq/privacy-security.png)

![chrome高级](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关”。

![chrome高级](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以禁用第三方Cookie并添加[*。]ds.adobe.net到允许列表。

导航到地址栏中的“chrome://flags/”。 使用右侧的下拉菜单，搜索并禁用标题为&#x200B;*&quot;默认为Cookie设置SameSite&quot;*&#x200B;的标记。

![禁用samesite标记](./images/faq/samesite-flag.png)

在步骤2之后，系统会提示您重新启动浏览器。 重新启动后，应该可以访问[!DNL Jupyterlab]。

## 为什么我在Safari中无法访问[!DNL JupyterLab]?

Safari在Safari &lt; 12中默认禁用第三方Cookie。 由于[!DNL Jupyter]虚拟机实例位于与其父框架不同的域上，因此Adobe Experience Platform当前要求启用第三方Cookie。 请启用第三方Cookie或切换到其他浏览器，如[!DNL Google Chrome]。

对于Safari 12，您需要将用户代理切换到“[!DNL Chrome]”或“[!DNL Firefox]”。 要切换用户代理，请首先打开&#x200B;*Safari*&#x200B;菜单，然后选择&#x200B;**首选项**。 此时将出现“首选项”窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择&#x200B;**Advanced**。 然后，选中菜单栏&#x200B;*中的*&#x200B;显示开发菜单。 完成此步骤后，您可以关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

接下来，从顶部导航栏中选择&#x200B;**Develop**&#x200B;菜单。 在&#x200B;**Develop**&#x200B;下拉列表中，将鼠标悬停在&#x200B;**User Agent**&#x200B;上。 您可以选择要使用的&#x200B;**[!DNL Chrome]**&#x200B;或&#x200B;**[!DNL Firefox]**&#x200B;用户代理字符串。

![“开发”菜单](./images/faq/user-agent.png)

## 尝试在[!DNL JupyterLab]中上传或删除文件时，为什么我看到“403禁止”消息？

如果您的浏览器启用了广告拦截软件（如[!DNL Ghostery]或[!DNL AdBlock] Plus），则必须允许每个广告拦截软件中的域“\*.adobe.net”才能使[!DNL JupyterLab]正常运行。 这是因为[!DNL JupyterLab]虚拟机在与[!DNL Experience Platform]域不同的域上运行。

## 为什么我的[!DNL Jupyter Notebook]的某些部分看起来已加扰或未呈现为代码？

如果相关的单元格意外从“代码”更改为“标记”，则可能会发生这种情况。 当代码单元格聚焦时，按键组合&#x200B;**ESC+M**&#x200B;会将单元格类型更改为Markdown。 单元格类型可以通过笔记本顶部选定单元格的下拉指示器进行更改。 要将单元格类型更改为代码，请首先选择要更改的给定单元格。 接下来，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义[!DNL Python]库？

[!DNL Python]内核已预安装了许多常用的机器学习库。 但是，您可以通过在代码单元格中执行以下命令来安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的[!DNL Python]库的完整列表，请参阅《JupyterLab用户指南》的[附录部分。](./jupyterlab/overview.md#supported-libraries)

## 我能否安装自定义PySpark库？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参阅《JupyterLab用户指南》的[附录部分。](./jupyterlab/overview.md#supported-libraries)

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

有关[!DNL Spark]群集资源配置（包括可配置属性的完整列表）的更多信息，请参阅[JupyterLab用户指南](./jupyterlab/overview.md#kernels)。

## 为什么在尝试为较大的数据集执行某些任务时我会收到错误？

如果您收到错误，原因如下：`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`。这通常意味着驱动程序或执行器内存不足。 有关数据限制以及如何在大型数据集上执行任务的更多信息，请参阅JupyterLab Notebooks [数据访问](./jupyterlab/access-notebook-data.md)文档。 通常，可通过将`mode`从`interactive`更改为`batch`来解决此错误。

此外，在写入大型Spark/PySpark数据集时，在执行写入代码之前缓存数据(`df.cache()`)可以大大提高性能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在读取数据时遇到问题，并对数据应用转换，请尝试在转换之前缓存数据。 缓存数据可防止通过网络进行多次读取。 首先，读取数据。 接下来，缓存(`df.cache()`)数据。 最后，执行转换。

## 为什么我的Spark/PySpark笔记本在读写数据方面需要这么长时间？

如果对数据执行转换（如使用`fit()`），则转换可能会执行多次。 要提高性能，请在执行`fit()`之前使用`df.cache()`缓存数据。 这可确保转换只执行一次，并防止跨网络进行多次读取。

**推荐顺序：** 从读取数据开始。接下来，执行转换，然后缓存(`df.cache()`)数据。 最后，执行`fit()`。

## 为什么我的Spark/PySpark笔记本无法运行？

如果您收到以下任何错误：

- 由于暂存失败，作业中止……只能压缩每个分区中元素数量相同的RDD。
- 远程RPC客户端已断开关联，并出现其他内存错误。
- 读取和写入数据集时性能不佳。

检查以确保在写入数据之前缓存数据(`df.cache()`)。 在笔记本中执行代码时，在`fit()`等操作之前使用`df.cache()`可以大大提高笔记本的性能。 在写入数据集之前使用`df.cache()`可确保转换只执行一次，而不是多次。

## [!DNL Docker Hub] 数据科学工作区中的限制限制

自2020年11月20日起，对Docker Hub的匿名和免费认证使用的费率限制已生效。 匿名用户和免费[!DNL Docker Hub]用户每六小时最多只能收到100个容器图像拉取请求。 如果您受这些更改的影响，将收到以下错误消息：`ERROR: toomanyrequests: Too Many Requests.`或`You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`。

目前，此限制仅在您尝试在6小时内构建100个指向方法的笔记本时，或者如果您在数据科学工作区中使用基于Spark的笔记本时（经常进行放大和缩小），才会影响您的组织。 但是，这不太可能，因为在上运行的群集在空闲之前保持活动状态两个小时。 这会减少群集处于活动状态时所需的提取数。 如果收到上述任何错误，则需要等待[!DNL Docker]限制重置。

有关[!DNL Docker Hub]速率限制的更多信息，请访问[DockerHub文档](https://www.docker.com/increase-rate-limits)。 正在为此制定解决方案，并预期在后续版本中推出。
