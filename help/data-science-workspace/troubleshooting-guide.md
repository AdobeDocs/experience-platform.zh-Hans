---
keywords: Experience Platform；故障排除；Data Science Workspace；热门主题
solution: Experience Platform
title: Data Science Workspace故障排除指南
description: 本文档提供了有关Adobe Experience Platform数据科学工作区的常见问题解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答 [!DNL Data Science Workspace]. 有关以下内容的问题和疑难解答： [!DNL Platform] API一般而言，请参阅 [Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md).

## JupyterLab Notebook查询状态停滞在执行状态

JupyterLab Notebook可能指示某个单元格在某些内存不足的情况下无限期地处于执行状态。 例如，在查询大型数据集或执行多个后续查询时，JupyterLab Notebook可能会耗尽可用内存以存储生成的数据流对象。 在此情况下可以看到一些指标。 首先，即使单元格显示为正在执行，内核也会进入空闲状态。 [`*`] 单元格旁边的图标。 此外，底栏显示已使用/可用的RAM数量。

![可用ram](./images/jupyterlab/user-guide/allocate-ram.png)

在读取数据期间，内存可能会一直增长，直到达到您分配的最大内存量。 一旦达到最大内存，并且内核重新启动，就会释放内存。 这意味着，由于内核重新启动，在此情况下使用的内存可能显示为非常低，而就在重新启动之前，内存将非常接近分配的最大RAM。

要解决此问题，请选择JupyterLab右上角的齿轮图标，然后将滑块滑向右侧，然后选择 **[!UICONTROL 更新配置]** 分配更多RAM。 此外，如果您正在运行多个查询，并且RAM值接近分配的最大量，除非您需要以前查询的结果，请重新启动内核以重置可用的RAM量。 这可确保您拥有可用于当前查询的最大RAM量。

![分配更多ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

如果您在分配最大内存量(RAM)但仍遇到此问题，您可以通过减少列或数据范围来修改查询，以便对较小的数据集大小进行操作。 要使用全部数据，建议您使用Spark笔记本。

## [!DNL JupyterLab] 环境未加载 [!DNL Google Chrome]

>[!IMPORTANT]
>
>此问题已得到解决，但可能仍然存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器处于最新状态。

使用 [!DNL Google Chrome] 浏览器版本80.x中，默认情况下会阻止所有第三方Cookie。 此策略可以阻止 [!DNL JupyterLab] 从Adobe Experience Platform中加载。

要解决此问题，请执行以下步骤：

在您的 [!DNL Chrome] 浏览器，导航到右上角并选择 **设置** (或者，您可以复制并粘贴“chrome://settings/”到地址栏中)。 接下来，滚动到页面底部，然后单击 **高级** 下拉菜单。

![chrome高级](./images/faq/chrome-advanced.png)

此 **隐私和安全性** 部分。 接下来，单击 **站点设置** 后接 **Cookie和网站数据**.

![chrome高级](./images/faq/privacy-security.png)

![chrome高级](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关闭”。

![chrome高级](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您可以禁用第三方Cookie并添加 [*.]ds.adobe.net以访问允许列表。

在地址栏中导航到“chrome://flags/”。 搜索并禁用标题为的标记 *&quot;默认为Cookie设置SameSite&quot;* 使用右侧的下拉菜单。

![禁用samesite标志](./images/faq/samesite-flag.png)

在步骤2之后，系统会提示您重新启动浏览器。 你重新启动后， [!DNL Jupyterlab] 应该易于访问。

## 为什么我无法访问 [!DNL JupyterLab] 在Safari中？

Safari在Safari &lt; 12中默认禁用第三方Cookie。 因为您的 [!DNL Jupyter] 虚拟机实例与其父框架驻留在不同的域上，Adobe Experience Platform当前要求启用第三方Cookie。 请启用第三方Cookie或切换到其他浏览器，例如 [!DNL Google Chrome].

对于Safari 12，您需要将用户代理切换到&#39;[!DNL Chrome]&#39;或&#39;[!DNL Firefox]&#39;. 要切换用户代理，请首先打开 *Safari* 菜单并选择 **首选项**. 将出现首选项窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择 **高级**. 然后查看 *在菜单栏中显示开发菜单* 盒子。 完成此步骤后，可以关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

接下来，从顶部导航栏中选择 **开发** 菜单。 从 **开发** 下拉列表，悬停在 **用户代理**. 您可以选择 **[!DNL Chrome]** 或 **[!DNL Firefox]** 要使用的用户代理字符串。

![“开发”菜单](./images/faq/user-agent.png)

## 为什么我在尝试上传或删除中的文件时看到“403禁止访问”消息 [!DNL JupyterLab]？

如果您的浏览器已启用广告阻止软件，例如 [!DNL Ghostery] 或 [!DNL AdBlock] 此外，每个播发阻止软件中必须允许使用域“\*.adobe.net” [!DNL JupyterLab] 才能正常运行。 这是因为 [!DNL JupyterLab] 虚拟机运行的域与 [!DNL Experience Platform] 域。

## 为什么我的某些部分 [!DNL Jupyter Notebook] 看起来混乱或不呈现为代码？

如果意外地将相关单元格从“代码”更改为“Markdown”，则可能会发生这种情况。 当代码单元格处于焦点时，按下按键组合 **ESC+M** 将单元格类型更改为Markdown。 可以通过笔记本顶部的下拉指示器更改选定单元格的类型。 要将单元格类型更改为代码，请从选择要更改的给定单元格开始。 接下来，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义 [!DNL Python] 图书馆？

此 [!DNL Python] kernel预装了许多流行的机器学习库。 但是，通过在代码单元格中执行以下命令，可以安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的完整列表 [!DNL Python] 库，请参见 [JupyterLab用户指南的附录部分](./jupyterlab/overview.md#supported-libraries).

## 我可以安装自定义PySpark库吗？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参见 [JupyterLab用户指南的附录部分](./jupyterlab/overview.md#supported-libraries).

## 是否可以配置 [!DNL Spark] 群集资源 [!DNL JupyterLab] [!DNL Spark] 或PySpark内核？

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

有关的详细信息 [!DNL Spark] 群集资源配置，包括可配置属性的完整列表，请参见 [JupyterLab用户指南](./jupyterlab/overview.md#kernels).

## 为什么在尝试为较大的数据集执行某些任务时收到错误？

如果您收到错误的原因有 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 这通常意味着驱动程序或执行器的内存不足。 查看JupyterLab Notebooks [数据访问](./jupyterlab/access-notebook-data.md) 文档，以了解有关数据限制以及如何对大型数据集执行任务的更多信息。 通常，此错误可通过更改 `mode` 起始日期 `interactive` 到 `batch`.

此外，在写入大型Spark/PySpark数据集时，缓存您的数据(`df.cache()`)可以极大地提高性能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在读取数据时遇到问题并且正在将转换应用于数据，请尝试在转换之前缓存数据。 缓存数据可防止通过网络进行多次读取。 首先从读取数据开始。 下一步，缓存(`df.cache()`)数据。 最后，执行转换。

## 为什么我的Spark/PySpark笔记本要花这么长时间来读写数据？

如果您对数据执行转换，例如使用 `fit()`，则转换可能会执行多次。 为了提高性能，请使用以下代码缓存数据： `df.cache()` 执行 `fit()`. 这样可确保仅执行一次转换，并防止通过网络进行多次读取。

**推荐顺序：** 首先从读取数据开始。 接下来，执行转换后进行缓存(`df.cache()`)数据。 最后，执行 `fit()`.

## 为什么我的Spark/PySpark笔记本无法运行？

如果收到以下任何错误：

- 由于暂存失败，作业已中止……只能压缩每个分区中具有相同元素数的RDD。
- 远程RPC客户端已取消关联和其他内存错误。
- 读取和写入数据集时性能不佳。

检查以确保您正在缓存数据(`df.cache()`)，然后再写入数据。 在笔记本中执行代码时，使用 `df.cache()` 在操作(例如 `fit()` 可以大大提高笔记本电脑的性能。 使用 `df.cache()` 在写入数据集之前，可以确保仅执行一次转换，而不是多次。

## [!DNL Docker Hub] 数据科学工作区中的限制限制

自2020年11月20日起，对匿名和自由身份验证使用Docker Hub的费率限制已生效。 匿名和免费 [!DNL Docker Hub] 每六小时，用户最多只能收到100个容器图像提取请求。 如果您受这些更改影响，您将收到此错误消息： `ERROR: toomanyrequests: Too Many Requests.` 或 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

目前，仅当您尝试在六小时内构建100台笔记本到配方时，或者如果您在数据科学工作区中使用经常进行放大和缩小的基于Spark的笔记本时，此限制才会影响您的组织。 但是，这不太可能，因为这些群集在空闲之前保持活动状态两个小时。 这减少了群集处于活动状态时所需的Pull数。 如果您收到上述任何错误，则需要等到您的 [!DNL Docker] 限制已重置。

有关详情，请参阅 [!DNL Docker Hub] 速率限制，请访问 [DockerHub文档](https://www.docker.com/increase-rate-limits). 我们正在研究此问题的解决方案，预计将在后续版本中推出。
