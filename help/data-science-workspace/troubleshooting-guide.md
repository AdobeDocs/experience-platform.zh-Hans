---
keywords: Experience Platform；疑难解答；数据科学工作区；热门主题
solution: Experience Platform
title: 数据科学工作区疑难解答指南
topic: Troubleshooting
description: 本文档提供有关Adobe Experience Platform数据科学工作区的常见问题解答。
translation-type: tm+mt
source-git-commit: 045ad186efac59317635439a05b9d24e703c9859
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 疑难解答指南

本文档提供有关Adobe Experience Platform[!DNL Data Science Workspace]的常见问题解答。 有关[!DNL Platform] API的一般问题和疑难解答，请参阅[Adobe Experience PlatformAPI疑难解答指南](../landing/troubleshooting.md)。

## [!DNL JupyterLab] 环境未加载  [!DNL Google Chrome]

>[!IMPORTANT]
>
>此问题已解决，但仍可能存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器是最新的。

在[!DNL Google Chrome]浏览器版本80.x中，默认情况下会阻止所有第三方Cookie。 此策略可以阻止[!DNL JupyterLab]在Adobe Experience Platform内加载。

要解决此问题，请执行以下步骤：

在[!DNL Chrome]浏览器中，导航到右上角并选择&#x200B;**设置**(或者，您也可以复制并粘贴地址栏中的“chrome://settings/”)。 接下来，滚动到页面底部并单击&#x200B;**高级**&#x200B;下拉列表。

![chrome advanced](./images/faq/chrome-advanced.png)

将显示&#x200B;**隐私和安全**&#x200B;部分。 接下来，单击&#x200B;**站点设置**，后跟&#x200B;**Cookie和站点数据**。

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关闭”。

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以禁用第三方Cookie并添加[*。]ds.adobe.net到允许列表。

导览至地址栏中的“chrome://flags/”。 使用右侧的下拉菜单搜索并禁用标题为&#x200B;*&quot;SameSite by default cookies&quot;*&#x200B;的标志。

![禁用samesite标志](./images/faq/samesite-flag.png)

步骤2后，系统会提示您重新启动浏览器。 重新启动后，应可访问[!DNL Jupyterlab]。

## 为什么我无法访问Safari中的[!DNL JupyterLab]?

默认情况下，在Safari&lt; 12中，Safari禁用第三方Cookie。 由于您的[!DNL Jupyter]虚拟机实例位于与其父帧不同的域上，Adobe Experience Platform当前要求启用第三方cookie。 请启用第三方Cookie或切换到其他浏览器，如[!DNL Google Chrome]。

对于Safari 12，您需要将用户代理切换为“[!DNL Chrome]”或“[!DNL Firefox]”。 要切换用户代理，请打开&#x200B;*Safari*&#x200B;菜单并选择&#x200B;**首选项**&#x200B;进行开始。 出现首选项窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择&#x200B;**高级**。 然后，选中菜单栏&#x200B;*中的*“显示修改照片”菜单。 完成此步骤后，可关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

然后，从顶部导航栏中选择&#x200B;**“开发”**&#x200B;菜单。 从&#x200B;**开发**&#x200B;下拉列表中，将指针悬停在&#x200B;**用户代理**&#x200B;上。 您可以选择要使用的&#x200B;**[!DNL Chrome]**&#x200B;或&#x200B;**[!DNL Firefox]**&#x200B;用户代理字符串。

![“开发”菜单](./images/faq/user-agent.png)

## 为什么在尝试上传或删除[!DNL JupyterLab]中的文件时，我会看到“403禁止”消息？

如果您的浏览器启用了广告阻止软件（如[!DNL Ghostery]或[!DNL AdBlock] Plus），则必须允许每个广告阻止软件中的域“\*.adobe.net”,[!DNL JupyterLab]才能正常运行。 这是因为[!DNL JupyterLab]虚拟机在与[!DNL Experience Platform]域不同的域上运行。

## 为什么我的[!DNL Jupyter Notebook]的某些部分看起来被加扰了，或者不呈现为代码？

如果所涉单元格意外从“代码”更改为“标记”，则会发生这种情况。 当代码单元格被聚焦时，按&#x200B;**ESC+M**&#x200B;键组合会将单元格的类型更改为Markdown。 单元格类型可以通过笔记本顶部的下拉列表指示符更改选定单元格的类型。 要将单元格类型更改为代码，请通过选择要更改的给定单元格进行开始。 然后，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义[!DNL Python]库？

[!DNL Python]内核预装了许多流行的机器学习库。 但是，可以通过在代码单元格中执行以下命令来安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的[!DNL Python]库的完整列表，请参见JupyterLab用户指南](./jupyterlab/overview.md#supported-libraries)的[附录部分。

## 能否安装自定义PySpark库？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参阅《JupyterLab用户指南》的[附录部分](./jupyterlab/overview.md#supported-libraries)。

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

有关[!DNL Spark]群集资源配置的详细信息(包括可配置属性的完整列表)，请参阅[JupyterLab用户指南](./jupyterlab/overview.md#kernels)。

## 为什么在尝试为较大的数据集执行某些任务时会收到错误？

如果收到错误，原因如`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`。这通常意味着驱动程序或执行器内存不足。 有关数据限制以及如何在大数据集上执行任务的更多信息，请参见JupyterLab笔记本[数据访问](./jupyterlab/access-notebook-data.md)文档。 通常，可通过将`mode`从`interactive`更改为`batch`来解决此错误。

## [!DNL Docker Hub] 数据科学工作区中的限制限制

自2020年11月20日起，对Docker Hub的匿名和免费认证使用的费率限制生效。 匿名和免费[!DNL Docker Hub]用户每六小时仅限100个容器图像拉取请求。 如果您受到这些更改的影响，您将收到以下错误消息：`ERROR: toomanyrequests: Too Many Requests.`或`You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`。

目前，此限制仅在您尝试在6小时内构建100个按方法制作的笔记本，或者您在数据科学工作区中使用基于Spark的笔记本时（经常进行放大和缩小），才会影响您的组织。 但是，这是不太可能的，因为在上运行的群集在空闲之前保持活动状态两个小时。 这会减少群集处于活动状态时所需的拉入数。 如果收到上述任何错误，您需要等待[!DNL Docker]限制重置。

有关[!DNL Docker Hub]速率限制的详细信息，请访问[DockerHub文档](https://www.docker.com/increase-rate-limits)。 正在为此制定解决方案，并期待在后续版本中提供。