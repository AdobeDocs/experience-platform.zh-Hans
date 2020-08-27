---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: 数据科学工作区疑难解答指南
topic: Troubleshooting
description: 本文档提供有关Adobe Experience Platform数据科学工作区的常见问题解答。
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 疑难解答指南

此文档提供有关Adobe Experience Platform的常见问题的解答 [!DNL Data Science Workspace]。 有关API的一般问题 [!DNL Platform] 和疑难解答，请参阅 [Adobe Experience PlatformAPI疑难解答指南](../landing/troubleshooting.md)。

## [!DNL JupyterLab] 环境未加载 [!DNL Google Chrome]

>[!IMPORTANT]
>
>此问题已解决，但仍可能存在于Google Chrome 80.x浏览器中。 请确保您的Chrome浏览器是最新的。

浏览 [!DNL Google Chrome] 器版本80.x默认情况下会阻止所有第三方Cookie。 本政策可防止 [!DNL JupyterLab] 在Adobe Experience Platform内装载。

要解决此问题，请执行以下步骤：

在您 [!DNL Chrome] 的浏览器中，导航到右上角并选 **择设置** (或者，您也可以复制并粘贴地址栏中的“chrome://settings/”)。 然后，滚动到页面底部并单击“高级 **”** 下拉框。

![chrome advanced](./images/faq/chrome-advanced.png)

将出 *现“隐私和安全* ”部分。 接下来，单击“ **站点设置** ”，后 **跟Cookie和站点数据**。

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

最后，将“阻止第三方Cookie”切换为“关闭”。

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以禁用第三方cookie并添加 [*。]ds.adobe.net到允许列表。

导览至地址栏中的“chrome://flags/”。 使用右侧的下拉菜单 *搜索并禁用标题为* “默认SameSite by cookies”的标志。

![禁用samesite标志](./images/faq/samesite-flag.png)

步骤2后，系统会提示您重新启动浏览器。 重新启动后， [!DNL Jupyterlab] 应可访问。

## 为什么我无法在Safari [!DNL JupyterLab] 中访问？

默认情况下，在Safari&lt; 12中，Safari禁用第三方Cookie。 由于您 [!DNL Jupyter] 的虚拟机实例位于与其父帧不同的域上，因此Adobe Experience Platform当前要求启用第三方cookie。 请启用第三方Cookie或切换到其他浏览器，如 [!DNL Google Chrome]。

对于Safari 12，您需要将用户代理切换[!DNL Chrome]为“”或[!DNL Firefox]“”。 要切换用户代理，请打开Safari菜单 *开始* ，然后选择 **首选项**。 出现首选项窗口。

![Safari首选项](./images/faq/preferences.png)

在Safari首选项窗口中，选择高 **级**。 然后，选中菜 *单栏框中的“显示修改照片* ”菜单。 完成此步骤后，可关闭首选项窗口。

![Safari高级](./images/faq/advanced.png)

然后，从顶部导航栏中选择“开 **发** ”菜单。 从“开发” *下拉* ，将鼠标悬停在“用 *户代理”上*。 您可以选择 **[!DNL Chrome]** 要使用的 **[!DNL Firefox]** 或用户代理字符串。

![“开发”菜单](./images/faq/user-agent.png)

## 为什么在尝试上传或删除文件时会看到“403禁止”消息 [!DNL JupyterLab]?

如果您的浏览器启用了广告阻止软件( [!DNL Ghostery] 如 [!DNL AdBlock] 或Plus)，则必须允许每个广告阻止软件中的域“\*.adobe.net”才能正 [!DNL JupyterLab] 常运行。 这是因为 [!DNL JupyterLab] 虚拟机在与域不同的域中运 [!DNL Experience Platform] 行。

## 为什么我的某些部分 [!DNL Jupyter Notebook] 被加扰或不呈现为代码？

如果所涉单元格意外从“代码”更改为“标记”，则会发生这种情况。 当代码单元格被聚焦时，按 **键组合ESC** +M会将单元格的类型更改为Markdown。 单元格类型可以通过笔记本顶部的下拉列表指示符更改选定单元格的类型。 要将单元格类型更改为代码，请通过选择要更改的给定单元格进行开始。 然后，单击指示单元格当前类型的下拉列表，然后选择“代码”。

![](./images/faq/code_type.png)

## 如何安装自定义 [!DNL Python] 库？

该内 [!DNL Python] 核随许多流行的机器学习库预装。 但是，可以通过在代码单元格中执行以下命令来安装其他自定义库：

```shell
!pip install {LIBRARY_NAME}
```

有关预安装库的完整 [!DNL Python] 列表，请参 [阅《JupyterLab用户指南》的附录部分](./jupyterlab/overview.md#supported-libraries)。

## 能否安装自定义PySpark库？

很遗憾，您无法为PySpark内核安装其他库。 但是，您可以联系Adobe客户服务代表，为您安装自定义PySpark库。

有关预安装的PySpark库的列表，请参 [阅《JupyterLab用户指南》的附录部分](./jupyterlab/overview.md#supported-libraries)。

## 是否可以为PySpark内 [!DNL Spark] 核配置群 [!DNL JupyterLab] 集资 [!DNL Spark] 源？

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

有关群集资源配 [!DNL Spark] 置(包括可配置属性的完整列表)的详细信息，请参 [阅JupyterLab用户指南](./jupyterlab/overview.md#kernels)。