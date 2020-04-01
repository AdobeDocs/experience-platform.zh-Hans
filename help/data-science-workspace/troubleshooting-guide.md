---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: 数据科学工作区疑难解答指南
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# 数据科学工作区疑难解答指南

本文档提供有关Adobe Experience Platform Data Science Workspace的常见问题解答。 有关Platform API的一般问题和疑难解答，请参阅 [Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

## JupyterLab环境未在Google Chrome中加载

将Google Chrome浏览器最新更新至版本80.x后，默认情况下将阻止所有第三方Cookie。 此新策略可以阻止JupyterLab在Adobe Experience Platform中加载。

>[!NOTE] 这是一个暂时的问题。 对第三方Cookie的依赖性设置为在将来的版本中删除。

要解决此问题，请执行以下步骤：

在Chrome浏览器中，导航到右上角并选择“设置” **** (或者，您也可以复制并粘贴地址栏中的“chrome://settings/”)。 然后，滚动到页面底部，单击“高级”下 **拉框** 。

![chrome高级](./images/faq/chrome-advanced.png)

将显 *示“隐私和安全* ”部分。 接下来，单击“ **站点设置** ”，后 **跟Cookie和站点数据**。

![chrome高级](./images/faq/privacy-security.png)

![chrome高级](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关闭”。

![chrome高级](./images/faq/toggle-off.png)

>[!NOTE] 或者，您也可以禁用第三方Cookie和白名 [单*。]ds.adobe.net

导览至地址栏中的“chrome://flags/”。 使用右侧的下拉菜单搜 *索并禁用标题为“SameSite by default cookies* ”的标记。

![禁用samesite标记](./images/faq/samesite-flag.png)

步骤2后，系统会提示您重新启动浏览器。 重新启动后，Jupyterlab应可访问。

## 为什么我无法在Safari中访问JupyterLab?

默认情况下，Safari会禁用第三方Cookie。 由于Jupyter虚拟机实例位于与其父帧不同的域上，因此Adobe Experience Platform当前要求启用第三方Cookie。 请启用第三方Cookie或切换到其他浏览器，如Google Chrome。

## 为什么在JupyterLab中上传或删除文件时，我会看到“403禁止”消息？

如果您的浏览器启用了广告阻止软件（如Ghostery或AdBlock Plus），则域“\*.adobe.net”必须在每个广告阻止软件中列入白名单，JupyterLab才能正常运行。 这是因为JupyterLab虚拟机在与Experience Platform域不同的域上运行。

## 为什么我的Jupyter笔记本的某些部分看起来有些乱七八糟，或者没有作为代码呈现？

如果所涉及的单元格意外地从“代码”更改为“标记”，则可能发生这种情况。 当代码单元格被聚焦时，按 **ESC+M组合键** ，将单元格的类型更改为Markdown。 单元格类型可以通过笔记本顶部的下拉列表指示符来更改选定单元格的类型。 要将单元格类型更改为代码，请通过选择要更改的给定单元格进行开始。 接下来，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义Python库？

Python内核预装了许多流行的机器学习库。 但是，您可以通过在代码单元格中执行以下命令来安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装的Python库的完整列表，请参阅JupyterLab [用户指南的附录部分](./jupyterlab/overview.md#supported-libraries)。

## 是否可以安装自定义PySpark库？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参阅《JupyterLab [用户指南》的附录部分](./jupyterlab/overview.md#supported-libraries)。

## 是否可以为JupyterLab Spark或PySpark内核配置Spark群集资源？

您可以通过向笔记本的第一个单元格添加以下块来配置资源：

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

有关Spark群集资源配置的详细信息(包括可配置属性的完整列表)，请参阅《 [JupyterLab用户指南》](./jupyterlab/overview.md#pyspark-spark-execution-resource)。