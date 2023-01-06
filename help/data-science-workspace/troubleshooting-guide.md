---
keywords: Experience Platform；故障诊断；Data Science Workspace；热门主题
solution: Experience Platform
title: Data Science Workspace疑难解答指南
description: 本文档提供了有关Adobe Experience Platform Data Science Workspace的常见问题解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑难解答指南

本文档提供了有关Adobe Experience Platform的常见问题解答 [!DNL Data Science Workspace]. 有关 [!DNL Platform] API通常，请参阅 [Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md).

## JupyterLab笔记本查询状态在执行状态中卡住

JupyterLab Notebook可能表示某个单元处于执行状态，无限期地处于某些内存不足状态。 例如，在查询大型数据集或执行多个后续查询时，JupyterLab Notebook可能会耗尽可用内存来存储生成的数据帧对象。 在这种情况下，可以看到一些指标。 首先，即使单元格显示为 [`*`] 图标。 此外，底栏还指示已使用/可用的RAM数量。

![可用内存](./images/jupyterlab/user-guide/allocate-ram.png)

在数据读取期间，内存可能会增长，直到达到您分配的最大内存量为止。 一旦达到最大内存并重新启动内核，就会释放内存。 这意味着，由于内核重新启动，此情景中已用的内存可能显示为非常低，而在重新启动之前，内存将非常接近分配的最大RAM。

要解决此问题，请选择JupyterLab右上角的齿轮图标，然后将滑块滑动到右侧，然后选择 **[!UICONTROL 更新配置]** 分配更多内存。 此外，如果您正在运行多个查询，并且RAM值接近最大分配量，除非您需要来自先前查询的结果，否则请重新启动内核以重置可用的RAM量。 这可确保您拥有当前查询可用的最大RAM量。

![分配更多内存](./images/jupyterlab/user-guide/notebook-gpu-config.png)

如果您正在分配最大内存量(RAM)，但仍然遇到此问题，则可以修改查询以通过减少数据列或范围对较小的数据集大小进行操作。 要使用全部数据，建议您使用Spark笔记本。

## [!DNL JupyterLab] 环境未在中加载 [!DNL Google Chrome]

>[!IMPORTANT]
>
>此问题已得到解决，但可能仍存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器是最新的。

使用 [!DNL Google Chrome] 浏览器版本80.x中的“隐藏主体”页面，则默认情况下会阻止所有第三方Cookie。 此策略可以阻止 [!DNL JupyterLab] 从Adobe Experience Platform中加载。

要解决此问题，请执行以下步骤：

在 [!DNL Chrome] 浏览器，导航到右上方并选择 **设置** (或者，您也可以复制并粘贴地址栏中的“chrome://settings/”)。 接下来，滚动到页面底部，然后单击 **高级** 下拉列表。

![chrome高级](./images/faq/chrome-advanced.png)

的 **隐私和安全** 的上界。 接下来，单击 **网站设置** 后跟 **Cookie和网站数据**.

![chrome高级](./images/faq/privacy-security.png)

![chrome高级](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关”。

![chrome高级](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以禁用第三方Cookie并添加 [*.]ds.adobe.net到允许列表。

导航到地址栏中的“chrome://flags/”。 搜索并禁用标题为的标记 *&quot;默认为Cookie设置SameSite&quot;* 使用右侧的下拉菜单。

![禁用samesite标记](./images/faq/samesite-flag.png)

在步骤2之后，系统会提示您重新启动浏览器。 你重新启动后， [!DNL Jupyterlab] 应该可以访问。

## 为什么我无法访问 [!DNL JupyterLab] 在Safari中？

Safari默认在Safari &lt; 12中禁用第三方Cookie。 因为 [!DNL Jupyter] 虚拟机实例位于与其父框架不同的域上，Adobe Experience Platform当前要求启用第三方Cookie。 请启用第三方Cookie或切换到其他浏览器，例如 [!DNL Google Chrome].

对于Safari 12，您需要将用户代理切换到[!DNL Chrome]&#39;或&#39;[!DNL Firefox]&#39;。 要切换用户代理，请首先打开 *Safari* 菜单和选择 **首选项**. 此时将出现“首选项”窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择 **高级**. 然后，检查 *在菜单栏中显示“开发”菜单* 框中。 完成此步骤后，您可以关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

接下来，从顶部导航栏中选择 **开发** 菜单。 从 **开发** 下拉菜单，悬停鼠标 **用户代理**. 您可以选择 **[!DNL Chrome]** 或 **[!DNL Firefox]** 要使用的用户代理字符串。

![“开发”菜单](./images/faq/user-agent.png)

## 为什么在尝试上传或删除文件时，我看到“403禁止”消息 [!DNL JupyterLab]?

如果您的浏览器启用了广告拦截软件，例如 [!DNL Ghostery] 或 [!DNL AdBlock] 此外，必须允许每个广告拦截软件中使用域“\*.adobe.net”，以便 [!DNL JupyterLab] 正常运行。 这是因为 [!DNL JupyterLab] 虚拟机在与 [!DNL Experience Platform] 域。

## 为什么我的 [!DNL Jupyter Notebook] 被加扰或未呈现为代码？

如果相关的单元格意外从“代码”更改为“标记”，则可能会发生这种情况。 在代码单元格聚焦时，按键组合 **ESC+M** 将单元格的类型更改为Markdown。 单元格类型可以通过笔记本顶部选定单元格的下拉指示器进行更改。 要将单元格类型更改为代码，请首先选择要更改的给定单元格。 接下来，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义 [!DNL Python] 库？

的 [!DNL Python] 内核随许多常用的机器学习库一起预安装。 但是，您可以通过在代码单元格中执行以下命令来安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的完整列表 [!DNL Python] 库，请参阅 [JupyterLab用户指南的附录部分](./jupyterlab/overview.md#supported-libraries).

## 我能否安装自定义PySpark库？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参阅 [JupyterLab用户指南的附录部分](./jupyterlab/overview.md#supported-libraries).

## 是否可以配置 [!DNL Spark] 群集资源 [!DNL JupyterLab] [!DNL Spark] 还是PySpark内核？

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

有关 [!DNL Spark] 群集资源配置（包括可配置属性的完整列表），请参阅 [JupyterLab用户指南](./jupyterlab/overview.md#kernels).

## 为什么在尝试为较大的数据集执行某些任务时我会收到错误？

如果您收到错误，原因如下 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 这通常意味着驱动程序或执行器内存不足。 查看JupyterLab笔记本 [数据访问](./jupyterlab/access-notebook-data.md) 有关数据限制以及如何在大型数据集上执行任务的更多信息。 通常，通过更改 `mode` 从 `interactive` to `batch`.

此外，在编写大型Spark/PySpark数据集时，会缓存您的数据(`df.cache()`)之前执行写入代码可以大大提高性能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在读取数据时遇到问题，并对数据应用转换，请尝试在转换之前缓存数据。 缓存数据可防止通过网络进行多次读取。 首先，读取数据。 接下来，缓存(`df.cache()`)数据。 最后，执行转换。

## 为什么我的Spark/PySpark笔记本在读写数据方面需要这么长时间？

如果您对数据执行转换，例如使用 `fit()`，则转换可能会执行多次。 要提高性能，请使用 `df.cache()` 执行 `fit()`. 这可确保转换只执行一次，并防止跨网络进行多次读取。

**建议顺序：** 首先，读取数据。 接下来，执行转换，然后执行缓存(`df.cache()`)数据。 最后，执行 `fit()`.

## 为什么我的Spark/PySpark笔记本无法运行？

如果您收到以下任何错误：

- 由于暂存失败，作业中止……只能压缩每个分区中元素数量相同的RDD。
- 远程RPC客户端已断开关联，并出现其他内存错误。
- 读取和写入数据集时性能不佳。

检查以确保缓存数据(`df.cache()`)。 在笔记本中执行代码时，使用 `df.cache()` (例如 `fit()` 可大大提高笔记本性能。 使用 `df.cache()` 在编写数据集之前，请确保转换只执行一次，而不是多次。

## [!DNL Docker Hub] 数据科学工作区中的限制限制

自2020年11月20日起，对Docker Hub的匿名和免费认证使用的费率限制已生效。 匿名和免费 [!DNL Docker Hub] 用户每六小时最多可获得100个容器图像拉取请求。 如果您受这些更改的影响，将收到以下错误消息： `ERROR: toomanyrequests: Too Many Requests.` 或 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

目前，此限制仅在您尝试在6小时内构建100个指向方法的笔记本时，或者如果您在数据科学工作区中使用基于Spark的笔记本时（经常进行放大和缩小），才会影响您的组织。 但是，这不太可能，因为在上运行的群集在空闲之前保持活动状态两个小时。 这会减少群集处于活动状态时所需的提取数。 如果您收到上述任何错误，则需要等到 [!DNL Docker] 限制已重置。

有关 [!DNL Docker Hub] 速率限制，访问 [DockerHub文档](https://www.docker.com/increase-rate-limits). 正在为此制定解决方案，并预期在后续版本中推出。
